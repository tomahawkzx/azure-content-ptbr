<properties 
   pageTitle="Monitore o uso e estatísticas em um serviço da Pesquisa do Azure | Microsoft Azure | Serviço de pesquisa de nuvem hospedado" 
   description="Acompanhe o consumo de recursos e o tamanho de índice da Pesquisa do Azure, um serviço de pesquisa de nuvem hospedado do Microsoft Azure." 
   services="search" 
   documentationCenter="" 
   authors="HeidiSteen" 
   manager="paulettm" 
   editor=""
   tags="azure-portal"/>

<tags
   ms.service="search"
   ms.devlang="na"
   ms.topic="article"
   ms.tgt_pltfrm="na"
   ms.workload="required" 
   ms.date="05/17/2016"
   ms.author="heidist"/>

# Monitorar o uso e as estatísticas em um serviço de Pesquisa do Azure

Acompanhar o crescimento do tamanho dos índices e do documento pode ajudar você a ajustar a capacidade de forma proativa antes de atingir o limite superior que você estabeleceu para seu serviço.

Para monitorar o uso de recursos, você pode ver as contagens e estatísticas do seu serviço com facilidade no [Portal do Azure](https://portal.azure.com), mas também pode obter essas informações por meio de programação se estiver criando uma ferramenta de administração de serviço personalizada. Este artigo aborda as etapas das duas técnicas.

Você também pode usar o novo recurso de análise de tráfego de pesquisa para obter informações sobre as atividades no nível do índice. Visite [Análise de Tráfego de Pesquisa para a Pesquisa do Azure](search-traffic-analytics.md) para começar.

##Ver contagens e métricas no portal 

1. Entre no [Portal do Azure](https://portal.azure.com). 

2. Abra o painel de serviços de seu serviço de Pesquisa do Azure. É possível encontrar blocos do serviço na Home page, ou você pode navegar até o serviço usando Procurar na Barra de navegação rápida. Confira [Criar um serviço](search-create-service-portal.md) para obter instruções passo a passo.

A seção Uso inclui um medidor que informa qual parte dos recursos disponíveis estão atualmente em uso.

  ![][1]

Lembre-se de que o serviço compartilhado tem um máximo de uma réplica por cada partição. Além disso, ele pode dar suporte a apenas 10.000 documentos no total ou 50 MB de dados, o que ocorrer primeiro.

##Obter estatísticas de índice usando a API REST

A API REST da Pesquisa do Azure e o SDK do .NET fornecem acesso programático às métricas de serviço. Se você estiver usando [indexadores](https://msdn.microsoft.com/library/azure/dn946891.aspx) para carregar um índice do Banco de Dados SQL ou do Banco de Dados de Documentos do Azure, uma API adicional estará disponível para obter os números dos quais você precisa.

  + [Obter estatísticas de índice](https://msdn.microsoft.com/library/azure/dn798942.aspx)
  + [Contar documentos](https://msdn.microsoft.com/library/azure/dn798924.aspx)
  + [Obter o status do indexador](https://msdn.microsoft.com/library/azure/dn946884.aspx)

## Próximas etapas

Revise [limites e capacidade](search-limits-quotas-capacity.md) para determinar a combinação de partições e réplicas que você precisará se a capacidade existente for insuficiente.

Visite [Gerenciar o serviço de pesquisa no Microsoft Azure](search-manage.md) para saber mais sobre a administração do serviço.

<!--Image references-->
[1]: ./media/search-monitor-usage/AzureSearch-Monitor1.PNG




 

<!---HONumber=AcomDC_0518_2016-->