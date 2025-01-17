# OpenID Connect configuration using Azure AD

**The configuration described below is for Azure public cloud only. Endpoints for sovereign Azure clouds (Azure Government, China Azure Cloud and Azure Germany) are separate.**

## 

1.	Sign up for an Azure account if you don’t already have one by going to this site: 
https://docs.microsoft.com/en-us/azure/active-directory/develop/quickstart-create-new-tenant

2.  Go to https://portal.azure.com/ and sign in.

3.	Register an app by following the instructions at https://docs.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app or by following the instructions below.

4.	Under Manage Azure Active Directory, click View.

![Image-Welcome to Azure](https://github.com/Esri/idp/blob/main/Documentation/OpenID/Images/Azure%20AD-Images/Image-Welcome%20to%20Azure.png)

5.	Click App registrations.

![Image-App registrations](https://github.com/Esri/idp/blob/main/Documentation/OpenID/Images/Azure%20AD-Images/Image-App%20registrations.png)

6.	Click New registration.

![Image-New registration](https://github.com/Esri/idp/blob/main/Documentation/OpenID/Images/Azure%20AD-Images/Image-New%20registration.png)

7.	Specify the app name. You will provide a redirect URI later.

![Image-Register an application](https://github.com/Esri/idp/blob/main/Documentation/OpenID/Images/Azure%20AD-Images/Image-Register%20an%20application.png)

8.	Click Register. This gives you the application (client) ID. You will have to come back to add a redirect URI that will be generated when OpenID Connect is configured in ArcGIS Online.

![Image-Application ID](https://github.com/Esri/idp/blob/main/Documentation/OpenID/Images/Azure%20AD-Images/Image-Application%20ID.png)

9.	Go to the Authentication tab and select Platform.

![Image-Authentication](https://github.com/Esri/idp/blob/main/Documentation/OpenID/Images/Azure%20AD-Images/Image-Authentication.png)

10.	Configure the platform. In this example, a web application is selected.

![Image-Configure Web](https://github.com/Esri/idp/blob/main/Documentation/OpenID/Images/Azure%20AD-Images/Image-Configure%20Web.png)

11.	Generate a secret by going to Certificates & secrets and clicking New client secret.

![Image-Certificates and secrets](https://github.com/Esri/idp/blob/main/Documentation/OpenID/Images/Azure%20AD-Images/Image-Certificates%20and%20secrets.png)

12.	Specify the description and expiry information.

![Image-Add a client secret](https://github.com/Esri/idp/blob/main/Documentation/OpenID/Images/Azure%20AD-Images/Image-Add%20a%20client%20secret.png)

13.	Browse to the well-known URL. 
    - The well-known URL is of the form https://login.microsoftonline.com/{tenant}/v2.0, where tenant value can be common, organizations, consumers, and so on, detailed [here](https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-protocols-oidc) depending on the type of account that is allowed to sign in to the app. 
    - In this case, use common, as the app will be used to allow both a personal Microsoft account and a work or school account from Azure AD, so the URL will look like this: https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration
Go to https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration.
    - The response will contain various values that are used for configuring OpenID Connect for online organization.
    - In a separate tab, sign in using your ArcGIS Online organization for which you want to configure OpenID Connect using Administrator credentials.

14.	Click Organization > Settings > Security > Logins > OpenID Connect login > Set up OpenID Connect login.

![Image-Security](https://github.com/Esri/idp/blob/main/Documentation/OpenID/Images/Azure%20AD-Images/Image-Security.png)

15.	Configure OpenID Connect properties from the well-known URL and the application client ID and secret created above, and click Save.

![Image-Edit OpenID Connect login](https://github.com/Esri/idp/blob/main/Documentation/OpenID/Images/Azure%20AD-Images/Image-Edit%20OpenID%20Connect%20login.png)

16.	This generates a login URI and a logout URI (if configured). Copy the login URI.

![Image-OpenID Connect login](https://github.com/Esri/idp/blob/main/Documentation/OpenID/Images/Azure%20AD-Images/Image-OpenID%20Connect%20login.png)

17.	Go to your Azure AD registered app that was created before. 
    - Go to the Overview tab on your registered app and click the link corresponding to  Redirect URIs: 1 web, 0 spa, 0 public client.
    
![Image-Redirect URIs](https://github.com/Esri/idp/blob/main/Documentation/OpenID/Images/Azure%20AD-Images/Image-Redirect%20URIs.png)

18.	Paste the login URI that was generated after configuring OpenID Connect.
    - Also, copy the last/previous logout URL that was generated (if the OpenID Connect logout endpoint was configured).
    - Click Save.
    - Configuration is complete.
    
![Image-Platform configurations](https://github.com/Esri/idp/blob/main/Documentation/OpenID/Images/Azure%20AD-Images/Image-Platform%20configurations.png)

19.	To test whether the Automatic join option was selected, sign out of your ArcGIS Online organization, and browse to your organization URL.

20.	Click Sign in. The Configured OpenID Connect sign in option is displayed.

21.	Click this OpenID Connect sign in option. Enter your Microsoft account or Azure AD credentials. A new user is created and signed in to your ArcGIS Online organization based on your Microsoft or Azure AD identity.

22.	To test whether the Upon invitation only option was configured, send an invitation to the user by clicking Organization > Members > Invite members. Upon receiving the invitation, click the OpenID Connect sign in option.


