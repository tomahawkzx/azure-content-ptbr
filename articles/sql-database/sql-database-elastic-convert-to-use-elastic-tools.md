<properties
   pageTitle="Migrar bancos de dados existentes para escala horizontal | Microsoft Azure"
   description="Converter bancos de dados fragmentados para usar ferramentas de banco de dados elástico criando um gerenciador de mapa de fragmentos"
   services="sql-database"
   documentationCenter=""
   authors="SilviaDoomra"
   manager="jhubbard"
   editor=""/>

<tags
   ms.service="sql-database"
   ms.devlang="NA"
   ms.topic="article"
   ms.tgt_pltfrm="NA"
   ms.workload="data-management"
   ms.date="04/26/2016"
   ms.author="SilviaDoomra"/>

# Migrar bancos de dados existentes para escala horizontal

Gerencie com facilidade seus bancos de dados fragmentados e escalonados horizontalmente existentes, usando as ferramentas de banco de dados do Banco de Dados SQL (como a [biblioteca de cliente do Banco de Dados Elástico](sql-database-elastic-database-client-library.md)). Você deve primeiro converter um conjunto existente de bancos de dados para usar o [gerenciador de mapa de fragmentos](sql-database-elastic-scale-shard-map-management.md).

## Visão geral
Para migrar um banco de dados fragmentado existente:

1. Prepare o [banco de dados do gerenciador de mapa de fragmentos](sql-database-elastic-scale-shard-map-management.md).
2. Criar o mapa de fragmentos.
3. Preparar os fragmentos individuais.  
2. Adicione os mapeamentos ao mapa de fragmentos.

Essas técnicas podem ser implementadas usando a [biblioteca de cliente .NET Framework](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) ou os scripts do PowerShell encontrados em [Azure SQL DB - Scripts de ferramentas de Banco de Dados Elástico](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db). Os exemplos aqui usam os scripts do PowerShell.

Para saber mais sobre o ShardMapManager, confira [Gerenciamento de mapa de fragmentos](sql-database-elastic-scale-shard-map-management.md). Para obter uma visão geral das ferramentas de banco de dados elástico, confira [Visão geral dos recursos do Banco de Dados Elástico](sql-database-elastic-scale-introduction.md).

## Preparar o banco de dados do gerenciador de mapa de fragmentos

O gerenciador de mapa de fragmentos é um banco de dados especial que contém os dados para gerenciar bancos de dados escalonados horizontalmente. Você pode usar um banco de dados existente ou criar um novo banco de dados. Observe que um banco de dados que atua como gerenciador de mapa de fragmentos não deve ser o mesmo banco de dados de um fragmento. Observe também que o script do PowerShell não cria o banco de dados para você.

## Etapa 1: criar um gerenciador de mapa de fragmentos

	# Create a shard map manager. 
	New-ShardMapManager -UserName '<user_name>' 
	-Password '<password>' 
	-SqlServerName '<server_name>' 
	-SqlDatabaseName '<smm_db_name>' 
	#<server_name> and <smm_db_name> are the server name and database name 
	# for the new or existing database that should be used for storing 
	# tenant-database mapping information.

### Para recuperar o gerenciador de mapa de fragmentos

Após a criação, você pode recuperar o gerenciador de mapa de fragmentos com este cmdlet. Esta etapa será necessária toda vez que você precisar usar o objeto ShardMapManager.

	# Try to get a reference to the Shard Map Manager  
	$ShardMapManager = Get-ShardMapManager -UserName '<user_name>' 
	-Password '<password>' 
	-SqlServerName '<server_name>' 
	-SqlDatabaseName '<smm_db_name>' 

  
## Etapa 2: criar o mapa de fragmentos

Você deve selecionar o tipo do mapa de fragmentos a criar. A escolha depende da arquitetura do banco de dados:

1. Um locatário único por banco de dados (para termos, consulte o [glossário](sql-database-elastic-scale-glossary.md).) 
2. Vários locatários por banco de dados (dois tipos):
	3. Mapeamento de lista
	4. Mapeamento de intervalo
 

Para um modelo de locatário único, crie um mapa de fragmentos de **mapeamento de lista**. O modelo de locatário único atribui um banco de dados por locatário. Esse é um modelo eficaz para desenvolvedores de SaaS, pois simplifica o gerenciamento.

![Mapeamento de lista][1]

O modelo multilocatário atribui vários locatários a um banco de dados individual (e você pode distribuir grupos de locatários entre vários bancos de dados). Use esse modelo quando você esperar que cada locatário tenha necessidades de dados pequenas. Nesse modelo, atribuímos um intervalo de locatários a um banco de dados usando **mapeamento de intervalo**.
 

![Mapeamento de intervalo][2]

Ou então, você pode implementar um modelo de banco de dados multilocatário usando um *mapeamento de lista* para atribuir vários locatários a um banco de dados individual. Por exemplo, DB1 é usado para armazenar informações sobre os locatários com IDs 1 e 5, e DB2 armazena dados dos locatários 7 e 10.

![Vários locatários em um banco de dados individual][3]

**Com base na sua escolha, escolha uma destas opções:**

### Opção 1: criar um mapa de fragmentos para um mapeamento de lista
Crie um mapa de fragmentos usando o objeto ShardMapManager.

	# $ShardMapManager is the shard map manager object. 
	$ShardMap = New-ListShardMap -KeyType $([int]) 
	-ListShardMapName 'ListShardMap' 
	-ShardMapManager $ShardMapManager 
 
 
### Opção 2: criar um mapa de fragmentos para um mapeamento de intervalo

Observe que, para utilizar esse padrão de mapeamento, os valores de ID de locatário precisam ser intervalos contínuos. É aceitável ter lacunas nos intervalos simplesmente ignorando o intervalo ao criar os bancos de dados.

	# $ShardMapManager is the shard map manager object 
	# 'RangeShardMap' is the unique identifier for the range shard map.  
	$ShardMap = New-RangeShardMap 
	-KeyType $([int]) 
	-RangeShardMapName 'RangeShardMap' 
	-ShardMapManager $ShardMapManager 

### Opção 3: mapeamentos de lista em um banco de dados individual
A configuração desse padrão também exige a criação de um mapa de lista conforme mostrado na etapa 2, opção 1.

## Etapa 3: preparar os fragmentos individuais

Adicione cada fragmento (banco de dados)ao gerenciador de mapa de fragmentos. Isso prepara os bancos de dados individuais para armazenar informações de mapeamento. Execute esse método em cada fragmento.
	 
	Add-Shard 
	-ShardMap $ShardMap 
	-SqlServerName '<shard_server_name>' 
	-SqlDatabaseName '<shard_database_name>'
	# The $ShardMap is the shard map created in step 2.
 

## Etapa 4: Adicionar mapeamentos

A adição de mapeamentos depende do tipo de mapa de fragmentos criado. Se tiver criado um mapa de lista, você adicionará mapeamentos de lista. Se tiver criado um mapa de intervalo, você adicionará mapeamentos de intervalo.

### Opção 1: mapear os dados para um mapeamento de lista

Mapeie os dados adicionando um mapeamento de lista para cada locatário.

	# Create the mappings and associate it with the new shards 
	Add-ListMapping 
	-KeyType $([int]) 
	-ListPoint '<tenant_id>' 
	-ListShardMap $ShardMap 
	-SqlServerName '<shard_server_name>' 
	-SqlDatabaseName '<shard_database_name>' 

### Opção 2: mapear os dados para um mapeamento de intervalo

Adicione os mapeamentos de intervalo para todo o intervalo de IDs de locatário – associações de banco de dados:

	# Create the mappings and associate it with the new shards 
	Add-RangeMapping 
	-KeyType $([int]) 
	-RangeHigh '5' 
	-RangeLow '1' 
	-RangeShardMap $ShardMap 
	-SqlServerName '<shard_server_name>' 
	-SqlDatabaseName '<shard_database_name>' 


### Etapa 4, opção 3: mapear os dados de vários locatários em um banco de dados individual

Para cada locatário, execute o Add-ListMapping (opção 1, acima).


## Verificando os mapeamentos

Informações sobre os fragmentos existentes e os mapeamentos associados a eles podem ser consultadas usando os seguintes comandos:

	# List the shards and mappings 
	Get-Shards -ShardMap $ShardMap 
	Get-Mappings -ShardMap $ShardMap 

## Resumo

Após ter concluído a configuração, você pode começar a usar a biblioteca de cliente do Banco de Dados Elástico. Pode também usar [roteamento dependente de dados](sql-database-elastic-scale-data-dependent-routing.md) e [consulta de vários fragmentos](sql-database-elastic-scale-multishard-querying.md).

## Próximas etapas


Obtenha os scripts do PowerShell de [Azure SQL DB - Scripts de ferramentas de Banco de Dados Elástico](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).

As ferramentas também estão no GitHub: [Azure/elastic-db-tools](https://github.com/Azure/elastic-db-tools).

Use a ferramenta de divisão e mesclagem para mover dados de/para um modelo multilocatário de/para um modelo de locatário único. Consulte [Ferramenta de divisão e mesclagem](sql-database-elastic-scale-get-started.md).

[AZURE.INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-convert-to-use-elastic-tools/listmapping.png
[2]: ./media/sql-database-elastic-convert-to-use-elastic-tools/rangemapping.png
[3]: ./media/sql-database-elastic-convert-to-use-elastic-tools/multipleonsingledb.png
 

<!---HONumber=AcomDC_0511_2016-->