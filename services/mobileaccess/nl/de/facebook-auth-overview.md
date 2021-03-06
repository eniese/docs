---

copyright:
  years: 2015, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Benutzer mit Facebook-Berechtigungsnachweisen authentifizieren
{: #facebook-auth-overview}

Letzte Aktualisierung: 22. Juli 2016
{: .last-updated}

Sie können den {{site.data.keyword.amashort}}-Service zum Schützen von Ressourcen durch die Verwendung von Facebook als Identitätsprovider konfigurieren. Die Benutzer Ihrer mobilen Anwendung oder Ihrer Webanwendung können ihre Facebook-Berechtigungsnachweise für die Authentifizierung nutzen.
{:shortdesc}

**Wichtig:** Sie müssen das von Facebook bereitgestellte Client-SDK nicht separat installieren. Das Facebook-SDK wird automatisch durch Abhängigkeitenmanager installiert, wenn Sie das {{site.data.keyword.amashort}}-Facebook-Client-SDK konfigurieren.

## {{site.data.keyword.amashort}}-Anforderungsablauf
{: #mca-facebook-sequence}

### Anforderungsablauf für mobilen Client

Im folgenden Diagramm wird die Integration von {{site.data.keyword.amashort}} in Facebook für die Authentifizierung über eine App eines mobilen Clients veranschaulicht.

![Anforderungsablaufdiagramm für mobilen Client](images/mca-sequence-facebook.jpg)

* Verwenden Sie das {{site.data.keyword.amashort}}-Client-SDK zum Senden einer Anforderung an Ihre Back-End-Ressourcen, die mit dem {{site.data.keyword.amashort}}-Server-SDK geschützt werden. 
* Das {{site.data.keyword.amashort}}-Server-SDK erkennt eine nicht autorisierte Anforderung und gibt den Code HTTP 401 sowie den Berechtigungsbereich zurück.
* Das {{site.data.keyword.amashort}}-Client-SDK erkennt den Code HTTP 401 automatisch und startet den Authentifizierungsprozess.
* Das {{site.data.keyword.amashort}}-Client-SDK kontaktiert den {{site.data.keyword.amashort}}-Service und fordert einen Berechtigungsheader an. 
* Der {{site.data.keyword.amashort}}-Service fordert den Client auf, sich zuerst bei Facebook durch die Bereitstellung einer Authentifizierungsanforderung (Challenge) zu authentifizieren.
* Das {{site.data.keyword.amashort}}-Client-SDK verwendet das Facebook-SDK, um den Authentifizierungsprozess zu starten. Nach einer erfolgreichen Authentifizierung gibt das Facebook-SDK ein Facebook-Zugriffstoken zurück.
* Das Facebook-Zugriffstoken wird als Antwort auf die Authentifizierungsanforderung (Challenge) betrachtet. Das Token wird an den {{site.data.keyword.amashort}}-Service gesendet.
* Der Service validiert die Antwort auf die Authentifizierungsanforderung mit Facebook-Servern.
* Wenn die Validierung erfolgreich ist, generiert der {{site.data.keyword.amashort}}-Service einen Berechtigungsheader und gibt diesen an das {{site.data.keyword.amashort}}-Client-SDK zurück. Der Berechtigungsheader enthält zwei Tokens: ein Zugriffstoken, das Informationen zu Zugriffsberechtigungen enthält, und ein ID-Token, das Informationen zum aktuellen Benutzer, zum Gerät und zur Anwendung enthält.
* Von diesem Punkt an haben alle Anforderungen, die durch das {{site.data.keyword.amashort}}-Client-SDK gesendet werden, einen neu abgerufenen Berechtigungsheader.
* Das {{site.data.keyword.amashort}}-Client-SDK wiederholt automatisch das Senden der ursprünglichen Anforderung, die den Berechtigungsablauf ausgelöst hat.
* Das {{site.data.keyword.amashort}}-Server-SDK extrahiert den Berechtigungsheader aus der Anforderung, validiert ihn mit dem {{site.data.keyword.amashort}}-Service und erteilt den Zugriff auf eine Back-End-Ressource. 

### {{site.data.keyword.amashort}}-Anforderungsablauf für Webanwendung
{: #mca-facebook-web-sequence}

Der {{site.data.keyword.amashort}}-Anforderungsablauf für eine Webanwendung ist vergleichbar mit dem Ablauf für einen mobilen Client. {{site.data.keyword.amashort}} schützt jedoch die Webanwendung anstatt einer {{site.data.keyword.Bluemix_notm}}-Back-End-Ressource. 

  * Die ursprüngliche Anforderung wird von der Webanwendung (zum Beispiel von einem Anmeldeformular) gesendet. 
  * Die letzte Weiterleitung erfolgt an den geschützten Bereich der Webanwendung selbst anstatt an die geschützte Back-End-Ressource.  


## Facebook-Anwendungs-ID vom Facebook-Entwicklerportal anfordern
{: #facebook-appID}

Zur Verwendung von Facebook als Identitätsprovider müssen Sie eine Anwendung im Facebook-Entwicklerportal erstellen. Bei diesem Prozess erhalten Sie eine Facebook-Anwendungs-ID, bei der es sich um eine eindeutige Kennung handelt, an der Facebook erkennt, welche Anwendung versucht, eine Verbindung herzustellen.

1. Öffnen Sie das [Facebook-Entwicklerportal](https://developers.facebook.com).

1. Klicken Sie auf **My Apps** im Menü und wählen Sie die Option **Create a new app** aus.
Wählen Sie entweder iOS- oder Android-Anwendung aus und klicken Sie auf **Skip and Create App ID** auf der nächsten Anzeige. 

1. Legen Sie den Anzeigenamen der Anwendung nach Ihrer Wahl fest und wählen Sie eine Kategorie aus. Klicken Sie auf **Create App ID**, um fortzufahren.

1. Kopieren Sie den angezeigten Wert für **App ID**. Dieser Wert ist Ihre Facebook-Anwendungs-ID.  Sie benötigen diesen Wert, um die Facebook-Authentifizierung für Ihre mobile App oder Ihre Web-App zu konfigurieren.

## Nächste Schritte
{: #next-steps}

* [Facebook-Authentifizierung für Android-Apps aktivieren](facebook-auth-android.html)
* [Facebook-Authentifizierung für iOS-Apps aktivieren (Swift-SDK)](facebook-auth-ios-swift-sdk.html)
* [Facebook-Authentifizierung für iOS-Apps aktivieren (Objective-C-SDK - nicht mehr verwendet)](facebook-auth-ios.html)
* [Facebook-Authentifizierung für Cordova-Apps aktivieren](facebook-auth-cordova.html)
