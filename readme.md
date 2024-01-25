## MtAdmob plugin for Xamarin

With this Plugin you can add a Google Admob Ads inside your Xamarin Android and iOS Projects with a single line!!!
This plugin supports: Banners, Interstitial, Rewarded Videos and Rewearded Interstitials (from version 1.9)

### PLEASE READ
From version 2.1.0, I've added support for the consent required by Google for all the final users living in Europe.
This support for UMP is only available in the licensed version of the plugin.
Without the license, the plugin will continue to work as usual with all the other features normally available.
This will allow me to continue supporting the development of the plugin.
You can buy the license at https://hightouchinnovation.com/XMTAdmob
If you are a charity or your app is used to support a good cause, contact me and I'll evaluate it to send you a free license.

### CRYPTOGRAPHY
This plugin uses a cryptographic algorithm to handle the license.

### Please, support my work
If you prefer to not buy a license, if possible, please, support my work with a few coffees or even better with a Membership!
You can do it here: [Buy Me A Coffee](https://www.buymeacoffee.com/xamarinexpert)
Your help allows me to continue to spend time on this project and continue to maintain and update it with new features and to be ready for the new Google SDK : [Google SDK Migration](https://developers.google.com/admob/android/migration).

### DISCLAIMER OF LIABILITY

By using MAUIMtAdmob (the "Plugin"), you agree that:

1. The Plugin is provided "as is" without any warranties or guarantees of any kind, either expressed or implied.
2. I shall not be responsible or liable for any direct, indirect, incidental, special, or consequential damages arising out of the use or inability to use the Plugin.
3. I do not warrant that the Plugin will meet your specific requirements or operate without interruption.

You acknowledge that the use of the Plugin is at your own risk. The author of the plugin disclaims all liability for any damage to your computer system or loss of data that results from the use of the Plugin.

This disclaimer of liability is a fundamental part of the agreement between you and the author of the plugin. You agree that the limitations and exclusions of liability set forth in this disclaimer are reasonable and fair.

If you do not agree to these terms, do not use the Plugin.

### Commercial support

If you need faster support with this plugin, custom changes or in general with your Xamarin or MAUI project, contact me at hightouchinnovation@gmail.com to discuss it further.

## Current Status (Version 2.1.0)

|                       | **Android** | **iOS** | **Windows** | **Mac** |
|-----------------------|:-------------:|:---------:|:---------:|:---------:|
| Banner                |     :heavy_check_mark:     |   :heavy_check_mark:      |    :x:  |    :x:  |
| Interstitial          |     :heavy_check_mark:     |  :heavy_check_mark:       |    :x:  |    :x:  |
| Rewarded              |    :heavy_check_mark:    |    :heavy_check_mark:     |    :x:  |    :x:  |
| Rewarded Interstitial |   :heavy_check_mark:    |    :x:*  |    :x:  |    :x:  |

*They are implemented but currently, they are not working. Probably something in the Admob SDK. I'm investigating it.

## Methods
| **Banner** | **Interstitial**     | **Rewarded**     | **Rewarded Interstitial**  |
|:----------:|--------------------|----------------|--------------------------|
| LoadAd     | LoadInterstitial     | LoadRewarded     | LoadRewardedInterstitial     |
|            | ShowInterstitial     | ShowRewarded     | ShowRewardedInterstitial     |
|            | IsInterstitialLoaded | IsRewardedLoaded | IsRewardedInterstitialLoaded |


## Events
| **Banner**      | **Interstitial**           | **Rewarded**         | **Rewarded Interstitial** |
|-----------------|----------------------------|----------------------|---------------------------|
| AdsLoaded       | OnInterstitialLoaded       | OnRewardedLoaded     | OnRewardedLoaded          |
| AdsFailedToLoad | OnInterstitialFailedToLoad | OnRewardedFailedToLoad| OnRewardedFailedToLoad|
| AdsImpression   | OnInterstitialImpression   | OnRewardedImpression | OnRewardedImpression |
| AdsClicked      | OnInterstitialOpened	   | OnRewardedOpened	  | OnRewardedOpened	  |
| AdsOpened		  | OnInterstitialFailedToShow | OnRewardedFailedToShow| OnRewardedFailedToShow|
| AdsClosed       | OnInterstitialClosed	   | OnRewardedClosed	  | OnRewardedClosed	  |
| AdsSwiped 	  | OnInterstitialClicked*     | OnRewardedClicked*   | OnRewardedClicked*|
|  				  | 						   | OnUserEarnedReward   | OnUserEarnedReward|

*Only supported on iOS

### IMPORTANT

#### To allow a smooth toward MAUI, Version 1.9 contains few breaking changes, several fixes and am improved support for Banner. It's not complicated to update your code and it's worth it.

### INITIALIZATION

From your platform code, from version 2.1.0, you need to call:
CrossMTAdmob.Current.Init(this,...);

If you don't you'll get an error!


#### Android
You need to add your Admob APPLICATION_ID to your AppManifest:

```xml
<meta-data android:name="com.google.android.gms.ads.APPLICATION_ID" android:value="YOUR APPLICATION ID" />
```

### iOS
You need to add GADApplicationIdentifier to your Info.plist:
  Edit your info.plist adding these Keys:
  ```xml
  <key>GADApplicationIdentifier</key>
  <string>YOUR APPLICATION ID</string>
  <key>GADIsAdManagerApp</key>
  <true/>
  ```
* If you don't do this, your iOS app will crash


### BANNER

To add a Banner on a page you have two options:

#### XAML

```csharp
<controls:MTAdView x:Name="myAds"></controls:MTAdView>
```

remember to add this line in your XAML:
```
xmlns:controls="clr-namespace:MarcTron.Plugin.Controls;assembly=Plugin.MtAdmob"
```

#### CODE
```
MTAdView ads = new MTAdView();
```

Now you can add the control to your layout.

### IMPORTANT

To test the banner during the development google uses two Banner Id, one for Android and the other for iOS. Use them then remember to replace them with your own IDs:
```
Android: ca-app-pub-3940256099942544/6300978111
iOS: ca-app-pub-3940256099942544/2934735716
```

**If the Banners don't appear in your app, probably it's a size problem. To solve it, add this style to your app.xaml:**
```xml
<Style TargetType="controls:MTAdView">
    <Setter Property="HeightRequest">
        <Setter.Value>
            <x:OnIdiom Phone="50" Tablet="90"></x:OnIdiom>
        </Setter.Value>
    </Setter>
</Style>
```

### PROPERTIES

For each AdView if you want, you can set this property:
AdsId: To add the id of your ads
AdSize: To choose the size of your banners (from version 1.9)
AutoSize: If true, the plugin will update the banner height according to the ads loaded (from version 1.9)

**From the 16th ofJanuary, Google made it mandatory to use Certified CMP! You ca implement your own or you can use the licensed version of the plugin, that implements the Google UMP to handle the Consent for the European users.**

### GLOBAL PROPERTIES

AdsId: To add the id of your ads

PersonalizedAds: You can set it to False if you want to use generic ads (for GDPR...) (It works only for Android Banners, for the others, you must ask for consent)

**From the 16th ofJanuary, Google made it mandatory to use Certified CMP! You ca implement your own or you can use the licensed version of the plugin, that implements the Google UMP to handle the Consent for the European users.**

TestDevices: You can add here the ID of your test devices

UseRestrictedDataProcessing: For compliance with the CCPA

You can use Global Properties in this way:
CrossMTAdmob.Current.UserPersonalizedAds = true;


### INTERSTITIAL

You can show an interstitial with a single line of code:

```csharp
CrossMTAdmob.Current.ShowInterstitial();
```
To Load an interstitial you can use this line:

```csharp 
CrossMTAdmob.Current.LoadInterstitial("xx-xxx-xxx-xxxxxxxxxxxxxxxxx/xxxxxxxxxx");
```

### REWARDED VIDEO

You can show a Rewarded video with a single line of code:
```csharp
CrossMTAdmob.Current.ShowRewarded();
```
To Load a Rewarded Video you can use this line:
```csharp
CrossMTAdmob.Current.LoadRewarded("xx-xxx-xxx-xxxxxxxxxxxxxxxxx/xxxxxxxxxx");
```

### REWARD INTERSTITIAL (From Version 1.9)

You can show a Rewarded video with a single line of code:
```csharp
CrossMTAdmob.Current.ShowRewardInterstitial();
```
To Load a Rewarded Video you can use this line:
```csharp
CrossMTAdmob.Current.LoadRewardInterstitial("xx-xxx-xxx-xxxxxxxxxxxxxxxxx/xxxxxxxxxx");
```

### IMPORTANT

Remember to include the MTAdmob library with this code (usually it's added automatically):
```
using MarcTron.Plugin;
```


### IMPORTANT FOR ANDROID:

Before loading ads, you need to call MobileAds.initialize() on OnCreate: 

```csharp
protected override void OnCreate(Bundle savedInstanceState)
        {
            TabLayoutResource = Resource.Layout.Tabbar;
            ToolbarResource = Resource.Layout.Toolbar;

            base.OnCreate(savedInstanceState);            
            MobileAds.Initialize(ApplicationContext);
            Xamarin.Forms.Forms.Init(this, savedInstanceState); 
            LoadApplication(new App());
        }
```
Remember to add this to your AppManifest:
```xml
<!-- Sample AdMob App ID: ca-app-pub-3940256099942544~3347511713 -->
<meta-data android:name="com.google.android.gms.ads.APPLICATION_ID"
           android:value="ca-app-pub-xxxxxxxxxxxxxxxx~yyyyyyyyyy"/>
```

### IMPORTANT FOR IOS:

  In case the plugin doesn't install automatically the nuget package:
  
  **Xamarin.Google.iOS.MobileAds**
  
  you need to add it manually.


  That's it. Cannot be easier than that :)


  ### VIDEO
  [Get Filthy Rich by Monetizing Your Xamarin.Forms App with AdMob - Gerald Versluis (Youtube)](https://www.youtube.com/watch?v=Bka0T3806qo&ab_channel=GeraldVersluis)


  ### LINKS
  To buy the license visit https://hightouchinnovation.com/XMTAdmob

  Available on Nuget: https://www.nuget.org/packages/MarcTron.Admob

  Tutorial: https://www.xamarinexpert.it/admob-made-easy/

  Guide: https://hightouchinnovation.com/XMTAdmobGuide

  To report any issue: https://github.com/marcojak/MTAdmob/issues
 
