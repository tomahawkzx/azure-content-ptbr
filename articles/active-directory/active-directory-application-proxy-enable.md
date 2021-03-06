<properties
	pageTitle="Habilitar o Proxy de Aplicativo do Azure AD | Microsoft Azure"
	description="Habilite o Proxy de Aplicativo no portal clássico do Azure e instale os Conectores para o proxy reverso."
	services="active-directory"
	documentationCenter=""
	authors="kgremban"
	manager="StevenPo"
	editor=""/>

<tags
	ms.service="active-directory"
	ms.workload="identity"
	ms.tgt_pltfrm="na"
	ms.devlang="na"
	ms.topic="get-started-article"
	ms.date="06/01/2016"
	ms.author="kgremban"/>

# Habilitar o Proxy de aplicativo no portal do Azure

Este artigo o orienta através sobre como habilitar o Proxy de Aplicativo do Microsoft Azure AD para seu diretório de nuvem no Azure AD. Isso envolve a instalação do Conector de Proxy de Aplicativo em sua rede privada, que mantém a conexão de rede com o serviço de proxy. Você também registrará o Conector com sua assinatura de locatário do Microsoft Azure AD. Se você estiver familiarizado com o que o Proxy de Aplicativo pode ajudá-lo a fazer, saiba mais sobre [Como fornecer acesso remoto seguro a aplicativos locais](active-directory-application-proxy-get-started.md).

Após concluir este passo a passo para habilitar o Proxy de Aplicativo do Azure AD, você estará pronto para publicar aplicativos locais para acesso remoto.

> [AZURE.NOTE] O Proxy de Aplicativo é um recurso que está disponível somente se você tiver atualizado para a edição Premium ou Básica do Active Directory do Azure. Para obter mais informações, consulte [Edições do Active Directory do Azure](active-directory-editions.md).

## Pré-requisitos de Proxy de aplicativo
Antes de habilitar e usar os serviços de Proxy de aplicativo, você precisa ter:

- Uma [assinatura premium ou básica](active-directory-editions.md) do Microsoft Azure AD e um diretório do Azure AD do qual você seja administrador global.
- Um servidor executando o Windows Server 2012 R2 ou Windows 8.1 ou posterior em que você possa instalar o Conector do Proxy de Aplicativo. O servidor enviará solicitações HTTPS aos serviços de Proxy de Aplicativo na nuvem e precisa de uma conexão HTTPS para os aplicativos que você deseja publicar.
- Se um firewall for colocado no caminho, verifique se o firewall está aberto para que o Conector possa fazer solicitações HTTPS (TCP) para o Proxy de Aplicativo. O Conector usa essas portas com subdomínios que fazem parte dos domínios de alto nível: *msappproxy.net* e *servicebus.windows.net*. Não esqueça de abrir **todas** as seguintes portas para o tráfego de **saída**:

	| Número da porta | Descrição |
	| --- | --- |
	| 80 | Para habilitar o tráfego HTTP de saída para a validação de segurança. |
	| 443 | Para habilitar a autenticação de usuário no Azure AD (necessário somente para o processo de registro do conector) |
	| 10100 - 10120 | Para habilitar respostas HTTP LOB enviadas de volta para o proxy |
	| 9352, 5671 | Para habilitar a comunicação entre o conector de serviço do Azure para solicitações de entrada. |
	| 9350 | Opcional, para permitir o melhor desempenho em solicitações de entrada. |
	| 8080 | Para habilitar a sequência de inicialização do Conector e habilitar sua atualização automática |
	| 9090 | Para ativar o registro do conector (necessário somente para o processo de registro do conector) |
	| 9091 | Para ativar a renovação automática de certificados de confiança de conector |

Se o firewall reforça o tráfego de acordo com os usuários de origem, abra essas portas para o tráfego proveniente de serviços do Windows em execução como um serviço de rede. Além disso, certifique-se de habilitar a porta 8080 para Autoridade NT\\Sistema.


## Etapa 1: habilite o Proxy de aplicativo no AD do Azure
1. Entre como administrador no [portal clássico do Azure](https://manage.windowsazure.com/).
2. Vá para o Active Directory e selecione o diretório no qual você deseja habilitar o Proxy de aplicativo.

	![Active Directory - ícone](./media/active-directory-application-proxy-enable/ad_icon.png)

3. Selecione **Configurar** na página de diretório e role para baixo até **Proxy de Aplicativo**.
4. Alterne **Habilitar serviços de Proxy de Aplicativo para este Diretório** para **Habilitado**.

	![Habilitar Proxy de aplicativo](./media/active-directory-application-proxy-enable/app_proxy_enable.png)

5. Selecione **Baixar agora**. Isso o levará para a **Download do Conector de Proxy de Aplicativo do Azure AD**. Leia e aceite os termos de licença e clique em **Download** para salvar o arquivo do Windows Installer (.exe) do Conector de Proxy de Aplicativo.

## Etapa 2: Instalar e registrar o conector
1. Execute *AADApplicationProxyConnectorInstaller.exe* no servidor que você preparou de acordo com os pré-requisitos acima.
2. Siga as instruções no Assistente para instalar.
3. Durante a instalação, você será solicitado a registrar o Conector com o Proxy de Aplicativo do seu locatário do AD do Azure.

  - Forneça suas credenciais de administrador global do AD do Azure. Seu locatário de administrador global pode ser diferente das suas credenciais do Microsoft Azure.
  - Verifique se o administrador que registra o Conector está no mesmo diretório em que você habilitou o serviço de Proxy de Aplicativo. Por exemplo, se o domínio de locatário for contoso.com, o administrador deverá ser admin@contoso.com ou qualquer outro alias no domínio.
  - Se a **Configuração de Segurança Aprimorada do Internet Explorer** estiver **Ativada** no servidor em que você estiver instalando o Conector do Azure AD, a tela de registro poderá ser bloqueada. Se isso acontecer, siga as instruções na mensagem de erro para permitir o acesso. Certifique-se de que a Segurança Melhorada do Internet Explorer está desativada.
  - Se o registro do Conector não for bem-sucedido, confira [Solucionar problemas de Proxy de Aplicativo](active-directory-application-proxy-troubleshoot.md).  

4. Quando a instalação for concluída, dois novos serviços são adicionados ao seu servidor, conforme mostrado abaixo.

 	- O **Conector de Proxy de Aplicativo do Microsoft AAD** habilita a conectividade
	- O **Atualizador do Conector de Proxy de Aplicativo do Microsoft AAD** é um serviço de atualização automatizada que verifica periodicamente se há novas versões do conector e atualiza o Conector conforme necessário.

	![Serviços do Conector de Proxy de Aplicativo - captura de tela](./media/active-directory-application-proxy-enable/app_proxy_services.png)

5. Clique em **Concluir** na janela de instalação para concluir a instalação.

Agora você está pronto para [Publicar aplicativos com o Proxy de Aplicativo](active-directory-application-proxy-publish.md).

Para fins de alta disponibilidade, você deve implantar pelo menos um Conector adicional. Para implantar mais Conectores, repita as etapas 2 e 3 acima. Cada conector deve ser registrado separadamente.

Se você deseja desinstalar o Conector, desinstale o serviço Conector e o serviço Atualizador; não deixe de reiniciar o computador para remover completamente o serviço.


## Próximas etapas

- [Publique aplicativos com proxy de aplicativo](active-directory-application-proxy-publish.md)
- [Publicar aplicativos usando seu próprio nome de domínio](active-directory-application-proxy-custom-domains.md)
- [Habilitar o logon único](active-directory-application-proxy-sso-using-kcd.md)
- [Solucionar problemas que surgirem com o Proxy de Aplicativo](active-directory-application-proxy-troubleshoot.md)

Para obter as últimas notícias e atualizações, confira o [blog do Proxy de Aplicativo](http://blogs.technet.com/b/applicationproxyblog/)

<!---HONumber=AcomDC_0608_2016-->