<properties
	pageTitle="Solução de problemas: criar e conectar-se a um espaço de trabalho do Aprendizado de Máquina | Microsoft Azure"
	description="Soluções para problemas comuns na criação e conexão a um espaço de trabalho de aprendizado de máquina do Azure"
	services="machine-learning"
	documentationCenter=""
	authors="garyericson"
	manager="paulettm"
	editor="cgronlun"/>

<tags
	ms.service="machine-learning"
	ms.workload="data-services"
	ms.tgt_pltfrm="na"
	ms.devlang="na"
	ms.topic="article"
	ms.date="03/09/2016"
	ms.author="garye"/>


# Guia de solução de problemas: criar e conectar-se a um espaço de trabalho do Aprendizado de Máquina

Este guia fornece soluções para alguns desafios encontrados com frequência quando você configura espaços de trabalho do Aprendizado de Máquina do Azure.

[AZURE.INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## Proprietário do espaço de trabalho

Quando você cria um novo espaço de trabalho do Aprendizado de Máquina, a ID que você insere no campo PROPRIETÁRIO DO ESPAÇO DE TRABALHO deve ser uma conta da Microsoft válida (anteriormente conhecida como Windows Live ID), por exemplo, john-contoso@live.com ou john-contoso@hotmail.com. Não pode ser uma conta que não seja da Microsoft, como seu e-mail corporativo. Para criar uma conta gratuita da Microsoft, acesse [www.live.com](http://www.live.com).

Observe que a conta usada para entrar no Portal Clássico do Azure para criar o espaço de trabalho não tem automaticamente permissão para *abrir* esse espaço de trabalho, a menos que você especifique essa conta como proprietária. Para abrir um espaço de trabalho no Estúdio de Aprendizado de Máquina, você deve estar conectado à Conta da Microsoft que foi definida como proprietária do espaço de trabalho ou precisa receber um convite do proprietário para ingressar no espaço de trabalho. No entanto, no Portal Clássico do Azure, você pode *gerenciar* o espaço de trabalho, o que inclui a capacidade de alterar o proprietário e configurar o acesso.

Para obter mais informações sobre como gerenciar um espaço de trabalho, consulte [Gerenciar um espaço de trabalho do Aprendizado de Máquina do Azure].

[Gerenciar um espaço de trabalho do Aprendizado de Máquina do Azure]: machine-learning-manage-workspace.md

## Regiões permitidas

No momento, o Aprendizado de Máquina está disponível em um número limitado de regiões. Se sua assinatura não incluir uma dessas regiões, talvez você receba a mensagem de erro “Você não tem assinaturas nas regiões permitidas”.

Para solicitar a adição de uma região à sua assinatura, selecione **Entre em contato com o Suporte da Microsoft** no Portal Clássico do Azure, escolha **Cobrança** como o tipo de problema e siga os prompts para enviar sua solicitação.

![Contatar Suporte da Microsoft][screen1]

## Conta de armazenamento

O serviço de Aprendizado de Máquina precisa de uma conta de armazenamento para armazenar dados. Você pode usar uma conta de armazenamento existente, ou pode criar uma nova conta de armazenamento ao criar o novo espaço de trabalho de Aprendizado de Máquina (se você tiver cota para criar uma nova conta de armazenamento).

<!-- These instructions no longer work, but I'm not sure what to replace them with
To see if you can create a new storage account, in the Classic Portal, go to **Settings** and then click **Usage**.
-->

![Criar espaço de trabalho][screen2]

Depois que o novo espaço de trabalho do Aprendizado de Máquina for criado, você poderá entrar no Estúdio de Aprendizado de Máquina usando a conta da Microsoft especificada como proprietária do espaço de trabalho. Se você encontrar a mensagem de erro "Espaço de Trabalho Não Encontrado" (semelhante à captura de tela a seguir), use as etapas a seguir para excluir os cookies do navegador.

![Espaço de trabalho não encontrado][screen3]

**Para excluir cookies do navegador**

Se você usa o Internet Explorer, clique no botão **Ferramentas** no canto superior direito e selecione **Opções da Internet**.

![Opções da Internet][screen4]

Na guia **Geral**, clique em **Excluir…**

![Guia Geral][screen5]

Na caixa de diálogo **Excluir Histórico de Navegação**, selecione **Cookies e dados de sites** e clique em **Excluir**.

![Excluir cookies][screen6]

Depois que os cookies forem excluídos, reinicie o navegador e vá para a página [Aprendizado de Máquina do Microsoft Azure](https://studio.azureml.net). Quando forem solicitados nome de usuário e senha, insira os dados da mesma conta da Microsoft que você especificou como conta do proprietário do espaço de trabalho.

Nosso objetivo é tornar a experiência do Aprendizado de Máquina o mais simples possível. Poste comentários e problemas no [Fórum do Aprendizado de Máquina do Azure](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) para nos ajudar a atendê-lo melhor.

[screen1]: media/machine-learning-troubleshooting-creating-ml-workspace/screen1.png
[screen2]: media/machine-learning-troubleshooting-creating-ml-workspace/screen2.png
[screen3]: media/machine-learning-troubleshooting-creating-ml-workspace/screen3.png
[screen4]: media/machine-learning-troubleshooting-creating-ml-workspace/screen4.png
[screen5]: media/machine-learning-troubleshooting-creating-ml-workspace/screen5.png
[screen6]: media/machine-learning-troubleshooting-creating-ml-workspace/screen6.png

<!---HONumber=AcomDC_0316_2016-->