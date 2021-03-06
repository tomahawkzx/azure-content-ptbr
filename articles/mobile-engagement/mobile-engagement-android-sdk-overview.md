<properties
	pageTitle="Integração do Android SDK para Azure Mobile Engagement"
	description="Descreve como integrar o SDK do Azure Mobile Engagement em aplicativos Android"
	services="mobile-engagement"
	documentationCenter="mobile"
	authors="piyushjo"
	manager="erikre"
	editor="" />

<tags
	ms.service="mobile-engagement"
	ms.workload="mobile"
	ms.tgt_pltfrm="mobile-android"
	ms.devlang="Java"
	ms.topic="article"
	ms.date="05/17/2016"
	ms.author="piyushjo;ricksal" />

# Integração do Android SDK para Azure Mobile Engagement

> [AZURE.SELECTOR]
- [Universal do Windows](mobile-engagement-windows-store-sdk-overview.md)
- [Windows Phone Silverlight](mobile-engagement-windows-phone-sdk-overview.md)
- [iOS](mobile-engagement-ios-sdk-overview.md)
- [Android](mobile-engagement-android-sdk-overview.md)

Este documento descreve todas as opções de integração e configuração disponíveis para o SDK do Azure Mobile Engagement para Android.

## Pré-requisitos

[AZURE.INCLUDE [Pré-requisitos](../../includes/mobile-engagement-android-prereqs.md)]

## Recursos avançados

### Recursos de relatório

Você pode adicionar esses recursos:

1. [Opções de relatório avançadas](mobile-engagement-android-advanced-reporting.md)
2. [Opções de relatório de localização](mobile-engagement-android-location-reporting.md)
3. [Opções de configuração avançada](mobile-engagement-android-advanced-configuration.md)

### Notificações:
[Como integrar o Reach (notificações) em seu aplicativo Android](mobile-engagement-android-integrate-engagement-reach.md)

1. GCM (Google Cloud Messaging): [como integrar o GCM com o Mobile Engagement](mobile-engagement-android-gcm-integrate.md)

2. ADM (Amazon Device Messaging): [como integrar o ADM com o Mobile Engagement](mobile-engagement-android-adm-integrate.md)

### Implementação do plano de marca:
[Como usar a API de marcação avançada do Mobile Engagement em seu aplicativo Android](mobile-engagement-android-use-engagement-api.md)

## Notas de versão

### 4\.2.2 (17/05/2016)

- Aprimoramentos de estabilidade.

### 4\.2.1 (10/05/2016)

- Segurança: desabilite o acesso de arquivo local de exibição na Web.
- Segurança: remova a classe `EngagementPreferenceActivity` que estende a classe `PreferenceActivity` obsoleta e não segura.
- Segurança: atividades de alcance agora estão documentadas para usar `exported="false"`; esse sinalizador também pode ser usado em versões anteriores do SDK.

### 4\.2.0 (03/11/2016)

- O SDK está licenciado sob MIT.
- Permita a especificação de um identificador de dispositivo personalizado no momento de inicialização do SDK.

Para obter todas as versões, veja as [notas de versão completas](mobile-engagement-android-release-notes.md).

## Procedimentos de atualização

Se você já tiver integrado uma versão mais antiga do nosso SDK em seu aplicativo, consulte os [Procedimentos de Atualização](mobile-engagement-android-upgrade-procedure.md).

<!---HONumber=AcomDC_0518_2016-->