<properties
   pageTitle="Implantar um aplicativo Node.js usando MongoDB | Microsoft Azure"
   description="Instruções passo a passo sobre como empacotar executáveis convidados para implantar em um cluster do Service Fabric do Azure"
   services="service-fabric"
   documentationCenter=".net"
   authors="bmscholl"
   manager=""
   editor=""/>

<tags
   ms.service="service-fabric"
   ms.devlang="dotnet"
   ms.topic="article"
   ms.tgt_pltfrm="NA"
   ms.workload="NA"
   ms.date="05/17/2016"
   ms.author="bscholl"/>


# Implantar vários executáveis de convidado

Este artigo mostra como empacotar e implantar vários executáveis convidados no Service Fabric do Azure usando a versão de visualização da ferramenta de empacotamento Service Fabric, disponível em [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool).

Para criar um pacote de Service Fabric manualmente, examine como [implantar um convidado executável ao Service Fabric](service-fabric-deploy-existing-app.md).

Embora este passo a passo mostre como implantar um aplicativo com um front-end Node.js que usa MongoDB como o repositório de dados, você pode aplicar as etapas a qualquer aplicativo que tenha dependências de outro aplicativo.

## Empacotar o aplicativo Node.js

Este artigo pressupõe que o Node.js não esteja instalado em nós do cluster do Service Fabric. Como consequência, você precisa adicionar o Node.exe ao diretório raiz de seu aplicativo de nó antes do empacotamento. A estrutura de diretórios do aplicativo Node.js (usando a estrutura da Web Express e o mecanismo de modelagem Jade) deve ser semelhante ao mostrado abaixo:

```
|-- NodeApplication
	|-- bin
        |-- www
	|-- node_modules
        |-- .bin
        |-- express
        |-- jade
        |-- etc.
	|-- public
        |-- images
        |-- etc.
	|-- routes
        |-- index.js
        |-- users.js
    |-- views
        |-- index.jade
        |-- etc.
    |-- app.js
    |-- package.json
    |-- node.exe
```

Como uma próxima etapa, crie um pacote de aplicativos para o aplicativo Node.js. O código a seguir cria um pacote de aplicativos do Service Fabric que contém o aplicativo Node.js.

```
.\ServiceFabricAppPackageUtil.exe /source:'[yourdirectory]\MyNodeApplication' /target:'[yourtargetdirectory] /appname:NodeService /exe:'node.exe' /ma:'bin/www' /AppType:NodeAppType
```

Veja a seguir uma descrição dos parâmetros que estão sendo usados:

- **/source**: aponta para o diretório do aplicativo que deve ser empacotado.
- **/target**: define o diretório no qual o pacote deve ser criado. Esse diretório deve ser diferente do diretório de origem.
- **/appname**: define o nome do aplicativo existente. É importante entender que isso significa o nome do serviço no manifesto, e não o nome do aplicativo do Service Fabric.
- **/exe**: define o arquivo executável que o Service Fabric deve iniciar, neste caso `node.exe`.
- **/ma**: define o argumento usado para iniciar o arquivo executável. Como o Node.js não está instalado, o Service Fabric precisa iniciar o servidor Web do Node.js executando `node.exe bin/www`. `/ma:'bin/www'` informa à ferramenta de empacotamento para usar `bin/ma` como o argumento para node.exe.
- **/AppType**: define o nome do tipo de aplicativo do Service Fabric.

Se você navegar até o diretório especificado no parâmetro /target, será possível ver que a ferramenta criou um pacote totalmente funcional do Service Fabric, como mostrado abaixo:

```
|--[yourtargetdirectory]
    |-- NodeApplication
        |-- C
		      |-- bin
              |-- data
              |-- node_modules
              |-- public
              |-- routes
              |-- views
              |-- app.js
              |-- package.json
              |-- node.exe
        |-- config
		      |--Settings.xml
	    |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```
Agora, o ServiceManifest.xml gerado tem uma seção que descreve como o servidor Web do Node.js deve ser iniciado, como mostrado no trecho de código a seguir:

```xml
<CodePackage Name="C" Version="1.0">
    <EntryPoint>
        <ExeHost>
            <Program>node.exe</Program>
            <Arguments>'bin/www'</Arguments>
            <WorkingFolder>CodePackage</WorkingFolder>
        </ExeHost>
    </EntryPoint>
</CodePackage>
```
Neste exemplo, o servidor Web do Node.js escuta a porta 3000, portanto, você precisa atualizar as informações do ponto de extremidade no arquivo ServiceManifest.xml, como mostrado abaixo.

```xml
<Resources>
      <Endpoints>
     	<Endpoint Name="NodeServiceEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
</Resources>
```
Agora que você empacotou o aplicativo Node.js, prossiga e empacote o MongoDB. Como mencionado anteriormente, as etapas que você percorrer agora não são específicas do Node.js e MongoDB. Na verdade, elas se aplicam a todos os aplicativos que devem ser empacotados juntamente como um único aplicativo do Service Fabric.

Para empacotar o MongoDB, convém empacotar os arquivos Mongod.exe e Mongo.exe. Os dois binários estão localizados no diretório `bin` do diretório de instalação do MongoDB. A estrutura de diretórios é parecida com o seguinte.

```
|-- MongoDB
	|-- bin
        |-- mongod.exe
        |-- mongo.exe
        |-- anybinary.exe
```
O Service Fabric precisa iniciar o MongoDB com um comando semelhante ao mostrado abaixo e, portanto, você precisa usar o parâmetro `/ma` ao empacotar o MongoDB.

```
mongod.exe --dbpath [path to data]
```
> [AZURE.NOTE] Os dados não serão preservados no caso de uma falha de nó se você colocar o diretório de dados do MongoDB no diretório local do nó. Você deve usar o armazenamento durável ou implementar um conjunto de réplicas do MongoDB para evitar a perda de dados.

No PowerShell ou no shell de comando, executamos a ferramenta de empacotamento com os seguintes parâmetros:

```
.\ServiceFabricAppPackageUtil.exe /source: [yourdirectory]\MongoDB' /target:'[yourtargetdirectory]' /appname:MongoDB /exe:'bin\mongod.exe' /ma:'--dbpath [path to data]' /AppType:NodeAppType
```

Para adicionar o MongoDB ao seu pacote de aplicativos do Service Fabric é necessário garantir que o parâmetro /target aponte para o mesmo diretório que já contém o manifesto do aplicativo com o aplicativo Node.js. Também é preciso garantir que você esteja usando o mesmo nome de ApplicationType.

Vamos navegar até o diretório e examinar o que a ferramenta criou.

```
|--[yourtargetdirectory]
    |-- MyNodeApplication
    |-- MongoDB
        |-- C
            |--bin
                |-- mongod.exe
                |-- mongo.exe
                |-- etc.
        |-- config
		    |--Settings.xml
	    |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```
Como você pode ver, a ferramenta adicionou uma nova pasta, MongoDB, ao diretório que contém os binários do MongoDB. Se você abrir o arquivo `ApplicationManifest.xml`, poderá ver que agora o pacote contém o aplicativo Node.js e o MongoDB. O código a seguir mostra o conteúdo do manifesto do aplicativo.

```xml
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyNodeApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MongoDB" ServiceManifestVersion="1.0" />
   </ServiceManifestImport>
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeService" ServiceManifestVersion="1.0" />
   </ServiceManifestImport>
   <DefaultServices>
      <Service Name="MongoDBService">
         <StatelessService ServiceTypeName="MongoDB">
            <SingletonPartition />
         </StatelessService>
      </Service>
      <Service Name="NodeServiceService">
         <StatelessService ServiceTypeName="NodeService">
            <SingletonPartition />
         </StatelessService>
      </Service>
   </DefaultServices>
</ApplicationManifest>  
```

A última etapa é publicar o aplicativo no cluster do Service Fabric local usando os scripts do PowerShell abaixo:

```
Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath '[yourtargetdirectory]' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'NodeAppType'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'NodeAppType'

New-ServiceFabricApplication -ApplicationName 'fabric:/NodeApp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0  
```

Depois que o aplicativo for publicado com êxito no cluster local, você poderá acessar o aplicativo Node.js na porta inserida no manifesto do serviço do aplicativo Node.js, por exemplo http://localhost:3000.

Neste tutorial, você viu como empacotar facilmente dois aplicativos existentes como um único aplicativo do Service Fabric. Você também aprendeu como implantá-lo no Service Fabric para que ele possa beneficiar dos recursos do Service Fabric, como alta disponibilidade e integração do sistema de integridade.

## Próximas etapas

- Saiba como [empacotar um aplicativo convidado manualmente](service-fabric-deploy-existing-app.md).

<!---HONumber=AcomDC_0518_2016-->