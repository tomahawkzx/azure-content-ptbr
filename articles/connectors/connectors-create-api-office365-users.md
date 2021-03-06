<properties
    pageTitle="Adicionar o conector dos Usuários do Office 365 ao PowerApps Enterprise ou aos Aplicativos Lógicos | Microsoft Azure"
    description="Visão geral do conector dos Usuários do Office 365 com os parâmetros da API REST"
    services=""    
    documentationCenter=""     
    authors="msftman"    
    manager="erikre"    
    editor="" 
    tags="connectors" />

<tags
ms.service="multiple"
ms.devlang="na"
ms.topic="article"
ms.tgt_pltfrm="na"
ms.workload="integration"
ms.date="05/18/2016"
ms.author="deonhe"/>

# Introdução ao conector dos Usuários do Office 365

Conecte-se aos Usuários do Office 365 para obter perfis, pesquisar usuários e muito mais. O conector dos Usuários do Office 365 pode ser usado em:

- Aplicativos lógicos 
- PowerApps

> [AZURE.SELECTOR]
- [Aplicativos lógicos](../articles/connectors/connectors-create-api-office365-users.md)
- [PowerApps Enterprise](../articles/power-apps/powerapps-create-api-office365-users.md)

&nbsp;

>[AZURE.NOTE] Esta versão do artigo aplica-se à versão do esquema 2015-08-01-preview de aplicativos lógicos.


Com os Usuários do Office 365, você pode:

- Criar seu fluxo de negócios baseado nos dados obtidos dos Usuários do Office 365. 
- Usar ações que obtêm relatórios diretos, o perfil de usuário de um gerenciador e muito mais. Essas ações obtêm uma resposta e disponibilizam a saída para outras ações. Por exemplo, obtenha relatórios diretos de uma pessoa e, em seguida, utilize essas informações e atualize um banco de dados SQL Azure. 
- Adicione o conector dos Usuários do Office 365 ao PowerApps Enterprise. Assim, seus usuários poderão usar esse conector em seus próprios aplicativos. 

Para saber mais sobre como adicionar um conector ao PowerApps Enterprise, acesse [Registrar um conector no PowerApps](../power-apps/powerapps-register-from-available-apis.md).

Para adicionar uma operação aos Aplicativos Lógicos, confira [Criar um aplicativo lógico](../app-service-logic/app-service-logic-create-a-logic-app.md).

## Gatilhos e ações

O conector dos Usuários do Office 365 tem as ações a seguir disponíveis. Não há nenhum gatilho.

| Gatilhos | Ações|
| --- | --- |
|Nenhum | <ul><li>Obter gerenciador</li><li>Obter meu perfil</li><li>Obter relatórios diretos</li><li>Obter o perfil do usuário</li><li>Pesquisar usuários</li></ul>|

Todos os conectores dão suporte a dados nos formatos JSON e XML.


## Criar uma conexão com os Usuários do Office 365

Ao adicionar esse conector aos seus aplicativos lógicos, é necessário entrar em sua conta dos Usuários do Office 365 e permitir que os aplicativos lógicos se conectem à sua conta.

>[AZURE.INCLUDE [Etapas para criar uma conexão com os Usuários do Office 365](../../includes/connectors-create-api-office365users.md)]

Depois de criar a conexão, insira as propriedades dos Usuários do Office 365, como a ID de usuário. A **Referência da API REST** neste tópico descreve essas propriedades.

>[AZURE.TIP] É possível usar essa mesma conexão dos Usuários do Office 365 em outros aplicativos lógicos.


## Referência da API REST dos Usuários do Office 365
Aplica-se à versão: 1.0.

### Obter meu perfil 
Recupera o perfil para o usuário atual.```GET: /users/me```

Não há parâmetros para esta chamada.

#### Resposta

|Nome|Descrição|
|---|---|
|200|Operação bem-sucedida|
|202|Operação bem-sucedida|
|400|BadRequest|
|401|Não Autorizado|
|403|Proibido|
|500|Erro interno do servidor|
|padrão|Falha na Operação.|


### Obter o perfil do usuário 
Recupera um perfil do usuário específico.```GET: /users/{userId}```

| Nome| Tipo de Dados|Obrigatório|Localizado em|Valor Padrão|Descrição|
| ---|---|---|---|---|---|
|coluna|string|sim|path|nenhum|Nome UPN ou ID do email|

#### Resposta

|Nome|Descrição|
|---|---|
|200|Operação bem-sucedida|
|202|Operação bem-sucedida|
|400|BadRequest|
|401|Não Autorizado|
|403|Proibido|
|500|Erro interno do servidor|
|padrão|Falha na Operação.|


### Obter o gerenciador 
Recupera o perfil do usuário para o gerenciador do usuário especificado.```GET: /users/{userId}/manager```

| Nome| Tipo de Dados|Obrigatório|Localizado em|Valor Padrão|Descrição|
| ---|---|---|---|---|---|
|coluna|string|sim|path|nenhum|Nome UPN ou ID do email|

#### Resposta

|Nome|Descrição|
|---|---|
|200|Operação bem-sucedida|
|202|Operação bem-sucedida|
|400|BadRequest|
|401|Não Autorizado|
|403|Proibido|
|500|Erro interno do servidor|
|padrão|Falha na Operação.|



### Obter relatórios diretos 
Obter relatórios diretos. ```GET: /users/{userId}/directReports```

| Nome| Tipo de Dados|Obrigatório|Localizado em|Valor Padrão|Descrição|
| ---|---|---|---|---|---|
|coluna|string|sim|path|nenhum|Nome UPN ou ID do email|

#### Resposta

|Nome|Descrição|
|---|---|
|200|Operação bem-sucedida|
|202|Operação bem-sucedida|
|400|BadRequest|
|401|Não Autorizado|
|403|Proibido|
|500|Erro interno do servidor|
|padrão|Falha na Operação.|



### Pesquisar por usuários 
Recupera os resultados da pesquisa dos perfis do usuário.```GET: /users```

| Nome| Tipo de Dados|Obrigatório|Localizado em|Valor Padrão|Descrição|
| ---|---|---|---|---|---|
|searchTerm|string|não|query|nenhum|Pesquisar cadeia de caracteres (aplica-se a: nome de exibição, nome, sobrenome, email, apelido de email e nome UPN)|

#### Resposta

|Nome|Descrição|
|---|---|
|200|Operação bem-sucedida|
|202|Operação bem-sucedida|
|400|BadRequest|
|401|Não Autorizado|
|403|Proibido|
|500|Erro interno do servidor|
|padrão|Falha na Operação.|



## Definições de objeto

#### Usuário: classe de modelo de usuário

|Nome da Propriedade | Tipo de Dados |Obrigatório
|---|---|---|
|DisplayName|string|não|
|GivenName|string|não|
|Sobrenome|string|não|
|Email|string|não|
|MailNickname|string|não|
|TelephoneNumber|string|não|
|AccountEnabled|booleano|não|
|ID|string|sim
|UserPrincipalName|string|não|
|Departamento|string|não|
|JobTitle|string|não|
|mobilePhone|string|não|


## Próximas etapas

[Criar um aplicativo lógico](../app-service-logic/app-service-logic-create-a-logic-app.md).

Voltar para a [Lista de APIs](apis-list.md).

<!--References-->
[5]: https://portal.azure.com
[7]: ./media/connectors-create-api-office365-users/aad-tenant-applications.PNG
[8]: ./media/connectors-create-api-office365-users/aad-tenant-applications-add-appinfo.PNG
[9]: ./media/connectors-create-api-office365-users/aad-tenant-applications-add-app-properties.PNG
[10]: ./media/connectors-create-api-office365-users/contoso-aad-app.PNG
[11]: ./media/connectors-create-api-office365-users/contoso-aad-app-configure.PNG

<!---HONumber=AcomDC_0525_2016-->