---

copyright:
  years: 2016

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# Installation et connexion du modèle d'application mobile 
{: #iotins_gettingstarted}
Dernière mise à jour : 12 septembre 2016
{: .last-updated}

Le modèle d'application mobile {{site.data.keyword.iotinsurance_full}} est une implémentation de référence d'un client mobile d'{{site.data.keyword.iotinsurance_short}}. Vous
pouvez utiliser l'application pour enregistrer de nouveaux périphériques sur le système et recevoir des alertes pour les périphériques. {:shortdesc}

**Configuration requise :** avant de commencer, assurez-vous de disposer des éléments requis suivants :

  - L'environnement de développement intégré Apple Xcode 7.3 ou version ultérieure. 
  - Un périphérique mobile iPhone avec iOS 9.0 ou version ultérieure. 
  - CocoaPods installé sur votre ordinateur. Voir le [site Web CocoaPods](https://guides.cocoapods.org/using/getting-started.html).
  - Les [paramètres](#iot4i_mobileParam) requis pour connecter le modèle d'application mobile à votre instance du service.


## Génération du modèle d'application mobile 
{: #building_mobile}
Pour tester le modèle d'application mobile, procédez comme suit : 

1. Clonez le [référentiel de code source pour le modèle d'application mobile](https://github.com/ibm-watson-iot/ioti-mobile) sur
un ordinateur sur lequel Xcode 7.3 ou version ultérieure est installé. 
2. Installez les packages requis et générez le fichier IoT4I.xcworkspace en exécutant la commande CocoaPods pod install pour votre projet. CocoaPods
doit être installé pour que vous puissiez effectuer cette tâche. 
3. Ouvrez le projet dans Xcode en cliquant deux fois sur le fichier IoT4I.xcworkspace. 
4. Connectez votre iPhone à votre ordinateur et sélectionnez-le comme destination de génération. 
5. Sélectionnez le fichier IoT4I dans la liste de fichiers afin d'afficher la boîte de dialogue Identity. 
6. Dans la boîte de dialogue Identity dans Xcode, apportez les modifications suivantes : 
  - Pour **Bundle Identifier**, indiquez un identificateur unique, par exemple **myIoT4Ibundle**.
  - Dans la zone **Team**, indiquez le nom de votre équipe personnelle, puis cliquez sur **Fix Issue**.
7. Pour connecter votre application à votre instance d'{{site.data.keyword.iotinsurance_short}}, définissez les paramètres suivants dans le
fichier **constants.swift** :   
    - [applicationRoute](#iot4i_mobileParam) = adresse URL de votre instance d'{{site.data.keyword.iotinsurance_short}}
    - [applicationId](#iot4i_mobileParam) = adresse URL de votre instance de {{site.data.keyword.amashort}}
8. Sur votre ordinateur, cliquez sur la flèche afin de générer et d'exécuter le schéma en cours. Le modèle d'application mobile est installé sur
votre téléphone. Pour plus d'informations, voir
les
[instructions
d'exécution d'applications sur des périphériques depuis Xcode pour les développeurs Apple](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/LaunchingYourApponDevices/LaunchingYourApponDevices.html).

  **Remarque :** si une erreur *Could not launch IoT4I because you have not yet
verified that your Developer App certificate is trusted on your device* est affichée lors de la tentative de génération, sélectionnez-vous comme
développeur digne de confiance, comme suit :
  
    1. Sur votre téléphone, sélectionnez **Paramètres > Général > Gestion des terminaux > votreIDDéveloppeur**.
    2. Tapez sur le nom de votre compte d'ID de développeur afin d'accréditer votre ID de développeur. 
    3. Lorsque vous y êtes invité, confirmez que l'ID de développeur est digne de confiance.

## Activation de notifications push pour l'application mobile 
{: #iot4i_pushNotification}

Procédez comme suit afin d'activer des notifications push pour votre périphérique mobile. Vous devez disposer d'un compte de
développeur Apple valide pour pouvoir utiliser le service de notification push.


1. Connectez-vous à votre compte de développeur Apple à l'adresse https://developer.apple.com/account.

2. Créez un fichier certificat. 
  1. Sélectionnez **Certificates, Identifiers & Profiles**.
  2. Sélectionnez Identifiers: App IDs.
  3. Cliquez sur le bouton d'ajout (+) pour créer un ID d'application. 
  4. Entrez une description de l'application dans **Description**.
  5. Sélectionnez **Explicit App ID** et entrez un ID de bundle, par exemple
com.NomDeVotreOrganisation.iot4i.mobileApp).
  6. Sélectionnez (V) dans **Push Notifications** et cliquez sur **Continue > Register > Done**.

3. Créez un certificat de notification push. 
  1. Sélectionnez **Certificates: All**.
  2. Cliquez sur le bouton d'ajout (+) pour créer un certificat APN. 
  3. Dans la page Add iOS Certificate, sélectionnez **Apple Push Notification service SSL (Sandbox)**, puis cliquez sur **Continue**.
  4. Sélectionnez l'ID d'application que vous avez créé à l'étape précédente, puis cliquez sur **Continue**.
  5. Créez un fichier CSR en suivant les instructions figurant sur la page, puis cliquez sur **Continue**.
  6. Sélectionnez le fichier CSR que vous avez créé, puis cliquez sur **Continue**.
  7. Téléchargez et exécutez le fichier certificat. 

4. Créez un profil. 
  1. Sélectionnez **Provisioning profile: Development**.
  2. Cliquez sur le bouton d'ajout (+) pour créer un profil de développement. 
  3. Sélectionnez **iOS App Development**, puis cliquez sur **Continue**.
  4. Sélectionnez l'ID d'application que vous avez créé précédemment. 
  5. Sélectionnez **Developer Certificates: All**, puis cliquez sur **Continue**.
  5. Sélectionnez **All development devices (testing devices)**, puis cliquez sur **Continue**.
  6. Spécifiez un nom de profil, puis cliquez sur **Continue**.
  7. Téléchargez et exécutez le profil généré. 

5. Créez un fichier Public Key Cryptography Standards (PKCS) 12 et ajoutez-le au service {{site.data.keyword.mobilepushshort}}. 
  1. Ouvrez Keychain Access et sélectionnez **My Certificates**.
  2. Cliquez avec le bouton droit de la souris sur **Apple Development IOS Push Service: (bundleID)**, puis procédez à
l'exportation et à la sauvegarde, et entrez un mot de passe pour le fichier.

  3. Dans votre tableau de bord {{site.data.keyword.Bluemix_notm}}, ouvrez le service {{site.data.keyword.mobilepushshort}}. 
  4. Cliquez sur l'option **Configurer Push**.
  5. Dans la section Certificat Apple Push Notification, téléchargez le fichier PKCS 12 et entrez le mot de passe. 
  6. Dans Xcode, remplacez l'identificateur de bundle par celui que vous avez créé précédemment. 
  7. Exécutez l'application et accordez des droits pour le service Push Notifications. 

# Liens connexes 
{: #rellinks}

## Référence d'API 
{: #api}
* [Exemples d'API {{site.data.keyword.iotinsurance_short}}](https://iot4i-docs-api.mybluemix.net/dist/){:new_window}

## Liens connexes 
{: #general}
* [Documentation d'{{site.data.keyword.iot_full}}](https://new-console.ng.bluemix.net/docs/services/IoT/index.html)
* 
[Forum de
support des développeurs](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix])
* [Forum de support stackoverflow](http://stackoverflow.com/questions/tagged/ibm-bluemix)
