<properties 
	pageTitle="Criar uma aplicativo Web Hello World para o Azure no Eclipse | Microsoft Azure" 
	description="Este tutorial mostra como usar o Kit de Ferramentas do Azure para Eclipse para criar um aplicativo Web Hello World para o Azure." 
	services="app-service\web" 
	documentationCenter="java" 
	authors="rmcmurray" 
	manager="wpickett" 
	editor=""/>

<tags 
	ms.service="app-service-web" 
	ms.workload="web" 
	ms.tgt_pltfrm="na" 
	ms.devlang="Java" 
	ms.topic="article" 
	ms.date="06/07/2016" 
	ms.author="robmcm"/>

# Criar uma aplicativo Web Hello World para o Azure no Eclipse

Este tutorial mostra como criar e implantar um aplicativo Hello World básico para o Azure como um aplicativo Web usando o [Kit de Ferramentas do Azure para Eclipse]. Um exemplo básico de JSP é exibido para manter a simplicidade, mas etapas muito semelhantes podem ser apropriadas para um servlet Java quando o assunto é a implantação do Azure.

Após a conclusão deste tutorial, seu aplicativo será semelhante à ilustração a seguir quando exibido em um navegador da Web:

![][01]
 
## Pré-requisitos

* Um JDK (Java Developer Kit) versão 1.7 ou posterior.
* Um IDE do Eclipse para desenvolvedores do Java EE, Indigo ou posterior. Isso pode ser baixado em <http://www.eclipse.org/downloads/>.
* Uma distribuição de um servidor Web ou de um servidor de aplicativo baseado em Java, como o Apache Tomcat ou o Jetty.
* Uma assinatura do Azure, que pode ser adquirida de <https://azure.microsoft.com/free/> ou de <http://azure.microsoft.com/pricing/purchase-options/>.
* O Kit de Ferramentas do Azure para Eclipse. Para saber mais, confira [Instalação do Kit de Ferramentas do Azure para Eclipse].

## Para criar um aplicativo Hello World

Primeiro, vamos começar com a criação de um projeto Java.

1. Inicie o Eclipse, no menu clique em **Arquivo**, clique em **Novo** e depois em **Projeto Web Dinâmico**. (Se você não vir o **Projeto Web Dinâmico** listado como um projeto disponível depois de clicar em **Arquivo** e em **Novo**, faça o seguinte: clique em **Arquivo**, clique em **Novo**, clique em **Projeto...**, expanda **Web**, clique em **Projeto Web Dinâmico** e clique em **Avançar**).

1. Para o objetivo deste tutorial, nomeie o projeto **MyHelloWorld**. Sua tela será semelhante à seguinte:

   ![][02]

1. Clique em **Concluir**.

1. No modo de exibição do Gerenciador de Projeto do Eclipse, expanda **MyHelloWorld**. Clique com o botão direito do mouse em **WebContent**, clique em **Novo** e, em seguida, clique em **Arquivo JSP**.

1. Na caixa de diálogo **Novo arquivo JSP**, nomeie o arquivo **index.jsp**. Mantenha a pasta pai como **MyHelloWorld/WebContent**.

1. Na caixa de diálogo **Selecionar Modelo JSP**, para a finalidade deste tutorial, escolha **Novo Arquivo JSP (html)** e clique em **Concluir**.

1. Quando o arquivo index.jsp for aberto no Eclipse, adicione o texto para exibir dinamicamente **Hello World!** dentro do elemento `<body>` existente. Seu conteúdo do `<body>` atualizado deve ser parecido com o exemplo a seguir:

   `<body><b><% out.println("Hello World!"); %></b></body>`

1. Salve o index.jsp.

## Para implantar seu aplicativo em um contêiner de aplicativos Web do Azure

Há várias maneiras pelas quais você pode implantar um aplicativo Web Java no Azure. Este tutorial descreve uma das mais simples: o aplicativo será implantado em um contêiner de aplicativos Web do Azure, e não há a necessidade de qualquer tipo de projeto especial nem de ferramentas adicionais. O JDK e o software do contêiner da Web serão fornecidos a você pelo Azure, portanto, não é necessário carregar seu próprio; tudo o que você precisa é de seu aplicativo Web Java. Como resultado, o processo de publicação de seu aplicativo demorará segundos, e não minutos.

1. No Gerenciador de Projetos do Eclipse, clique com o botão direito do mouse em **MyHelloWorld**.

1. No menu de contexto, selecione **Azure** e clique em **Publicar como Aplicativo Web do Azure...**

   ![][03]
   
   Como alternativa, enquanto o projeto do aplicativo Web é selecionado no Explorador de Projeto, é possível clicar no botão suspenso **Publicar** na barra de ferramentas e selecionar **Publicar como Aplicativo Web do Azure** lá:
   
   ![][14]
   
1. Se você ainda não entrou no Azure por meio do Eclipse, será solicitado que você entre em sua conta do Azure:

   ![][04]
   
   Observação: se você tiver várias contas do Azure, alguns dos avisos mostrados durante o processo de entrada poderão ser exibidos mais de uma vez, mesmo se forem, aparentemente, os mesmos. Quando isso acontecer, continue seguindo as instruções de entrada.
1. Após o logon bem-sucedido em sua conta do Azure, a caixa de diálogo **Gerenciar Assinaturas** exibirá uma lista de assinaturas associadas às suas credenciais. Se houver várias assinaturas listadas e se você quiser trabalhar com apenas um subconjunto específico delas, poderá, opcionalmente, desmarcar as que deseja usar. Depois de selecionar suas assinaturas, clique em **Fechar**.

   ![][05]
   
1. Quando a caixa de diálogo **Implantar no Contêiner do Aplicativo Web do Azure** for mostrada, ela exibirá todos os contêineres do Aplicativo Web criados anteriormente por você; se você não tiver criado nenhum contêiner, a lista estará vazia.

   ![][06]
   
1. Se você nunca tiver criado um contêiner de aplicativos Web do Azure, ou se quiser publicar seu aplicativo em um novo contêiner, use as etapas a seguir. Caso contrário, selecione um Contêiner de Aplicativo Web existente e pule para a etapa 7 abaixo.

  1. Clique em **Novo...**

        ![][15]

  1. A caixa de diálogo **Novo Contêiner do Aplicativo Web** será exibida:

        ![][07]

  1. Insira um **Rótulo DNS** para seu Contêiner do Aplicativo Web; isso formará o rótulo DNS folha da URL do host de seu aplicativo Web no Azure. Observação: o nome deve estar disponível e de acordo com os requisitos de nomenclatura de aplicativo Web do Azure.

  1. No menu suspenso **Contêiner da Web**, selecione o software apropriado ao seu aplicativo.

        Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9. A recent distribution of the selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.

  1. No menu suspenso **Assinatura**, selecione a assinatura que deseja usar para essa implantação.

  1. No menu suspenso **Grupo de Recursos**, selecione o Grupo de Recursos com o qual deseja associar seu Aplicativo Web.

        Note: Azure Resource Groups allow you to group related resources together so that, for example, they can be deleted together.

        You can select an existing Resource Group (if you have any) and skip to step g below, or use the following these steps to create a new Resource Group:

      * Clique em **Novo...**

      * A caixa de diálogo **Novo Grupo de Recursos** será exibida:

            ![][08]

      * Na caixa de texto **Nome**, especifique um nome para o novo Grupo de Recursos.

      * No menu suspenso **Região**, selecione o local do data center do Azure apropriado ao Grupo de Recursos.

      * Clique em **OK**.

  1. O menu suspenso **Plano do Serviço de Aplicativo** lista os planos do serviço de aplicativo associados ao Grupo de Recursos selecionado.

        Note: An App Service Plan specifies information such as the location of your Web App, the pricing tier and the compute instance size. A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.

        You can select an existing App Service Plan (if you have any) and skip to step h below, or use the following these steps to create a new App Service Plan:

      * Clique em **Novo...**

      * A caixa de diálogo **Novo Plano do Serviço de Aplicativo** será exibida:

            ![][09]

      * Na caixa de texto **Nome**, especifique um nome para o novo Plano do Serviço de Aplicativo.

      * No menu suspenso **Local**, selecione o local do data center do Azure apropriado ao plano.

      * No menu suspenso **Tipo de Preço**, selecione o preço apropriado ao plano. Para fins de teste, é possível escolher **Gratuito**.

      * No menu suspenso **Tamanho da Instância**, selecione o tamanho de instância apropriado ao plano. Para fins de teste, é possível escolher **Pequeno**.

  1. Depois de concluir todas as etapas acima, a caixa de diálogo New Web App Container (Novo Contêiner de Aplicativos Web) deve ser semelhante à ilustração a seguir:

        ![][10]

  1. Clique em **OK** para concluir a criação do novo contêiner do Aplicativo Web.

        Wait a few seconds for the list of the Web App containers to be refreshed, and your newly-created web app container should now be selected in the list.

1. Agora você está pronto para concluir a implantação inicial de seu Aplicativo Web no Azure:

    ![][11]

    Clique em **OK** para implantar o aplicativo Java no contêiner do Aplicativo Web selecionado.

    Observação: por padrão, o aplicativo será implantado como um subdiretório do servidor de aplicativos. Se desejar implantá-lo como o aplicativo raiz, marque a caixa de seleção **Implantar na raiz** antes de clicar em **OK**.

1. Em seguida, você deverá ver o modo de exibição do **Log de Atividades do Azure**, que indicará o status da implantação do Aplicativo Web.

    ![][12]

    O processo de implantação de seu aplicativo Web no Azure deve demorar apenas alguns segundos para ser concluído. Quando o aplicativo estiver pronto, você verá um link chamado **Publicado** na coluna **Status**. Ao clicar no link, você será levado à home page do Aplicativo Web implantado.

## Atualização de seu aplicativo Web

A atualização de um aplicativo Web do Azure em execução é um processo rápido e fácil, e você tem duas opções de atualização:

* Você pode atualizar a implantação de um aplicativo Web Java existente.
* Você pode publicar um aplicativo Java adicional no mesmo contêiner de aplicativo Web.

Em ambos os casos, o processo é idêntico e demora apenas alguns segundos:

1. No explorador de projetos do Eclipse, clique com o botão direito do mouse no aplicativo Java que você deseja atualizar ou adicionar a um contêiner de aplicativos Web existente.

2. Quando o menu de contexto for exibido, selecione **Azure** e, em seguida, **Publicar como Aplicativo Web do Azure...**

3. Como você já fez logon anteriormente, verá uma lista com seus contêineres de aplicativo Web existentes. Selecione aquele no qual deseja publicar ou publicar novamente o aplicativo Java e clique em **OK**.

Após alguns segundos, o modo de exibição do **Log de Atividades do Azure** mostrará a implantação atualizada como **Publicada** e será possível verificar o aplicativo atualizado em um navegador da Web.

## Interromper um aplicativo Web existente

Para interromper um contêiner do Aplicativo Web do Azure existente, (incluindo todos os aplicativos Java implantados nele), é possível usar o modo de exibição do **Azure Explorer**.

Se o modo de exibição do **Azure Explorer** ainda não estiver aberto, você poderá abri-lo clicando no menu **Janela** no Eclipse, clicando em **Mostrar Modo de Exibição**, em **Outros...**, em **Azure** e em **Azure Explorer**. Se você não tiver feito logon anteriormente, receberá uma solicitação para fazê-lo.

Quando o modo de exibição do **Azure Explorer** for exibido, use estas etapas para interromper o Aplicativo Web:

1. Expanda o nó **Azure**.
2. Expanda o nó **Aplicativos Web**. 
3. Clique com botão direito do mouse no Aplicativo Web desejado.
5. Quando o menu de contexto for exibido, clique em **Parar**. ![][13]

## Próximas etapas

Para obter mais informações sobre os kits de ferramentas do Azure para Java IDEs, confira os links a seguir:

- [Kit de ferramentas do Azure para Eclipse]
  - [Instalação do Kit de Ferramentas do Azure para o Eclipse]
  - *Criar uma aplicativo Web Hello World para o Azure no Eclipse (este artigo)*
  - [Novidades no Kit de Ferramentas do Azure para o Eclipse]
- [Kit de Ferramentas do Azure para IntelliJ]
  - [Instalação do Kit de Ferramentas do Azure para IntelliJ]
  - [Criar um aplicativo Web Hello World para o Azure no IntelliJ]

Para obter mais informações sobre como usar o Azure com o Java, confira a [Central de desenvolvimento Java do Azure].

Para obter mais informações sobre como criar aplicativos Web do Azure, consulte a [Visão geral de Aplicativos Web].

[AZURE.INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Kit de Ferramentas do Azure para Eclipse]: ../azure-toolkit-for-eclipse.md
[Kit de Ferramentas do Azure para IntelliJ]: ../azure-toolkit-for-intellij.md
[Criar um aplicativo Web Hello World para o Azure no IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[Instalação do Kit de Ferramentas do Azure para Eclipse]: ../azure-toolkit-for-eclipse-installation.md
[Instalação do Kit de Ferramentas do Azure para o Eclipse]: ../azure-toolkit-for-eclipse-installation.md
[Instalação do Kit de Ferramentas do Azure para IntelliJ]: ../azure-toolkit-for-intellij-installation.md
[Novidades no Kit de Ferramentas do Azure para o Eclipse]: ../azure-toolkit-for-eclipse-whats-new.md

[Central de desenvolvimento Java do Azure]: https://azure.microsoft.com/develop/java/
[Visão geral de Aplicativos Web]: ./app-service-web-overview.md

<!-- IMG List -->

[01]: ./media/app-service-web-eclipse-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/app-service-web-eclipse-create-hello-world-web-app/02-Dynamic-Web-Project.png
[03]: ./media/app-service-web-eclipse-create-hello-world-web-app/03-Context-Menu.png
[04]: ./media/app-service-web-eclipse-create-hello-world-web-app/04-Log-In-Dialog.png
[05]: ./media/app-service-web-eclipse-create-hello-world-web-app/05-Manage-Subscriptions-Dialog.png
[06]: ./media/app-service-web-eclipse-create-hello-world-web-app/06-Deploy-To-Azure-Web-Container.png
[07]: ./media/app-service-web-eclipse-create-hello-world-web-app/07-New-Web-App-Container-Dialog.png
[08]: ./media/app-service-web-eclipse-create-hello-world-web-app/08-New-Resource-Group-Dialog.png
[09]: ./media/app-service-web-eclipse-create-hello-world-web-app/09-New-Service-Plan-Dialog.png
[10]: ./media/app-service-web-eclipse-create-hello-world-web-app/10-Completed-Web-App-Container-Dialog.png
[11]: ./media/app-service-web-eclipse-create-hello-world-web-app/11-Completed-Deploy-Dialog.png
[12]: ./media/app-service-web-eclipse-create-hello-world-web-app/12-Activity-Log-View.png
[13]: ./media/app-service-web-eclipse-create-hello-world-web-app/13-Azure-Explorer-Web-App.png
[14]: ./media/app-service-web-eclipse-create-hello-world-web-app/14-publishDropdownButton.png
[15]: ./media/app-service-web-eclipse-create-hello-world-web-app/15-New-Azure-Web-Container.png

<!---HONumber=AcomDC_0608_2016-->