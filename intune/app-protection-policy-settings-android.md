---
# required metadata

title: Android app protection policy settings
titlesuffix: Microsoft Intune
description: This topic describes the app protection policy settings for Android devices.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/26/2018
ms.topic: article
ms.prod:
ms.service: microsoft-intune
ms.technology:
ms.assetid: 9e9ef9f5-1215-4df1-b690-6b21a5a631f8

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: andcerat
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-azure
---
# Android app protection policy settings in Microsoft Intune
This article describes the app protection policy settings for Android devices. The policy settings that are described can be [configured](app-protection-policies.md) for an app protection policy on the **Settings** blade in the Azure portal.
There are two categories of policy settings: data relocation settings and access settings. In this article, the term *policy-managed apps* refers to apps that are configured with app protection policies.

##  Data relocation settings

| Setting | How to use | Default value(s) |
|------|------|------|
| **Prevent Android backups** | Choose **Yes** to prevent this app from backing up work or school data to the [Android Backup Service](https://developer.android.com/google/backup/index.html) Choose **No** to allow this app to back up work or school data.| Yes |
| **Allow app to transfer data to other apps** | Specify what apps can receive data from this app: <ul><li> **Policy managed apps**: Allow transfer only to other policy-managed apps.</li> <li>**All apps**: Allow transfer to any app. </li> <li>**None**: Do not allow data transfer to any app, including other policy-managed apps.</li></ul> <p>There are some exempt apps and services to which Intune may allow data transfer by default. In addition, you can create your own exemptions if you need to allow data to be transferred to an app that does not support Intune APP. See [Data transfer exemptions](#Data-transfer-exemptions) for more information.<p>This policy also impacts the behavior of web content. If this policy is set to **blocked**, the user will be unable to open http links to any browser, including the Managed Browser. Additionally, if this policy is set to **policy managed only**, then http links will only be able to open in the Managed Browser.<p>**Note:** Intune does not currently support the Android Instant Apps feature. Intune will block any data connection to or from the app.  See the Android Developer documentation for more information about [Android Instant Apps](https://developer.android.com/topic/instant-apps/index.html).</p>| All apps |
| **Allow app to receive data from other apps** | Specify what apps can transfer data to this app: <ul><li>**Policy managed apps**: Allow transfer only from other policy-managed apps.</li><li>**All apps**: Allow data transfer from any app.</li><li>**None**: Do not allow data transfer from any app, including other policy-managed apps. </li></ul> <p>There are some exempts apps and services from which Intune may allow data transfer. See  [Data transfer exemptions](#Data-transfer-exemptions) for a full list of apps and services. | All apps |
| **Prevent "Save As"** | Choose **Yes** to disable the use of the Save As option in this app. Choose **No** if you want to allow the use of Save As. **Note:** This setting is supported for Microsoft Excel, OneNote, PowerPoint, and Word. It may also be supported by 3rd party and LOB apps. <p>**Select which storage services corporate data can be saved to** <br>Users are able to save to the selected services (OneDrive for Business, SharePoint, and Local Storage). All other services will be blocked.</p> | No<p>&nbsp;</p><p>&nbsp;</p>0 selected |
| **Restrict cut, copy, and paste with other apps** | Specify when cut, copy, and paste actions can be used with this app. Choose from: <ul><li>**Blocked**:  Do not allow cut, copy, and paste actions between this app and any other app.</li><li>**Policy managed apps**: Allow cut, copy, and paste actions between this app and other policy-managed apps.</li><li>**Policy managed with paste in**: Allow cut or copy between this app and other policy-managed apps. Allow data from any app to be pasted into this app.</li><li>**Any app**: No restrictions for cut, copy, and paste to and from this app. | Any app |
|**Restrict web content to display in the Managed Browser** | Choose **Yes** to enforce web links in the app to be opened in the Managed Browser app. <br><br> For devices not enrolled in Intune, the web links in policy-managed apps can open only in the Managed Browser app. <br><br> If you are using Intune to manage your devices, see [Manage Internet access using managed browser policies with Microsoft Intune](app-configuration-managed-browser.md).<br><br> The Microsoft Edge browser for mobile devices (iOS and Android) supports Intune app protection policies. Users who sign in with their corporate Azure AD accounts in the Edge browser application will be protected by Intune. The Edge browser integrates the MAM SDK and supports all of its data protection policies, with the exception of preventing:<ul><li>**Save-as**: The Edge browser does not allow a user to add direct, in-app connections to cloud storage providers (such as OneDrive).</li><li>**Contact sync**: The Edge browser does not save to native contact lists.</li></ul> | No |
| **Encrypt app data** | Choose **Yes** to enable encryption of work or school data in this app. Intune uses an OpenSSL, 128-bit AES encryption scheme along with the Android Keystore system to securely encrypt app data. Data is encrypted synchronously during file I/O tasks. Content on the device storage is always encrypted. <br><br> The encryption method is **not** FIPS 140-2 certified.  | Yes |
| **Disable app encryption when device encryption is enabled** | Choose **Yes** to disable app encryption for internal app storage when device encryption is detected on an enrolled device. <br><br>**Note:** Intune can only detect device enrollment with Intune MDM. External app storage will still be encrypted to ensure data cannot be accessed by unmanaged applications. | Yes |
| **Disable contact sync** | Choose **Yes** to prevent the app from saving data to the native Contacts app on the device. If you choose **No**, the app can save data to the native Contacts app on the device. <br><br>When you perform a selective wipe to remove work, or school data from the app, contacts synced directly from the app to the native Contacts app are removed. Any contacts synced from the native address book to another external source cannot be wiped. Currently this applies only to the Microsoft Outlook app. | No |
| **Disable printing** | Choose **Yes** to prevent the app from printing work or school data. | No |

  >[!NOTE]
  >The encryption method for the **Encrypt app data** setting is **not** FIPS 140-2 certified.

  ## Data transfer exemptions

  There are some exempt apps and platform services that Intune app protection policy may allow data transfer to and from. For example, all Intune-managed apps on Android must be able to transfer data to and from the Google Text-to-speech, so that text from your mobile device screen can be read aloud. This list is subject to change and reflects the services and apps considered useful for secure productivity.

  ### Full exemptions

  These apps and services are fully allowed for data transfer to and from Intune-managed apps.

  |App/service name | Description |
  | ------ | ---- |
  | com.android.phone | Native phone app
  | com.android.vending | Google Play Store |
  | com.android.documentsui | Android Document Picker|
  | com.google.android.webview | [WebView](https://developer.android.com/reference/android/webkit/WebView.html), which is necessary for many apps including Outlook. |
  | com.android.webview |[Webview](https://developer.android.com/reference/android/webkit/WebView.html), which is necessary for many apps including Outlook.|
  | com.google.android.tts | Google Text-to-speech |
  | com.android.providers.settings | Android system settings |
  | com.android.settings | Android system settings |
  | com.azure.authenticator | Azure Authenticator app, which is required for successful authentication in many scenarios. |
  | com.microsoft.windowsintune.companyportal | Intune Company Portal|

  ### Conditional exemptions
  These apps and services are only allowed for data transfer to and from Intune-managed apps under certain conditions.

  |App/service name | Description | Exemption condition|
  | ------ | ---- | --- |
  | com.android.chrome | Google Chrome Browser | Chrome is used for some WebView components on Android 7.0+ and is never hidden from view. Data flow to and from the app, however, is always restricted.  |
  | com.skype.raider | Skype | The Skype app is allowed only for certain actions that result in a phone call. |
  | com.android.providers.media | Android media content provider | The media content provider allowed only for the ringtone selection action. |
  | com.google.android.gms; com.google.android.gsf | Google Play Services packages | These packages are allowed for Google Cloud Messaging actions, such as push notifications. |

For more information, see [Data transfer policy exceptions for apps](app-protection-policies-exception.md).

##  Access settings

| Setting | How to use |  
|------|------| 
| **Require PIN for access** | Select **Yes** to require a PIN to use this app. The user is prompted to set up this PIN the first time they run the app in a work or school context. <br><br> Default value = **Yes**.<br><br> Configure the following settings for PIN strength: <br> <ul><li>**Select Type**: Set a requirement for either numeric or passcode type PINs before accessing an app that has app protection policies applied. Numeric requirements involve only numbers, while a passcode can be defined with at least 1 alphabetical letter **or** at least 1 special character. <br><br> Default value = **Numeric**<br><br> ***Note:** Special characters allowed include the special characters and symbols on the Android English language keyboard.*</li></ul>  <ul><li>**Number of attempts before PIN reset**: Specify the number of tries the user has to successfully enter their PIN before they must reset it. <br><br> Default value = **5** </li> <br> <li> **Allow simple PIN**: Select **Yes** to allow users to use simple PIN sequences like *1234*, *1111*, *abcd* or *aaaa*. Select **No** to prevent them from using simple sequences. <br><br>Default value = **Yes** <br><br>***Note**: If Passcode type PIN is configured, and Allow simple PIN is set to Yes, the user needs at least one letter **or** at least one special character in their PIN. If Passcode type PIN is configured, and Allow simple PIN is set to No, the user needs at least one number **and** one letter **and** at least one special character in their PIN.* </li> <br> <li>  **PIN length**: Specify the minimum number of digits in a PIN sequence. <br><br>Default value = **4** </li> <br> <li> **Allow fingerprint instead of PIN (Android 6.0+)**: Select **Yes** to allow the user to use [fingerprint authentication](https://developer.android.com/about/versions/marshmallow/android-6.0.html#fingerprint-authentication) instead of a PIN for app access. <br><br>Default value = **Yes** <br><br>***Note**: This feature supports generic controls for biometric on Android devices. OEM-specific biometric settings, like* Samsung Pass, *are not supported.* <br><br>On Android, you can let the user prove their identity by using [Android fingerprint authentication](https://developer.android.com/about/versions/marshmallow/android-6.0.html#fingerprint-authentication) instead of a PIN. When the user tries to use this app with their work or school account, they are prompted to provide their fingerprint identity instead of entering a PIN. <br><br> Android work profiles require registering a separate fingerprint for the **Allow fingerprint instead of PIN** policy to be enforced. This policy takes effect only for policy-managed apps installed in the Android work profile. The separate fingerprint must be registered with the device after the Android work profile is created by enrolling in the Company Portal. For more information about work profile fingerprints using Android work profiles, see [Lock your work profile](https://support.google.com/work/android/answer/7029958). <!--INSERT --> <br><br>  <ul><ul><li>**Require additional PIN entry after biometric timeout**: Select **Yes** to require use of a PIN instead of a fingerprint after the configured number of minutes have elapsed. Select **No** if a fingerprint is required for all prompts. <br><br> Default value = **No**. <br><br><li>**Inactivity required for PIN prompt (minutes)**: Set the number of minutes of inactivity after which a user is shown a PIN prompt instead of a fingerprint prompt, when access requirements are rechecked. How often policy requirements are rechecked depends on the value of the **Timeout** setting for the **Recheck the access requirements after (minutes)** setting. <br><br>***Example:** When this setting is turned on with the default configuration of 60 minutes, and the recheck Timeout value is set to 30 minutes, the behavior is as follows. A user accesses an Intune-managed app after 31 minutes of inactivity. The user is prompted for their fingerprint to get access. If the user waited for 61 minutes of inactivity before accessing the app, they would find that they are prompted for a PIN instead of a fingerprint.*<br><br>***Note:** Configure this value to be greater than the recheck timeout value. If this value is less than the recheck timeout value, the user does not receive prompts for fingerprints, only for a PIN.* <br><br> Default value = **60**. </li></ul>| 
| **Require corporate credentials for access** | Choose **Yes** to require the user to sign in with their work or school account instead of entering a PIN for app access. When set to **Yes**, and PIN or biometric prompts are turned on, both corporate credentials and either the PIN or biometric prompts will be shown. <br><br>Default value = **No** |
| **Block managed apps from running on jailbroken or rooted devices** |Choose **Yes** to prevent this app from running on jailbroken or rooted devices. The user can continue to use this app for personal tasks, but must use a different device to access work or school data in this app. <br><br>Default value = **Yes** |
| **Recheck the access requirements after (minutes)** | Configure the following settings: <ul><li>**Timeout**: This is the number of minutes before the access requirements (defined earlier in the policy) are rechecked. For example, an admin turns on PIN and Blocks rooted devices in the policy, a user opens an Intune-managed app, must enter a PIN, and must be using the app on a non-rooted device. When using this setting, the user would not have to enter a PIN or undergo another root-detection check on any Intune-managed app for a period of time equal to the configured value.  <br><br>This policy setting format supports a positive whole number. <br><br> Default value = **30 minutes** <br><br> ***Note:** On Android, the PIN is shared with all Intune-managed apps. The PIN timer is reset once the app leaves the foreground on the device. The user won't have to enter a PIN on any Intune-managed app that shares its PIN for the duration of the timeout defined in this setting.* <br><br></li><li>**Offline grace period**: This is the number of minutes that MAM apps can run offline. Specify the time (in minutes) before the access requirements for the app are rechecked. After this period expires, the app requires user authentication to Azure Active Directory (Azure AD) so that the app can continue to run. <br><br>This policy setting format supports a positive whole number. <br><br>Default value = **720** minutes (12 hours)</li></ul>|
| **Offline interval before app data is wiped (days)** | After this many days (defined by the admin) of running offline, the app requires the user to connect to the network and reauthenticate. If the user successfully authenticates, they can continue to access their data and the offline interval will reset. If the user fails to authenticate, the app performs a selective wipe of the users account and data. For more information about what data is removed with a selective wipe, see [How to wipe only corporate data from Intune-managed apps](https://docs.microsoft.com/intune/apps-selective-wipe). <br><br>This policy setting format supports a positive whole number. <br><br>Default value = **90 days** |
| **Block screen capture and Android Assistant (Android 6.0+)** | Select **Yes** to block screen capture and the **Android Assistant** capabilities of the device when using this app. Choosing **Yes** will also blur the App-switcher preview image when using this app with a work or school account. <br><br>Default value = **No** |
| **Disable app PIN when device PIN is managed** | Select **Yes** to disable the app PIN when a device lock is detected on an enrolled device. <br><br>***Note:** Intune cannot detect device enrollment with a third-party EMM solution on Android.* <br><br>Default value = **No** |
| **Require minimum Android operating system** | Select **Yes** to require a minimum Android operating system to use this app. The user will be blocked from access if the Android version on the device doesn't meet the requirement. <br><br>This policy setting format supports either major.minor, major.minor.build, major.minor.build.revision. <br><br>Default value = **No** |
| **Require minimum Android operating system (Warning only)** | Select **Yes** to require a minimum Android operating system to use this app. The user will see a notification if the Android version on the device does not meet the requirement. This notification can be dismissed.<br><br> This policy setting format supports either major.minor, major.minor.build, major.minor.build.revision. <br><br>Default value = **No** |
| **Require minimum app version** | Select **Yes** to require a minimum app version to use the app. The user will be blocked from access if the app version on the device does not meet the requirement.<br><br>As apps often have distinct versioning schemes between them, create a policy with one minimum app version targeting one app (for example, *Outlook version policy*). <br><br> This policy setting format supports either major.minor, major.minor.build, major.minor.build.revision. <br><br>Default value = **No** |
| **Require minimum app version (Warning only)** | Select **Yes** to recommend a minimum app version to use this app. The user will see a notification if the app version on the device does not meet the requirement. This notification can be dismissed.<br><br>As apps often have distinct versioning schemes between them, create a policy with one minimum app version targeting one app (for example, *Outlook version policy*). <br><br> This policy setting format supports either major.minor, major.minor.build, major.minor.build.revision. <br><br>Default value = **No** |
| **Require Minimum Android Patch Version** | Select **Yes** to require a minimum Android security patch released by Google. The user will be blocked from access if the Android security patch on the device does not meet the requirement.<br><br> This policy setting format supports the date format of *YYYY-MM-DD*.  <br><br>Default value = **No** |
| **Require Minimum Android Patch Version (Warning Only)** | Select **Yes** to require a minimum Android security patch released by Google. The user will see a notification if the Android security patch on the device does not meet the requirement. This notification can be dismissed.<br><br> This policy setting format supports the date format of *YYYY-MM-DD*.  <br><br>Default value = **No**|

> [!NOTE]
> To learn more about how multiple Intune app protection settings configured in the Access section to the same set of apps and users work on Android, see [Intune MAM frequently asked questions](mam-faq.md) and [Selectively wipe data using app protection policy access actions in Intune](app-protection-policies-access-actions.md).
