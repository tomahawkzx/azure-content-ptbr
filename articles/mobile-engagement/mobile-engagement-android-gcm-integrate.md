<properties
	pageTitle="Integração do SDK do Android do Azure Mobile Engagement"
	description="Atualizações e procedimentos mais recentes para o SDK do Android do Azure Mobile Engagement"
	services="mobile-engagement"
	documentationCenter="mobile"
	authors="piyushjo"
	manager="dwrede"
	editor="" />

<tags
	ms.service="mobile-engagement"
	ms.workload="mobile"
	ms.tgt_pltfrm="mobile-android"
	ms.devlang="Java"
	ms.topic="article"
	ms.date="03/10/2016"
	ms.author="piyushjo" />

#Como integrar o GCM ao Mobile Engagement

> [AZURE.IMPORTANT] Você deve seguir o procedimento de integração descrito no documento Como Integrar o Engagement, antes de seguir este guia.
>
> Este documento será útil apenas se você já tiver integrado o módulo de Alcance e planeja enviar por push os dispositivos Google Play. Para integrar campanhas de Alcance em seu aplicativo, leia primeiro Como Integrar o Engagement Reach no Android.

##Introdução

A integração do GCM permite que o seu aplicativo seja enviado por push.

As cargas do GCM enviadas por push para o SDK sempre contêm a chave `azme` no objeto de dados. Portanto, se você usar o GCM para outra finalidade em seu aplicativo, é possível filtrar os pushes com base nessa chave.

> [AZURE.IMPORTANT] Somente os dispositivos que executam Android 2.2 ou acima, com o Google Play instalado e com a conexão em tela de fundo do Google habilitada podem ser enviados por push pelo GCM; no entanto, você pode integrar esse código com segurança em dispositivos sem suporte (ele apenas utiliza intenções).

##Criar um projeto do Google Cloud Messaging com uma chave de API

[AZURE.INCLUDE [mobile-engagement-enable-Google-cloud-messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

> [AZURE.IMPORTANT] O **Número do Projeto** não deve ser confundido com a **ID do Projeto**.

##Integração do SDK

### Gerenciando registros de dispositivo

Cada dispositivo deve enviar um comando de registro aos servidores do Google, caso contrário eles não poderão ser alcançados.

Um dispositivo também pode cancelar o registro de notificações do GCM (o registro do dispositivo será cancelado automaticamente se o aplicativo for desinstalado).

Se você não usa o [SDK do Google Play] ou ainda não enviou a intenção de registro por conta própria, você poderá fazer com que o Engagement registre o dispositivo automaticamente para você.

Para habilitar isso, adicione o seguinte ao seu arquivo `AndroidManifest.xml` dentro da marca`<application/>`:

			<!-- If only 1 sender, don't forget the \n, otherwise it will be parsed as a negative number... -->
			<meta-data android:name="engagement:gcm:sender" android:value="<Your Google Project Number>\n" />

### Comunicar a ID de registro para o serviço de envio por push do Engagement e receber notificações

Para comunicar a ID de registro do dispositivo para o serviço de envio por push do Engagement e receber notificações, adicione o seguinte ao seu arquivo `AndroidManifest.xml` dentro da marca `<application/>` (mesmo que você gerencie registros de dispositivo por conta própria):

			<receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMEnabler"
			  android:exported="false">
			  <intent-filter>
			    <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT" />
			  </intent-filter>
			</receiver>

			<receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMReceiver" android:permission="com.google.android.c2dm.permission.SEND">
			  <intent-filter>
			    <action android:name="com.google.android.c2dm.intent.REGISTRATION" />
			    <action android:name="com.google.android.c2dm.intent.RECEIVE" />
			    <category android:name="<your_package_name>" />
			  </intent-filter>
			</receiver>

Certifique-se de ter as seguintes permissões em seu `AndroidManifest.xml` (após a marca `</application>`).

			<uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
			<uses-permission android:name="<your_package_name>.permission.C2D_MESSAGE" />
			<permission android:name="<your_package_name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

##Permitir acesso do Mobile Engagement à sua chave de API do GCM

Siga [este guia](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) para permitir acesso do Mobile Engagement à sua chave de API do GCM.

[SDK do Google Play]: https://developers.google.com/cloud-messaging/android/start

<!---HONumber=AcomDC_0316_2016-->