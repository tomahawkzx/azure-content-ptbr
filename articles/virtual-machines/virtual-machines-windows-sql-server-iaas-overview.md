<properties
	pageTitle="Introdução ao SQL Server em Máquinas Virtuais do Microsoft Azure | Microsoft Azure"
	description="Mova suas cargas de trabalho de banco de dados do SQL Server local para a nuvem com as máquinas virtuais do Azure. Introdução rápida às imagens pré-configuradas da VM do SQL."
	services="virtual-machines-windows"
	documentationCenter=""
	authors="rothja"
	manager="jhubbard"
	editor=""
	tags="azure-service-management"/>

<tags
	ms.service="virtual-machines-windows"
	ms.devlang="na"
	ms.topic="get-started-article"
	ms.tgt_pltfrm="vm-windows-sql-server"
	ms.workload="infrastructure-services"
	ms.date="06/13/2016"
	ms.author="jroth"/>

# Introdução ao SQL Server nas Máquinas Virtuais do Azure

Este tópico descreve suas opções para executar o SQL Server em máquinas virtuais do Azure e fornece diretrizes e recursos para ajudar você a começar.

Talvez você seja um administrador de banco de dados querendo mover suas cargas de trabalho do SQL Server local para a nuvem. Ou pode ser um desenvolvedor considerando os recursos de banco de dados relacional do SQL Server para seu aplicativo do Azure. Qual é a vantagem de executar cargas de trabalho do SQL Server em máquinas virtuais do Azure? O seguinte vídeo de visão geral aborda os benefícios e fornece uma visão geral técnica.

> [AZURE.VIDEO data-driven-sql-server-2016-azure-vm-is-the-best-platform-for-sql-server-2016]

## Avaliar os benefícios

Antes de começar, primeiro avalie o que você obtém ao usar o SQL Server em VMs do Azure.

Se você estiver movendo outras cargas de trabalho no Azure, como um aplicativo empresarial, faz sentido também mover qualquer banco de dados dependente do SQL Server no Azure para melhorar o desempenho. Mas hospedar o SQL Server em VMs do Azure fornece outros benefícios. Por exemplo, você tem acesso automaticamente em vários data centers para uma recuperação de desastres e presença global. Para obter uma lista completa de cenários e benefícios, confira o [SQL Server na página do produto das VMs do Azure](https://azure.microsoft.com/services/virtual-machines/sql-server/).

> [AZURE.NOTE] Quando você estiver avaliando o SQL Server em VMs do Azure, analise o outro armazenamento e as opções de SQL no Azure, como [Banco de dados SQL](../sql-database/sql-database-technical-overview.md), [SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md), e [SQL Server Stretch Database](../sql -server-stretch-database/sql-server-stretch-database-overview.md). Para obter uma comparação detalhada, confira [Escolher uma opção do SQL Server de nuvem: Banco de Dados do Azure SQL (PaaS) ou SQL Server em VMs do Azure (IaaS)](../sql-database/data-management-azure-sql-database-and-sql-server-iaas.md).

Depois que você optar por executar o SQL Server em VMs do Azure, uma das primeiras decisões é se deseja usar uma imagem de VM que inclui os custos de licenciamento do SQL Server. A outra opção é trazer sua própria licença (BYOL) e pagar somente pela VM em si. As duas próximas seções descrevem essas opções.

## Opção 1: implantar uma VM do SQL (licenciamento por minuto)
A tabela a seguir fornece uma matriz de imagens do SQL Server disponíveis na galeria de máquinas virtuais. Clique em qualquer link para começar a criar uma nova VM do SQL com a versão especificada, a edição e o sistema operacional. Todas as imagens incluem os [Custos de licenciamento do SQL Server](https://azure.microsoft.com/pricing/details/virtual-machines/#Sql).

Diretrizes passo a passo estão disponíveis no tutorial, [Provisionar uma máquina virtual do SQL Server no Portal do Azure](virtual-machines-windows-portal-sql-server-provision.md). Além disso, revise as [Práticas recomendadas para VMs do SQL Server](virtual-machines-windows-sql-performance.md), que explicam como selecionar o tamanho da máquina apropriado e outros recursos disponíveis durante o provisionamento.

|Versão|Sistema operacional|Edição|
|---|---|---|
|**SQL 2016**|Windows Server 2012 R2|[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2016RTMEnterpriseWindowsServer2012R2), [Standard](https://portal.azure.com/#create/Microsoft.SQLServer2016RTMStandardWindowsServer2012R2), [Web](https://portal.azure.com/#create/Microsoft.SQLServer2016RTMWebWindowsServer2012R2), [Dev](https://portal.azure.com/#create/Microsoft.SQLServer2016RTMDeveloperWindowsServer2012R2), [Express](https://portal.azure.com/#create/Microsoft.SQLServer2016RTMExpressWindowsServer2012R2)|
|**SQL 2014 SP1**|Windows Server 2012 R2|[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2014SP1EnterpriseWindowsServer2012R2), [Standard](https://portal.azure.com/#create/Microsoft.SQLServer2014SP1StandardWindowsServer2012R2), [Web](https://portal.azure.com/#create/Microsoft.SQLServer2014SP1WebWindowsServer2012R2), [Express](https://portal.azure.com/#create/Microsoft.SQLServer2014SP1ExpressWindowsServer2012R2)|
|**SQL 2014**|Windows Server 2012 R2|[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2014EnterpriseWindowsServer2012R2), [Standard](https://portal.azure.com/#create/Microsoft.SQLServer2014StandardWindowsServer2012R2), [Web](https://portal.azure.com/#create/Microsoft.SQLServer2014WebWindowsServer2012R2)|
|**SQL 2012 SP3**|Windows Server 2012 R2|[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3EnterpriseWindowsServer2012R2), [Standard](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3StandardWindowsServer2012R2), [Web](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3WebWindowsServer2012R2), [Express](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3ExpressWindowsServer2012R2)|
|**SQL 2012 SP2**|Windows Server 2012 R2|[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2012SP2EnterpriseWindowsServer2012R2), [Standard](https://portal.azure.com/#create/Microsoft.SQLServer2012SP2StandardWindowsServer2012R2), [Web](https://portal.azure.com/#create/Microsoft.SQLServer2012SP2WebWindowsServer2012R2)|
|**SQL 2012 SP2**|Windows Server 2012|[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2012SP2EnterpriseWindowsServer2012), [Standard](https://portal.azure.com/#create/Microsoft.SQLServer2012SP2StandardWindowsServer2012), [Web](https://portal.azure.com/#create/Microsoft.SQLServer2012SP2WebWindowsServer2012), [Express](https://portal.azure.com/#create/Microsoft.SQLServer2012SP2ExpressWindowsServer2012)|
|**SQL 2008 R2 SP3**|Windows Server 2008 R2|[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2008R2SP3EnterpriseWindowsServer2008R2), [Standard](https://portal.azure.com/#create/Microsoft.SQLServer2008R2SP3StandardWindowsServer2008R2), [Web](https://portal.azure.com/#create/Microsoft.SQLServer2008R2SP3WebWindowsServer2008R2)|
|**SQL 2008 R2 SP3**|Windows Server 2012|[Express](https://portal.azure.com/#create/Microsoft.SQLServer2008R2SP3ExpressWindowsServer2012)|

## Opção 2: implantar uma VM do SQL (BYOL)
Outra opção é trazer sua própria licença (BYOL). Nesse cenário, você paga apenas pela VM sem encargos adicionais para o licenciamento do SQL Server. Para usar sua própria licença, use a matriz de versões do SQL Server, edições e sistemas operacionais abaixo. No portal, os nomes de imagem são prefixados com **{BYOL}** no Portal.

> [AZURE.IMPORTANT] Para usar imagens da VM BYOL, você deve ter o Contrato Enterprise com [License Mobility por meio do Software Assurance no Azure](https://azure.microsoft.com/pricing/license-mobility/). Também é necessário uma licença válida para a versão/edição do SQL Server que você deseja usar. Você deve [fornecer as informações necessárias de BYOL à Microsoft](http://d36cz9buwru1tt.cloudfront.net/License_Mobility_Customer_Verification_Guide.pdf) em **10** dias de provisionamento da VM.

As diretrizes no [tutorial de provisionamento](virtual-machines-windows-portal-sql-server-provision.md) se aplica, mas você deve usar uma das seguintes opções de imagem de **BYOL**. Além disso, revise as [Práticas recomendadas para VMs do SQL Server](virtual-machines-windows-sql-performance.md), que explicam como selecionar o tamanho da máquina apropriado e outros recursos disponíveis durante o provisionamento.

|Versão|Sistema operacional|Edição|
|---|---|---|
|**SQL Server 2016**|Windows Server 2012 R2|[Enterprise BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2016RTMStandardWindowsServer2012R2), [Standard BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2016RTMStandardWindowsServer2012R2)|
|**SQL Server 2014 SP1**|Windows Server 2012 R2|[Enterprise BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2014SP1EnterpriseWindowsServer2012R2), [Standard BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2014SP1StandardWindowsServer2012R2)|
|**SQL Server 2012 SP2**|Windows Server 2012 R2|[Enterprise BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2012SP3EnterpriseWindowsServer2012R2), [Standard BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2012SP3StandardWindowsServer2012R2)|

## Gerenciar sua VM do SQL
Depois de provisionar sua VM do SQL Server, há várias tarefas de gerenciamento opcional. Em alguns aspectos, você configura e gerencia o SQL Server exatamente como faria no local. Mas algumas tarefas são específicas do Azure. As seções a seguir destacam algumas dessas áreas com links para obter mais informações.

### Migrar seus dados

Se você tiver um banco de dados existente, deverá movê-lo para a VM do SQL recentemente provisionada. Para obter uma lista das opções de migração e diretrizes, confira [Migrar um banco de dados para SQL Server em uma VM do Azure](virtual-machines-windows-migrate-sql.md).

### Configurar alta disponibilidade

Se você precisar de alta disponibilidade, considere configurar grupos de disponibilidade do SQL Server. Isso envolve várias VMs do Azure em uma rede virtual. O portal do Azure tem um modelo que define essa configuração para você. Para obter mais informações, confira [Configurar um grupo de disponibilidade AlwaysOn nas máquinas virtuais do Azure Resource Manager](virtual-machines-windows-portal-sql-alwayson-availability-groups.md). Se você deseja configurar manualmente o Grupo de Disponibilidade e o ouvinte associado, confira [Configurar os Grupos de Disponibilidade AlwaysOn na VM do Azure](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).

Para outras considerações sobre alta disponibilidade, consulte [alta disponibilidade e recuperação de desastres para SQL Server em Máquinas Virtuais do Azure](virtual-machines-windows-sql-high-availability-dr.md).

### Fazer backup de seus dados
As VMs do Azure podem tirar proveito do [Backup Automatizado](virtual-machines-windows-sql-automated-backup.md), que cria regularmente backups do banco de dados no armazenamento de blob. Essa técnica também pode ser usada manualmente. Para obter mais informações, confira Usar o [Armazenamento do Azure para Backup e Restauração do SQL Server](../sql-database/storage-use-storage-sql-server-backup-restore.md). Para obter uma visão geral das opções de backup e restauração, veja [Backup e Restauração do SQL Server em Máquinas Virtuais do Azure](virtual-machines-windows-sql-backup-recovery.md).

### Automatizar as atualizações
As VMs do Azure podem usar a [Aplicação de Patch Automatizada](virtual-machines-windows-sql-automated-patching.md) a fim de agendar uma janela de manutenção para a instalação automática de atualizações importantes do Windows e do SQL Server.

### Programa de aperfeiçoamento da experiência do usuário (CEIP)
O CEIP (Programa de Aperfeiçoamento da Experiência do Usuário) está habilitado por padrão. Isso não é uma tarefa de gerenciamento, a menos que você queira desativar o CEIP após o provisionamento. Você pode personalizar ou desabilitar o CEIP conectando-se à VM com área de trabalho remota. Em seguida, execute o utilitário **Erro do SQL Server e o Relatório de uso**. Siga as instruções para desabilitar o relatório.

## Próximas etapas
[Explorar o Roteiro de Aprendizagem ](https://azure.microsoft.com/documentation/learning-paths/sql-azure-vm/) do SQL Server em máquinas virtuais do Azure.

Mais perguntas? Primeiramente, confira as [Perguntas frequentes sobre o SQL Server em Máquinas Virtuais do Azure](virtual-machines-windows-sql-server-iaas-faq.md). Adicione também suas perguntas ou comentários à parte inferior de qualquer um dos tópicos sobre VM do SQL para interagir com a Microsoft e com a comunidade.

<!---HONumber=AcomDC_0615_2016-->