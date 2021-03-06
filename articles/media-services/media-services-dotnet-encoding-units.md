<properties 
	pageTitle="Como adicionar unidades de codificação" 
	description="Saiba como adicionar unidades de codificação com o .NET"  
	services="media-services" 
	documentationCenter="" 
	authors="juliako" 
	manager="erikre" 
	editor=""/>

<tags 
	ms.service="media-services" 
	ms.workload="media" 
	ms.tgt_pltfrm="na" 
	ms.devlang="na" 
	ms.topic="article" 
 	ms.date="04/18/2016"
	ms.author="juliako;milangada;gtrifonov"/>


#Como dimensionar a codificação com o SDK do .NET


> [AZURE.SELECTOR]
- [Portal](media-services-portal-encoding-units.md)
- [.NET](media-services-dotnet-encoding-units.md)
- [REST](https://msdn.microsoft.com/library/azure/dn859236.aspx)
- [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
- [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)

##Visão geral

Uma conta de serviços de mídia está associada a um tipo de unidade reservada que determina a velocidade com que seus trabalhos de codificação são processados. Você pode escolher entre os seguintes tipos de unidade reservada: S1, S2 ou S3. Por exemplo, o mesmo trabalho de codificação é executado mais rápido quando se usa o tipo de unidade reservada Standard em comparação com aquela do tipo Básico. Para saber mais, consulte o blog "Encoding Reserved Unit Types”, escrito por [Milan Gada](https://azure.microsoft.com/blog/high-speed-encoding-with-azure-media-services/).

Além de especificar o tipo de unidade reservada, você pode especificar para provisionar sua conta com unidades reservadas para codificação. O número de unidades reservadas para codificação provisionada determina o número de tarefas de mídia que podem ser processadas simultaneamente em uma determinada conta. Por exemplo, se sua conta tiver cinco unidades reservadas, as cinco tarefas de mídia serão executadas simultaneamente enquanto houver tarefas para serem processadas. As tarefas restantes irão aguardar na fila e serão selecionadas para processamento sequencialmente assim que uma tarefa em execução seja concluída. Se uma conta não tiver nenhuma unidade reservada provisionada, as tarefas serão selecionadas sequencialmente. Nesse caso, o tempo de espera entre a conclusão de uma tarefa e o início da próxima dependerá da disponibilidade dos recursos do sistema.

Para alterar o tipo de unidade reservada e o número de unidades reservadas para codificação usando o SDK do .NET, faça o seguinte:

IEncodingReservedUnit encodingS1ReservedUnit = \_context.EncodingReservedUnits.FirstOrDefault(); encodingS1ReservedUnit.ReservedUnitType = ReservedUnitType.Basic; // Corresponds to S1 encodingS1ReservedUnit.Update(); Console.WriteLine("Tipo de unidade reservada: {0}", encodingS1ReservedUnit.ReservedUnitType);

encodingS1ReservedUnit.CurrentReservedUnits = 2; encodingS1ReservedUnit.Update();

Console.WriteLine("Número de unidade reservadas: {0}", encodingS1ReservedUnit.CurrentReservedUnits);

##Abrindo um tíquete de suporte

Por padrão, todas as contas dos Serviços de Mídia podem ser dimensionadas para até 25 Unidades Reservadas para Codificação e cinco para Streaming por Demanda. Você pode solicitar um limite mais alto abrindo um tíquete de suporte.

###Abra um tíquete de suporte

Para abrir um tíquete de suporte, faça o seguinte:

1. Clique em [Obter suporte](https://manage.windowsazure.com/?getsupport=true). Se você não estiver conectado, você será solicitado a inserir suas credenciais.

1. Selecione sua assinatura.

1. Em tipo de suporte, selecione "Técnico".

1. Clique em "Criar Tíquete".

1. Selecione "Serviços de Mídia do Azure" na lista de produtos apresentados na próxima página.

1. Selecione um "tipo de problema" que é apropriado para o seu problema.

1. Clique em Continuar.

1. Siga as instruções na próxima página e, em seguida, insira os detalhes sobre o problema.

1. Clique em Enviar para abrir o tíquete.



##Roteiros de aprendizagem dos Serviços de Mídia

[AZURE.INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

##Fornecer comentários

[AZURE.INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

<!---HONumber=AcomDC_0518_2016-->