# Ussd plugin for Flutter

This plugin makes it possible to access Android's [sendUssdRequest](https://developer.android.com/reference/android/telephony/TelephonyManager.html#sendUssdRequest(java.lang.String,%20android.telephony.TelephonyManager.UssdResponseCallback,%20android.os.Handler)) method from a Flutter application.

## Installation

Add `ussd_service` as a dependency in your pubspec.yaml.

Make sure that your `AndroidManifext.xml` file includes the following permission:
```xml
<uses-permission android:name="android.permission.CALL_PHONE" />
```

### Usage

Before you use this plugin, you must:
- make sure that the user has authorized access to his phone calls, for example with the [permission_handler plugin](https://pub.dev/packages/permission_handler).
- retrieve the [SIM card subscription ID](https://developer.android.com/reference/android/telephony/SubscriptionInfo#getSubscriptionId()), for example with the [sim_service plugin](https://pub.dev/packages/sim_service).

You may then use the plugin:
``` dart
import 'package:ussd_service/ussd_service.dart';

makeMyRequest() async {
  int subscriptionId = 1; // sim card subscription ID
  String code = "*21#"; // ussd code payload
  try {
    String ussdResponseMessage = await UssdService.makeRequest(subscriptionId, code);
    print("succes! message: $ussdResponseMessage");
  } catch(e) {
    debugPrint("error! code: ${e.code} - message: ${e.message}");
  }
};

makeMyRequest();
```