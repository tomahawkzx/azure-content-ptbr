<properties 
   pageTitle="API REST de Alerta do Log Analytics"
   description="A API de REST do Log Analytics permite criar e gerenciar alertas no OMS (Operations Management Suite). Este artigo fornece detalhes da API e vários exemplos para executar operações diferentes."
   services="log-analytics"
   documentationCenter=""
   authors="bwren"
   manager="jwhit"
   editor="tysonn" />
<tags 
   ms.service="log-analytics"
   ms.devlang="na"
   ms.topic="article"
   ms.tgt_pltfrm="na"
   ms.workload="infrastructure-services"
   ms.date="05/03/2016"
   ms.author="bwren" />

# API REST de alerta do Log Analytics

A API de REST do Log Analytics permite criar e gerenciar alertas no OMS (Operations Management Suite). Este artigo fornece detalhes da API e vários exemplos para executar operações diferentes.

A API REST de Pesquisa do Log Analytics é RESTful e pode ser acessada por meio da API REST do Azure Resource Manager. Neste documento, você encontrará exemplos em que a API é acessada por meio de uma linha de comando do PowerShell usando o [ARMClient](https://github.com/projectkudu/ARMClient), uma ferramenta de linha de comando de software livre que simplifica a invocação da API do Azure Resource Manager. O uso do ARMClient e do PowerShell é uma das muitas opções para acessar a API de Pesquisa do Log Analytics. Com essas ferramentas, você pode utilizar a API RESTful do Azure Resource Manager para fazer chamadas aos espaços de trabalho do OMS e executar comandos de pesquisa dentro deles. A API produzirá resultados da pesquisa para você no formato JSON, permitindo que você use os resultados da pesquisa de diferentes maneiras por meio de programação.

## Pré-requisitos
Atualmente, os alertas somente podem ser criados com uma pesquisa salva no Log Analytics. Você pode consultar a [API REST da Pesquisa de Log](log-analytics-log-search-api.md) para obter mais informações.

## Agendas
Uma pesquisa salva pode ter um ou mais agendamentos. O agendamento define a frequência com que a pesquisa é executada e o intervalo de tempo em que os critérios são identificados. Os agendamentos têm as propriedades indicadas na tabela a seguir.

| Propriedade | Descrição |
|:--|:--|
| Intervalo | A frequência com que a pesquisa é executada. Medida em minutos. |
| QueryTimeSpan | O intervalo durante o qual os critérios são avaliados. Deve ser igual ou maior que Interval. Medida em minutos. |
| Versão | A versão da API que está sendo usada. Atualmente, isso sempre deve ser definido como 1. |

Por exemplo, considere uma consulta de evento com um Interval (Intervalo) de 15 minutos e Timespan (Período) de 30 minutos. Nesse caso, a consulta deverá ser executada a cada 15 minutos e um alerta deverá ser disparado se os critérios continuarem a ser resolvidos como verdadeiro por um período de 30 minutos.

### Recuperando agendamentos
Use o método Get para recuperar todos os agendamentos de uma pesquisa salva.

	armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/{Search  ID}/schedules?api-version=2015-03-20

Use o método Get para recuperar um agendamento específico para uma pesquisa salva.

	armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20

A seguir está um exemplo de resposta para um agendamento.

	{
		"id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/MyWorkspace/savedSearches/0f0f4853-17f8-4ed1-9a03-8e888b0d16ec/schedules/a17b53ef-bd70-4ca4-9ead-83b00f2024a8",
		"etag": "W/"datetime'2016-02-25T20%3A54%3A49.8074679Z'"",
		"properties": {
		"Interval": 15,
		"QueryTimeSpan": 15
	}

### Criar ou editar um agendamento
Use o método Put com uma ID de agendamento que seja exclusiva para a pesquisa salva para criar uma nova agenda. Se você usar uma ID de agendamento existente, ele será modificado. Ao criar um agendamento no console do OMS, uma GUID é criado para a ID de agendamento.

	$scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' }"
	armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson

### Excluindo agendamentos
Use o método Delete com uma ID de agendamento para excluir um agendamento.

	armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20


## Ações
Um agendamento pode ter várias ações. Uma ação pode definir um ou mais processos a serem executados, como enviar um email ou iniciar um runbook, ou então ela pode definir um limite que determina quando os resultados de uma pesquisa correspondem a certos critérios. Algumas ações definirão ambos para que os processos sejam executados quando o limite for atingido.
 
Todas as ações têm as propriedades indicadas na tabela a seguir. Diferentes tipos de alertas têm diferentes propriedades adicionais que são descritas abaixo.

| Propriedade | Descrição |
|:--|:--|
| Tipo | Tipo da ação. Atualmente, os valores possíveis são Alerta e Webhook. |
| Nome | Nome de exibição para o alerta. |
| Versão | A versão da API que está sendo usada. Atualmente, isso sempre deve ser definido como 1. |

### Recuperando ações
Use o método Get para recuperar todas as ações de um agendamento.

	armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/{Search  ID}/schedules/{Schedule ID}/actions?api-version=2015-03-20

Use o método Get com a ID de ação para recuperar uma ação específica de um agendamento.

	armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/actions/{Action ID}?api-version=2015-03-20

### Criar ou editar ações
Use o método Put com uma ID de atividade que seja exclusiva para o agendamento para criar uma nova atividade. Se você usar uma ID de atividade existente, ela será modificada. Quando você cria uma atividade no console do OMS, um GUID é fornecido para a ID de atividade.

O formato da solicitação para criar uma nova atividade varia conforme o tipo de atividade, veja os exemplos fornecidos nas seções a seguir.

### Excluindo ações
Use o método Delete com a ID de ação para excluir uma ação.
	
	armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/Actions/{Action ID}?api-version=2015-03-20

### Ações de Alerta
Um Agendamento deve ter somente uma ação de Alerta. Ações de alerta têm uma ou mais das seções na tabela a seguir. Elas são descritas em mais detalhes abaixo.

| Seção | Descrição |
|:--|:--|
| Limite | Critérios para quando a ação for executada. |  
| EmailNotification | Envie email para vários destinatários. |
| Correção | Inicie um runbook na Automação do Azure para tentar corrigir o problema identificado. |

#### Limites
Uma ação de Alerta deve ter somente um limite. Quando os resultados de pesquisas salvas coincidem com o limite de uma ação associada à pesquisa, outros processos nesta ação são executados. Uma ação também pode conter apenas um limite para ser usado com ações de outros tipos que não contêm os limites.

Os limites têm as propriedades indicadas na tabela a seguir.

| Propriedade | Descrição |
|:--|:--|
| Operador | Operador de comparação de limite. <br> gt = Maior Que <br> lt = Menor Que |
| Valor | Valor para o limite. |

Por exemplo, considere uma consulta de evento com um Interval (Intervalo) de 15 minutos, Timespan (Período) de 30 minutos e Threshold (Limite) maior que 10. Nesse caso, a consulta deverá ser executada a cada 15 minutos e um alerta deverá ser disparado se ela retornar 10 eventos criados dentro de um período de 30 minutos.

Veja a seguir um exemplo de resposta para uma ação com apenas um limite.

	"etag": "W/"datetime'2016-02-25T20%3A54%3A20.1302566Z'"",
	"properties": {
		"Type": "Alert",
		"Name": "My threshold action",
		"Threshold": {
			"Operator": "gt",
			"Value": 10
		},
    	"Version": 1
	}

Use o método Put com a ID de ação para criar uma nova ação de limite para um agendamento. Se você usar uma nova ID para a ação, uma nova ação será criada. Se você usar uma ID já existente para o agendamento, essa ação será modificada.

	$thresholdJson = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
	armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

#### Notificação por email
Notificações por Email enviam email para um ou mais destinatários. Elas incluem as propriedades indicadas na tabela a seguir.

| Propriedade | Descrição |
|:--|:--|
| Destinatários | Lista de endereços de email. |
| Assunto | O assunto do email. |
| Anexo | Atualmente, não há suporte para nexos, por isso este item sempre terá um valor de "None" (Nenhum). |

Veja a seguir uma resposta de exemplo para uma ação de notificação por email com um limite.

	"etag": "W/"datetime'2016-02-25T20%3A54%3A20.1302566Z'"",
	"properties": {
		"Type": "Alert",
		"Name": "My email action",
		"Threshold": {
			"Operator": "gt",
			"Value": 10
		},
		"EmailNotification": {
			"Recipients": [
    			"recipient1@contoso.com",
		    	"recipient2@contoso.com"
			],
			"Subject": "This is the subject",
			"Attachment": "None"
		},
    	"Version": 1
	}

Use o método Put com a ID de ação para criar uma nova ação de email para um agendamento. Se você usar uma nova ID para a ação, uma nova ação será criada. Se você usar uma ID já existente para o agendamento, essa ação será modificada.

O exemplo a seguir cria uma notificação por email com um limite para que o email seja enviado quando os resultados da pesquisa salvos excederem o limite.

	$emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is the subject', 'Attachment':'None'} }"
	armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $ emailJson

#### Ações de correção
As correções iniciam um runbook na Automação do Azure que tenta corrigir o problema identificado pelo alerta. Você deve criar um webhook para o runbook usado em uma ação de correção e especificar o URI na propriedade WebhookUri. Quando você cria essa ação usando o console do OMS, um novo webhook é criado automaticamente para o runbook.

As correções incluem as propriedades indicadas na tabela a seguir.

| Propriedade | Descrição |
|:--|:--|
| RunbookName | Nome do runbook. Isso deve corresponder a um runbook publicado na conta de automação configurada na Solução de Automação no seu espaço de trabalho do OMS. |
| WebhookUri | O URI do webhook.
| Expiry | A data e hora de expiração do webhook. Caso o webhook não expire, esta pode ser qualquer data futura válida. |

Veja a seguir uma resposta de exemplo para uma ação de correção com um limite.

	"etag": "W/"datetime'2016-02-25T20%3A54%3A20.1302566Z'"",
	"properties": {
		"Type": "Alert",
		"Name": "My remediation action",
		"Threshold": {
			"Operator": "gt",
			"Value": 10
		},
		"Remediation": {
			"RunbookName": "My-Runbook",
			"WebhookUri": "https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d",
			"Expiry": "2018-02-25T18:27:20"
			},
		"Version": 1
	}

Use o método Put com a ID de ação para criar uma nova ação de correção para um agendamento. Se você usar uma nova ID para a ação, uma nova ação será criada. Se você usar uma ID já existente para o agendamento, essa ação será modificada.

O exemplo a seguir cria uma correção com um limite para que o runbook seja iniciado quando os resultados da pesquisa salvos excederem o limite.

	$remediateJson = "{'properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
	armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

#### Exemplo
Veja a seguir um exemplo completo para criar um novo alerta de email. Ele cria um novo agendamento juntamente com uma ação que contém um limite e um email.

	$subscriptionId = "3d56705e-5b26-5bcc-9368-dbc8d2fafbfc"
	$workspaceId    = "MyWorkspace"
	$searchId       = "51cf0bd9-5c74-6bcb-927e-d1e9080b934e"

	$scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' }"
	armclient put /subscriptions/$subscriptionId/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/$workspaceId/savedSearches/$searchId/schedules/myschedule?api-version=2015-03-20 $scheduleJson

	$thresholdJson = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
	armclient put /subscriptions/$subscriptionId/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/$workspaceId/savedSearches/$searchId/schedules/myschedule/actions/mythreshold?api-version=2015-03-20 $thresholdJson

	$emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is the subject', 'Attachment':'None'} }"
	armclient put /subscriptions/$subscriptionId/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/$workspaceId/savedSearches/$searchId/schedules/myschedule/actions/myemailaction?api-version=2015-03-20 $emailJson

### Ações de Webhook
Ações de Webhook iniciam um processo chamando uma URL e, opcionalmente, fornecendo uma carga a ser enviada. Elas são semelhantes às ações de Correção, exceto que se destinam a webhooks que podem invocar outros processos além de runbooks da Automação do Azure. Eles também oferecem a opção adicional de fornecer uma carga a ser enviada para o processo remoto.

Ações de Webhook não têm um limite, devendo ser adicionadas a um agendamento que tem uma ação de Alerta com um limite. Você pode adicionar várias ações de Webhook que serão executadas quando o limite for atingido.

Ações de webhook incluem as propriedades indicadas na tabela a seguir.

| Propriedade | Descrição |
|:--|:--|
| WebhookUri | O assunto do email. |
| CustomPayload | Carga personalizada a ser enviada para o webhook. O formato dependerá do que o webhook está esperando. |

Veja a seguir um exemplo de resposta para a ação de webhook e uma ação de alerta associada com um limite.

	{
		"__metadata": {},
		"value": [
			{
				"id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/72884702-acf9-4653-bb67-f42436b342b4",
				"etag": "W/"datetime'2016-02-26T20%3A25%3A00.6862124Z'"",
				"properties": {
					"Type": "Webhook",
					"Name": "My Webhook Action",
					"WebhookUri": "https://oaaswebhookdf.cloudapp.net/webhooks?token=VfkYTIlpk%2fc%2bJBP",
					"CustomPayload": "{"fielld1":"value1","field2":"value2"}",
					"Version": 1
				}
			},
			{
				"id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/90a27cf8-71b7-4df2-b04f-54ed01f1e4b6",
				"etag": "W/"datetime'2016-02-26T20%3A25%3A00.565204Z'"",
				"properties": {
					"Type": "Alert",
					"Name": "Threshold for my webhook action",
					"Threshold": {
						"Operator": "gt",
						"Value": 10
					},
					"Version": 1
				}
			}
		]
	}

#### Criar ou editar uma ação de webhook
Use o método Put com a ID de ação para criar uma nova ação de webhook para um agendamento. Se você usar uma nova ID para a ação, uma nova ação será criada. Se você usar uma ID já existente para o agendamento, essa ação será modificada. O exemplo a seguir cria uma ação de Webhook e uma ação de alerta com um limite para que o webhook seja acionado quando os resultados da pesquisa salvos excederem o limite.

	$thresholdAction = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
	armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdAction
	
	$webhookAction = "{'properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{"field1":"value1","field2":"value2"}', 'Version': 1 }"
	armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction


## Próximas etapas

- Use a [API REST para executar pesquisas de log](log-analytics-log-search-api.md) no Log Analytics.
 

<!---HONumber=AcomDC_0518_2016-->