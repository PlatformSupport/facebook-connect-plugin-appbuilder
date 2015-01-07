# facebook-connect-plugin-appbuilder

This is the AppBuilder-compatible version of the Wizcorp Facebook Connect Plugin. The original version could be found at https://github.com/Wizcorp/phonegap-facebook-plugin.

## In order to use the plugin in your application build with Telerik AppBuilder:

* [Import it in your favorite AppBuilder client](http://docs.telerik.com/platform/appbuilder/creating-your-project/using-plugins/using-custom-plugins/add-custom-plugins).

* From the **Project Navigator** in the right navigate to **Plugins > Facebook-AB > plugin.xml**  and open it.

* Remove the two `<preference>` tags with names – `APP_ID` and `APP_NAME`.

* Locate the `$APP_ID` and `$APP_NAME` configurations for Android and iOS.

* Replace them with the App ID that you obtained from the Facebook Developers portal and its name.

* Add the APP ID in the `CFBundleURLSchemes` for iOS. It must look something like *fb1111111111111111* after the replacement with an actual App ID.

## How to configure your APP ID in Facebook for Android

In order to configure your app in the Facebook Portal for Android you need:

* **PackageName** - as it is entered in the Application Identifier of the AppBuilder project, for example com.mycompany.myappname.
* **ClassName** - the name of the main activity in the project, which you can see in the `AndroidManifest.xml` file. You can follow the steps outlined in this [article](http://docs.telerik.com/platform/appbuilder/configuring-your-project/edit-configuration) to open the AndroidManifest configuration file in AppBuilder. The activity tag describes the main activity in the project and by default its name is [MyPackageName].TelerikCallbackActivity, for example `com.mycompany.myappname.TelerikCallbackActivity`.
* **Key Hashes** - you can get the hash for the key used to sign your app in AppBuilder for Google Play or for Development by following these steps:
        Verify that you have the latest Java Development Kit installed on your machine.
        In AppBuilder, open the User Options. (In the title bar, click Welcome, User Name -> Options).
        Go to Mobile -> Android - > Certification Management.
        In the Cryptographic Identities panel select your Google Play cryptographic identity. If you do not have one, create it.
        Click Export to export the cryptographic identity, set a password for it, and store it on your local file system.
        Run a command prompt and the command below.

Note that you will need also installed the OpenSSL library. The creators of the plugin recommend that If you are generating this hash on Windows (specifically 64 bit versions) to use version 0.9.8e or 0.9.8d of OpenSSL for Windows and not 0.9.8k.
```
keytool -exportcert -alias "ALIAS" -keystore "path to the .p12 from AppBuilder" -storepass "password-here" -storetype PKCS12 | "path to openssl.exe" sha1 -binary | "path to openssl.exe" base64
```

Note that ALIAS should be replaced with the name of the .p12 file as exported from AppBuilder, for example, USER NAME, if the .p12 is exported as USER NAME.p12. After you have a release certificate for Google Play, you can follow the same procedure, to obtain a hash for the release ALIAS.

You will receive a key hash which should be entered in the FB app settings. This is the hash of the certificate used to sign the app which will be verified by FB in order to determine that the authorized app is making the request.

## How to configure your APP ID in Facebook for iOS

There are no additional configurations required for the app to work for iOS. In case your app requires a configuration for iOS you can read more about iOS configuration in the Facebook Developers portal [here](https://developers.facebook.com/quickstarts/286797954843521/?platform=ios). Please explore the Facebook [documentation page](https://developers.facebook.com/docs/apps/review) for app review and submission for more information too.

