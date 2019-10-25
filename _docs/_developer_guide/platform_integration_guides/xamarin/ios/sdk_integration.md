---
nav_title: Initial SDK Setup
platform: Xamarin
subplatform: iOS
page_order: 0
---
# Initial SDK Setup

Installing the Braze SDK will provide you with basic analytics functionality as well as working in-app messages with which you can engage your users.

## Step 1: Get the Xamarin binding

A Xamarin binding is a way to use native libraries in Xamarin apps.  The implementation of a binding consists of building a C# interface to the library, and then using that interface in your application.

##### Nuget

The recommended integration method is to get the Braze SDK Bindings from the [Nuget.org][9] central repository. In the Visual Studio sidebar, right click `Packages` folder and click `Add Packages...`.  Search for 'Braze' and install the [`AppboyPlatformXamariniOSBinding`][11] package into your project.

## Step 2: Update your App Delegate and Declare Xamarin Usage

Within your `AppDelegate.cs` file, add the following snippet within your `FinishedLaunching` method:

>  Be sure to update `YOUR-API-KEY` with the correct value from your [App Settings][5] page.

```csharp
 Appboy.StartWithApiKey ("YOUR-API-KEY", UIApplication.SharedApplication, options);
 Appboy.SharedInstance.SdkFlavor = ABKSDKFlavor.Xamarin;
```

**Implementation Example**

See the `AppDelegate.cs` file in the [TestApp.XamariniOS][10] sample app.

## SDK Integration Complete

Braze should now be collecting data from your application and your basic integration should be complete. Please see the following sections in order to enable custom event tracking, push messaging, the news-feed and the complete suite of Braze features.

>  Our current public Xamarin binding for the iOS SDK does not connect to the iOS Facebook SDK (linking social data) and does not include sending the IDFA to Braze.


[2]: http://developer.xamarin.com/guides/ios/advanced_topics/binding_objective-c/
[4]: #add-api-calls
[5]: https://dashboard-01.braze.com/app_settings/app_settings/ "App Settings"
[9]: https://www.nuget.org/
[10]: https://github.com/Appboy/appboy-xamarin-bindings/tree/master/appboy-component/samples/ios-unified/TestApp.XamariniOS
[11]: https://www.nuget.org/packages/AppboyPlatformXamariniOSBinding/
