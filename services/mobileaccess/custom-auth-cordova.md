---

copyright:
  years: 2015, 2016

---

# Configuring custom authentication for your {{site.data.keyword.amashort}} Cordova app
{: #custom-cordova}

Last updated: 23 August 2016
{: .last-updated}


Configure your Cordova application that is using custom authentication to use the {{site.data.keyword.amafull}} client SDK and connect your application to {{site.data.keyword.Bluemix}}.


## Before you begin
{: #before-you-begin}
You must have a resource that is protected by an instance of the {{site.data.keyword.amashort}} service that is configured to use a custom identity provider.  Your mobile app also must be instrumented with the {{site.data.keyword.amashort}} client SDK.  For more information, see the following information:
 * [Getting started with {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)
 * [Setting up Cordova SDK](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html)
 * [Using a custom identity provider](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [Creating a custom identity provider](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [Configuring {{site.data.keyword.amashort}} for custom authentication](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)

## Initializing the {{site.data.keyword.amashort}} client SDK
{: #custom-cordova-sdk}
Initialize the SDK by passing applicationGUID and applicationRoute parameters.

1. Get your application parameter values. Open your app in the {{site.data.keyword.Bluemix_notm}} dashboard. Click **Mobile Options**. The **Route** (`applicationRoute`) and **App GUID** (`applicationGUID`) values are displayed.
1. Initialize the client SDK.

	```JavaScript
	 BMSClient.initialize("applicationRoute", "applicationGUID");

	```
 * Replace `applicationRoute` and `applicationGUID` with the **Route** and **AppGuid** values. These values can be find by clicking the **Mobile Options** button within your {{site.data.keyword.Bluemix_notm}} application on the {{site.data.keyword.Bluemix_notm}} dashboard.
	
 
 
## Initializing the {{site.data.keyword.amashort}} AuthorizationManager
 {: #custom-cordova-MCAAM}
Initialize the `MCAAuthorizationManager` by passing the  {{site.data.keyword.amashort}} service `tenantId` parameter. You can find this value by clicking the **Show Credentials** button on the {{site.data.keyword.amashort}} service tile.

```JavaScript
MFPAuthorizationManager.initialize("tenantId");
        
```

## Authentication listener interface
{: #custom-cordva-auth}

The {{site.data.keyword.amashort}} client SDK provides an authentication listener interface to implement a custom authentication flow. You must add the following methods that are called in different phases of an authentication process.

```JavaScript
var customAuthenticationListener = {
	onAuthenticationChallengeReceived: function(authenticationContext, challenge) {...},
	onAuthenticationSuccess: function(info){...},
	onAuthenticationFailure: function(info){...}
}
```

Each method handles a different phase of an authentication process.

### onAuthenticationChallengeReceived method
{: #onAuthenticationChallengeReceived}
This method is called when a custom authentication challenge is received from {{site.data.keyword.amashort}} service.
```JavaScript
onAuthenticationChallengeReceived: function(authenticationContext, challenge) {...}
```

#### Arguments
{: #onAuthenticationChallengeReceived-args}
* `authenticationContext`: Provided by {{site.data.keyword.amashort}} client SDK so that developer can report back authentication challenge answers or failure during credentials collection, such as the user cancelling the authentication request.
* `challenge`: A JSON object that contains a custom authentication challenge, as returned by a custom identity provider.

Calling the `onAuthenticationChallengeReceived` method the {{site.data.keyword.amashort}} client SDK delegates control to developer. The {{site.data.keyword.amashort}} waits for credentials. The developer must collect credentials and report them back to the {{site.data.keyword.amashort}} client SDK by using one of the following  `authContext` interface methods.

```JavaScript
onAuthenticationSuccess: function(info){...}
```

This method is called after a successful authentication. The arguments include an optional JSON object that contains extended information about the authentication success.

```JavaScript
onAuthenticationFailure: function(info){...}
```

This method is called after an authentication failure. The arguments include an optional JSON object that contains extended information about the authentication failure.

## authenticationContext
{: #custom-cordova-authcontext}

The `authenticationContext` value is supplied as an argument to the `onAuthenticationChallengeReceived` method of a custom authentication listener. The developer must collect credentials and use the `authenticationContext` methods to either return credentials to the {{site.data.keyword.amashort}} client SDK or report a failure. Use one of the following methods:

```JavaScript
authenticationContext.submitAuthenticationChallengeAnswer(challengeAnswer);

authenticationContext.submitAuthenticationFailure(info);
```

## Sample implementation of a custom authentication listener
{: #custom-cordova-authlisten-sample}

This authentication listener sample is designed to work with a custom identity provider. You can download the custom identity provider from [this Github repository](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample).

```JavaScript
var customAuthenticationListener = {
	onAuthenticationChallengeReceived: function(authenticationContext, challenge) {
		console.log("onAuthenticationChallengeReceived :: ", challenge);

		// In this sample the authentication listener immediatelly returns a hardcoded
		// set of credentials. In a real life scenario this is where developer would
		// show a login screen, collect credentials and invoke
		// authenticationContext.submitAuthenticationChallengeAnswer() API

		var challengeResponse = {
			username: "john.lennon",
			password: "12345"
		}

		authenticationContext.submitAuthenticationChallengeAnswer(challengeResponse);

		// In case there was a failure collecting credentials you need to report
		// it back to the authenticationContext. Otherwise Mobile Client
		// Access client SDK will remain in a waiting-for-credentials state
		// forever

	},

	onAuthenticationSuccess: function(info){
		console.log("onAuthenticationSuccess :: ", info);
	},

	onAuthenticationFailure: function(info){
		console.log("onAuthenticationFailure :: ", info);
	}
}
```

## Registering a custom authentication listener
{: #custom-cordova-authreg}

After you create a custom authentication listener, register it with `BMSClient` before you can start using it. Add the following code to your application.  Call this code before you send any requests to your protected resources.

```Java
BMSClient.registerAuthenticationListener(realmName, customAuthenticationListener);
```
 Use *realmName* that you specified in the {{site.data.keyword.amashort}} dashboard.


## Testing the authentication
{: #custom-cordova-test}
After the client SDK is initialized and a custom AuthenticationListener is registered, you can start making requests to your mobile back-end application.

### Before you begin
{: #custom-cordova-testing-before}
You must have an application that was created with the {{site.data.keyword.mobilefirstbp}} boilerplate and have a resource that is protected by {{site.data.keyword.amashort}} at the `/protected` endpoint.


1. Send a request to protected endpoint of your mobile back-end application in your browser by opening `{applicationRoute}/protected`, for example `http://my-mobile-backend.mybluemix.net/protected`.
 The `/protected` endpoint of a mobile back-end application that is created with the {{site.data.keyword.mobilefirstbp}} boilerplate is protected with {{site.data.keyword.amashort}}. The endpoint can  be accessed by only mobile applications that are instrumented with the {{site.data.keyword.amashort}} client SDK. As a result, an `Unauthorized` message displays in your browser.

1. Use your Cordova application to make request to the same endpoint. Add the following code after you initialize `BMSClient` and register your custom AuthenticationListener.

	```JavaScript
	var success = function(data){
    	console.log("success", data);
    }
	var failure = function(error)
    	{console.log("failure", error);
    }
	var request = new MFPRequest("/protected", MFPRequest.GET);
	request.send(success, failure);
	```

1. 	When your request succeeds, the following output is in the LogCat or Xcode console:

	![image](images/android-custom-login-success.png)

	![image](images/ios-custom-login-success.png)
