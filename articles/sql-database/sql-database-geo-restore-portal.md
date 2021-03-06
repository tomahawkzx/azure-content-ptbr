<properties
	pageTitle="Restaurar um Banco de Dados SQL do Azure de um backup com redundância geográfica (Portal do Azure) | Microsoft Azure"
	description="Restaurar geograficamente um Banco de Dados SQL do Azure de um backup com redundância geográfica (Portal do Azure)."
	services="sql-database"
	documentationCenter=""
	authors="stevestein"
	manager="jhubbard"
	editor=""/>

<tags
	ms.service="sql-database"
	ms.devlang="NA"
	ms.date="05/10/2016"
	ms.author="sstein"
	ms.workload="data-management"
	ms.topic="article"
	ms.tgt_pltfrm="NA"/>


# Restaurar um Banco de Dados SQL do Azure de um backup com redundância geográfica usando o Portal do Azure


> [AZURE.SELECTOR]
- [Portal do Azure](sql-database-geo-restore-portal.md)
- [PowerShell](sql-database-geo-restore-powershell.md)

Este artigo mostra como restaurar seu banco de dados para um novo servidor usando a restauração geográfica com o Portal do Azure.

A [Restauração Geográfica](sql-database-geo-restore.md) possibilita restaurar um banco de dados por meio de um backup com redundância geográfica para criar um novo banco de dados. O banco de dados pode ser criado em qualquer servidor em qualquer região do Azure. Como usa um backup com redundância geográfica como sua fonte, ele pode ser usado para recuperar um banco de dados mesmo que este esteja inacessível devido a uma interrupção. A restauração geográfica está habilitada automaticamente para todas as camadas de serviço sem custo extra.

## Selecionar o banco de dados a ser restaurado

Para restaurar um banco de dados no Portal do Azure, faça o seguinte:

1.	Abra o [Portal do Azure](https://portal.azure.com).
2.  No lado esquerdo da tela, selecione **Novo** > **Dados e Armazenamento** > **Banco de Dados SQL**.
3.  Selecione **Backup** como a origem e selecione o backup redundante geograficamente do qual você deseja recuperar.

    ![Restaurar um Banco de Dados SQL do Azure](./media/sql-database-geo-restore-portal/geo-restore.png)

4.  Especifique um nome de banco de dados, um servidor para o qual você deseja restaurar o banco de dados e clique em Criar:

## Próximas etapas

- [Conectar-se ao Banco de Dados SQL com o SQL Server Management Studio e executar um exemplo de consulta T-SQL](sql-database-connect-query-ssms.md)
- [Executar análise de recuperação de desastres](sql-database-disaster-recovery-drills.md)


## Recursos adicionais

- [Restauração geográfica](sql-database-geo-restore.md)
- [Visão geral da continuidade dos negócios](sql-database-business-continuity.md)
- [Documentação do Banco de Dados SQL](https://azure.microsoft.com/documentation/services/sql-database/)

<!---HONumber=AcomDC_0511_2016-->