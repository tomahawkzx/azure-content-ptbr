<properties

	pageTitle="Managing groups in Azure Active Directory | Microsoft Azure"
	description="How to create and manage groups to manage Azure users using Azure Active Directory."
	services="active-directory"
	documentationCenter=""
	authors="curtand"
	manager="stevenpo"
	editor=""/>

<tags
	ms.service="active-directory"
	ms.workload="identity"
	ms.tgt_pltfrm="na"
	ms.devlang="na"
	ms.topic="get-started-article"
	ms.date="06/14/2016"
	ms.author="curtand"/>


# Gerenciamento de grupos no Azure Active Directory

Um dos recursos de gerenciamento de usuários do Azure AD (Azure Active Directory) é a capacidade de criar grupos de usuários. Você pode usar um grupo para executar tarefas de gerenciamento, como a atribuição de licenças ou permissões a vários usuários de uma vez. Você também pode usar grupos para atribuir a permissão de acesso a

- Recursos como objetos no diretório
- Recursos externos para o diretório, como aplicativos SaaS, serviços do Azure, sites do SharePoint ou recursos locais

Além disso, o proprietário do recurso também pode atribuir acesso a um recurso a um grupo do Azure AD pertencente a outra pessoa. Essa atribuição concede acesso ao recurso aos membros desse grupo. Em seguida, o proprietário do grupo gerencia a associação ao grupo. Efetivamente, o proprietário do recurso delega ao proprietário do grupo a permissão de atribuir usuários aos seus recursos.

## Como faço para criar um grupo?

Dependendo dos serviços que sua organização assinou, você pode criar um grupo usando um dos seguintes itens:
- o portal clássico do Azure
- o portal da conta do Office 365
- o portal da conta do Windows Intune

Descreveremos as tarefas da forma como são realizadas no portal clássico do Azure. Para saber mais sobre como usar portais que não são do Azure para gerenciar seu diretório do Azure AD, confira [Administrar seu diretório do Azure AD](active-directory-administer.md).

1. No [portal clássico do Azure](https://manage.windowsazure.com), selecione **Active Directory** e o nome do diretório de sua organização.

2. Selecione a guia **Grupos**.

3. Selecione **Adicionar Grupo**.

4. Na janela **Adicionar grupo**, especifique o nome e a descrição de um grupo.


## Como faço para adicionar ou remover usuários individuais em um grupo de segurança?

**Para adicionar um usuário individual a um grupo**

1. No [portal clássico do Azure](https://manage.windowsazure.com), selecione **Active Directory** e o nome do diretório de sua organização.

2. Selecione a guia **Grupos**.

3. Abra o grupo ao qual você deseja adicionar membros. Abra a guia **Membros** do grupo selecionado, se ela ainda não estiver sendo exibida.

4. Selecione **Adicionar Membros**.

5. Na página **Adicionar Membros**, selecione o nome do usuário ou um grupo que você deseja adicionar como membro do grupo. Verifique se esse nome é adicionado ao painel **Selecionados**.


**Para remover um usuário individual de um grupo**

1. No [portal clássico do Azure](https://manage.windowsazure.com), selecione **Active Directory** e o nome do diretório de sua organização.

2. Selecione a guia **Grupos**.

3. Abra o grupo do qual deseja remover membros.

4. Selecione a guia **Membros** e o nome do membro que você deseja remover do grupo e clique em **Remover**.

6. No prompt, confirme que você deseja remover esse membro do grupo.


## Como posso gerenciar a associação de um grupo dinamicamente?

No Azure AD, você pode configurar com facilidade uma regra simples para determinar quais usuários devem ser membros do grupo. Uma regra simples é aquele que faz uma única comparação. Por exemplo, se um grupo for atribuído a um aplicativo SaaS, você poderá configurar uma regra para adicionar usuários que têm o cargo de "Representante de Vendas". Essa regra concede então acesso ao aplicativo SaaS para todos os usuários com esse cargo no diretório.

> [AZURE.NOTE] Você pode configurar uma regra de associação dinâmica em grupos de segurança ou em grupos do Office 365. Atualmente não há suporte a associações de grupo aninhadas para atribuição com base em grupo para aplicativos.
>
> As associações dinâmicas de grupos exigem que uma licença do Azure AD Premium seja atribuída a
>
> - O administrador que gerencia a regra em um grupo
> - Todos os membros do grupo

**Para habilitar a associação dinâmica a um grupo**

1. No [portal clássico do Azure](https://manage.windowsazure.com), selecione **Active Directory** e o nome do diretório de sua organização.

2. Selecione a guia **Grupos** e abra o grupo que você deseja editar.

3. Selecione a guia **Configurar** e defina **Habilitar Associações Dinâmicas** como **Sim**.

4. Configure uma única regra simples para que o grupo controle o funcionamento da associação dinâmica para esse grupo. Verifique se a opção **Adicionar usuários em que** está marcada e selecione uma propriedade de usuário na lista (por exemplo, departamento, jobTitle, etc.)

5. Em seguida, selecione uma condição (Não É Igual a, Igual a, Não Começa com, Começa com, Não Contém, Contém, Não Corresponde, Corresponde).

6. Especifique um valor de comparação para a propriedade de usuário selecionada.

Para saber mais sobre como criar regras *avançadas* (regras que podem conter várias comparações) para a associação dinâmica de grupo, confira [Uso de atributos para criar regras avançadas](active-directory-accessmanagement-groups-with-advanced-rules.md).

## Informações adicionais

Esses artigos fornecem mais informações sobre o Active Directory do Azure.

* [Gerenciamento de acesso a recursos com grupos do Active Directory do Azure](active-directory-manage-groups.md)

* [Cmdlets do Azure Active Directory para definir configurações de grupo](active-directory-accessmanagement-groups-settings-cmdlets.md)

* [Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure](active-directory-apps-index.md)

* [O que é o Active Directory do Azure?](active-directory-whatis.md)

* [Integração de suas identidades locais com o Active Directory do Azure](active-directory-aadconnect.md)

<!---HONumber=AcomDC_0615_2016-->