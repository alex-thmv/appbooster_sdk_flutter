![Bintray](https://img.shields.io/bintray/v/appbooster/appbooster_android_sdk/experiments_sdk?color=dark%20green&style=flat-square)

# appbooster-sdk-android

Mobile framework for Appbooster platform.

## Installation

1. Add this to your package's pubspec.yaml file:
```
    dependencies:
      appbooster_sdk_flutter:
```

2. Now in your Dart code, you can use:
```
    import 'package:appbooster_sdk_flutter/appbooster_sdk_flutter.dart';
```

## Usage


### Initialization:

```
    await Appbooster.initialize(
      appId: "${YOUR_APP_ID}",
      sdkToken: "${YOUR_SDK_TOKEN}",
      deviceId: "${YOUR_DEVICE_ID}" // optional, UUID generated by default
      appsFlyerId: "${YOUR_APPS_FLYER_UID}" // optional
      amplitudeDeviceId: "${YOUR_AMPLITUDE_DEVICE_ID}" // optional, if Amplitude integration is needed
      defaults: {"${TEST_1_KEY}": "${TEST_1_DEFAULT_VALUE}", "${TEST_2_KEY}": "${TEST_2_DEFAULT_VALUE}"},
    );
```

After initialization all functionality will be available via singleton:

```
    Appbooster.instance()
```

### How to fetch known test values that associated with your device?

```
    Appbooster.instance().loadExperiments((List<String> experimentsKeys) {
        // Handle loaded experiments
    });
```

### How to get the value for a specific test?

```
    final value = Appbooster.instance().experiment("${TEST_KEY}");
```

In case of problems with no internet connection or another, the values obtained in the previous session will be used, or if they are missing, the default values specified during initialization will be used.

### How to get user tests for analytics?

```
    final value = Appbooster.instance().experiments;
    
    // or if you need additional details for experiments
    final value = Appbooster.instance().experimentsWithDetails;

```

### How to debug?

Before debug make sure that debug-mode for your App is turned-on on [settings page](https://platform.appbooster.com/ab/settings)

  ![](https://imgproxy.appbooster.com/9ACImnEbmsO822dynjTjcC_B8aXzbbpPQsOgop2PlBs//aHR0cHM6Ly9hcHBib29zdGVyLWNsb3VkLnMzLmV1LWNlbnRyYWwtMS5hbWF6b25hd3MuY29tLzk0N2M5NzdmLTAwY2EtNDA1Yi04OGQ4LTAzOTM4ZjY4OTAzYi5wbmc.png)

In debug mode you can see all actual tests and check how the user will see each option of the test.
To show the debug bottom sheet you just need to turn it on in your personal cabinet and call

```
    Appbooster.instance().showDebugLayer(
      context: context,
      valuesChangedCallback: (List<String> changedExperimentsKeys) {
        // Handle changed experiments
      },
    );
```

You can enable showing debug bottom sheet by performing shake motion on your device:

```
    Appbooster.instance().enableDebugOnShake(
      context: context,
      valuesChangedCallback: (List<String> changedExperimentsKeys) {
        // Handle changed experiments
      },
    );
```

or disable this behavior:

```
    Appbooster.instance().disableDebugOnShake();
```
