<properties
	pageTitle="Tutorial: Integração do Azure Active Directory ao Origami | Microsoft Azure"
	description="Saiba como configurar o logon único entre o Azure Active Directory e o Origami."
	services="active-directory"
	documentationCenter=""
	authors="jeevansd"
	manager="stevenpo"
	editor=""/>

<tags
	ms.service="active-directory"
	ms.workload="identity"
	ms.tgt_pltfrm="na"
	ms.devlang="na"
	ms.topic="article"
	ms.date="04/27/2016"
	ms.author="jeedes"/>


# Tutorial: Integração do Azure Active Directory ao Origami

Neste tutorial, você aprenderá a integrar o Origami ao Azure AD (Azure Active Directory).

A integração do Origami ao Azure AD oferece os seguintes benefícios:

- No Azure AD, é possível controlar quem tem acesso ao Origami
- É possível permitir que os usuários façam logon automaticamente no Origami (Logon Único) com suas contas do Azure AD
- Você pode gerenciar suas contas em um único local: o Portal clássico do Azure

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md).

## Pré-requisitos

Para configurar a integração do Azure AD ao Origami, você precisará dos seguintes itens:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Origami


> [AZURE.NOTE] Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.


Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).


## Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.

O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adicionando o Origami por meio da galeria
2. Configurar e testar o logon único do AD do Azure


## Adicionando o Origami por meio da galeria
Para configurar a integração do Origami ao Azure AD, você precisará adicionar o Origami por meio da galeria à sua lista de aplicativos SaaS gerenciados.

**Para adicionar o Origami por meio da galeria, realize as seguintes etapas:**

1. No **portal clássico do Azure**, no painel de navegação à esquerda, clique em **Active Directory**.

	![Active Directory][1]
2. Na lista **Diretório**, selecione o diretório para o qual você deseja habilitar a integração de diretórios.

3. Para abrir a visualização dos aplicativos, na exibição do diretório, clique em **Aplicativos** no menu principal.

	![Aplicativos][2]

4. Clique em **Adicionar** na parte inferior da página.

	![Aplicativos][3]

5. Na caixa de diálogo **O que você deseja fazer**, clique em **Adicionar um aplicativo da galeria**.

	![Aplicativos][4]

6. Na caixa de pesquisa, digite **Origami**.

	![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-origami-tutorial/tutorial_origami_01.png)
7. No painel de resultados, selecione **Origami** e clique em **Concluir** para adicionar o aplicativo.

	![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-origami-tutorial/tutorial_origami_02.png)

##  Configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o Origami, com base em um usuário de teste chamado “Brenda Fernandes”.

Para que o logon único funcione, o Azure AD precisa saber qual usuário do Origami é equivalente a um usuário do Azure AD. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Origami.

Essa relação de vínculo é estabelecida atribuindo o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** no Origami.

Para configurar e testar o logon único do Azure AD com o Origami, você precisará concluir os seguintes blocos de construção:

1. **[Configurar o Logon único do AD do Azure](#configuring-azure-ad-single-sign-on)**: para habilitar seus usuários a usar esse recurso.
2. **[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**: para testar o logon único do AD do Azure com Brenda Fernandes.
3. **[Criando um usuário de teste do Origami](#creating-a-origami-test-user)** - para ter um equivalente de Brenda Fernandes no Origami que esteja vinculado à representação dela no Azure AD.
4. **[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)**: para permitir que Brenda Fernandes use o logon único do AD do Azure.
5. **[Teste do logon único](#testing-single-sign-on)**: para verificar se a configuração funciona.

### Configuração do logon único do AD do Azure

Nesta seção, você habilitará o logon único do Azure AD no portal clássico e configurará o logon único em seu aplicativo do Origami.


**Para configurar o logon único do Azure AD com o Origami, realize as seguintes etapas:**

1. No portal clássico, na página de integração de aplicativos do **Origami**, clique em **Configurar logon único** para abrir o diálogo **Configurar Logon Único**.
	 
	![Configurar o logon único][6]

2. Na página **Como você deseja que os usuários façam logon no Origami**, selecione **Logon único do Azure AD** e clique em **Avançar**.

	![Configurar o logon único](./media/active-directory-saas-origami-tutorial/tutorial_origami_03.png)

3. Na página de diálogo **Definir Configurações de Aplicativo**, execute as seguintes etapas:

	![Configurar o logon único](./media/active-directory-saas-origami-tutorial/tutorial_origami_04.png)

    a. Na caixa de texto **URL de Entrada**, digite a URL usada pelos usuários para entrar em seu aplicativo do Origami usando o seguinte padrão: **https://live.origamirisk.com/origami/account/login?account=\<nome da empresa>**
	
	b. Clique em **Avançar**
 
4. Na página **Configurar logon único no Origami**, realize as seguintes etapas:

	![Configurar o logon único](./media/active-directory-saas-origami-tutorial/tutorial_origami_05.png)

    a. Clique em **Baixar certificado** e salve o arquivo em seu computador.

    b. Clique em **Próximo**.



1. Faça logon na conta do Origami com direitos de Administrador.

1. No menu na parte superior, clique em **Administrador**.

	![Configurar o logon único](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)
  

1. Na página do diálogo Configuração de Logon Único, realize as seguintes etapas:

	![Configurar o logon único](./media/active-directory-saas-origami-tutorial/123.png)

	a. Selecione **Habilitar Logon Único**.

	b. No portal clássico do Azure, copie a **URL de SSO de SAML** e cole-a na caixa de texto **URL da Página de Entrada do Provedor de Identidade**.

	c. No portal clássico do Azure, copie a **URL DO SERVIÇO DE LOGON ÚNICO** e cole-a na caixa de texto **URL de Página de Saída do Provedor de Identidade**.

	d. Clique em **Procurar** para carregar o certificado baixado no portal clássico do Azure.

	e. Clique em **Salvar Alterações**.


6. No portal clássico, selecione a confirmação da configuração de logon único e clique em **Avançar**.
	
	![Logon único do AD do Azure][10]

7. Na página **Confirmação de logon único**, clique em **Concluir**.
 
	![Logon único do AD do Azure][11]


### Criação de um usuário de teste do AD do Azure
Nesta seção, você criará uma usuária de teste no portal clássico chamada Brenda Fernandes.


![Criar um usuário do AD do Azure][20]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No **portal clássico do Azure**, no painel de navegação à esquerda, clique em **Active Directory**.

	![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-origami-tutorial/create_aaduser_09.png)

2. Na lista **Diretório**, selecione o diretório para o qual você deseja habilitar a integração de diretórios.

3. Para exibir a lista de usuários, no menu na parte superior, clique em **Usuários**.

	![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-origami-tutorial/create_aaduser_03.png)

4. Para abrir o diálogo **Adicionar Usuário**, na barra de ferramentas na parte inferior, clique em **Adicionar Usuário**.

	![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-origami-tutorial/create_aaduser_04.png)

5. Na página do diálogo **Conte-nos sobre este usuário**, realize as seguintes etapas: ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-origami-tutorial/create_aaduser_05.png)

    a. Em Tipo de Usuário, selecione Novo usuário na organização.

    b. Na **caixa de texto** Nome do Usuário, digite **BrendaFernandes**.

    c. Clique em **Próximo**.

6.  Na página do diálogo **Perfil do Usuário**, realize as seguintes etapas: ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-origami-tutorial/create_aaduser_06.png)

    a. Na caixa de texto **Nome**, digite **Brenda**.

    b. Na caixa de texto **Sobrenome**, digite **Fernandes**.

    c. Na caixa de texto **Nome de exibição**, digite **Brenda Fernandes**.

    d. Na lista **Função**, selecione **Usuário**.

    e. Clique em **Próximo**.

7. Na página de caixa de diálogo **Obter senha temporária**, clique em **criar**.

	![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-origami-tutorial/create_aaduser_07.png)

8. Na página de caixa de diálogo **Obter senha temporária**, execute as seguintes etapas:

	![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-origami-tutorial/create_aaduser_08.png)

    a. Anote o valor da **Nova Senha**.

    b. Clique em **Concluído**.



### Criando um usuário de teste do Origami

Nesta seção, você criará um usuário chamado Brenda Fernandes no Origami.

1. Faça logon na conta do Origami com direitos de Administrador.

2. No menu na parte superior, clique em **Administrador**.

	![Configurar o logon único](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

3. No diálogo **Usuários e Segurança**, clique em **Usuários**.
	
	![Configurar o logon único](./media/active-directory-saas-origami-tutorial/tutorial_origami_54.png)

4. Clique em **Adicionar Novo Usuário**.

	![Configurar o logon único](./media/active-directory-saas-origami-tutorial/tutorial_origami_55.png)

5. Na caixa de diálogo Adicionar Novo Usuário, execute as seguintes etapas:

	![Configurar o logon único](./media/active-directory-saas-origami-tutorial/tutorial_origami_56.png)

	a. Na caixa de texto **Nome de Usuário**, digite o Nome de Usuário Brenda Fernandes no portal clássico do Azure.

	b. Na caixa de texto **Senha**, digite uma senha.

	c. Na caixa de texto **Confirmar Senha**, digite a senha novamente.

	d. Na caixa de texto **Nome**, digite **Brenda**.

    e. Na caixa de texto **Sobrenome**, digite **Fernandes**.

	f. Clique em **Salvar**.

	![Configurar o logon único](./media/active-directory-saas-origami-tutorial/tutorial_origami_57.png)

1. Atribua **Funções de Usuário** e **Acesso para Cliente** ao usuário.

	![Configurar o logon único](./media/active-directory-saas-origami-tutorial/tutorial_origami_58.png)

### Atribuição do usuário de teste do AD do Azure

Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure, concedendo a ela acesso ao Origami.

![Atribuir usuário][200]

**Para atribuir Brenda Fernandes ao Origami, realize as seguintes etapas:**

1. No portal clássico, para abrir o modo de exibição de aplicativos, no modo de exibição de diretório, clique em **Aplicativos** no menu superior.

	![Atribuir usuário][201]

2. Na lista de aplicativos, selecione **Origami**.

	![Configurar o logon único](./media/active-directory-saas-origami-tutorial/tutorial_origami_50.png)

3. No menu na parte superior, clique em **Usuários**.

	![Atribuir usuário][203]

4. Na lista Usuários, selecione **Brenda Fernandes**.

5. Na barra de ferramentas na parte inferior, clique em **Atribuir**.

	![Atribuir usuário][205]


### Teste do logon único

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Ao clicar no bloco do Origami no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo do Origami.


## Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-origami-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-origami-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-origami-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-origami-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-origami-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-origami-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-origami-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-origami-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-origami-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-origami-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-origami-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-origami-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-origami-tutorial/tutorial_general_205.png

<!---HONumber=AcomDC_0504_2016-->