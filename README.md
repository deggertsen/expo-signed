# expo-signed

**A Plugin for Signing Android Builds on Expo Prebuild**

Effortlessly configure signing for Android builds in Expo projects during the prebuild process.

### How It Works

- **Step 1**: Updates the `gradle.properties` file to include signing configurations.
- **Step 2**: Modifies the `build.gradle` file to switch from debug signing to release signing.
- **Step 3**: Adds a `release` signing block to the `build.gradle` file if it doesn’t already exist.
- **Step 4**: Copies the keystore file to the `android > app` directory for signing during the build process.

---

### Resources

- [Expo Local App Production Guide](https://docs.expo.dev/guides/local-app-production/#android)
- [Continuous Native Generation in Expo](https://docs.expo.dev/workflow/continuous-native-generation/)
- [React Native Documentation: Generating an Upload Key](https://reactnative.dev/docs/signed-apk-android#generating-an-upload-key)

---

## Features

- **Automatic Configuration**: Updates `android > gradle.properties` to include the specified signing properties if they don’t already exist.
- **Signing Configuration**: Replaces `signingConfig signingConfigs.debug` with `signingConfig signingConfigs.release` under `android.buildTypes.release` in `android > app > build.gradle`.
- **Release Block Addition**: Adds the `release` block with the specified properties to `android.signingConfigs` in `android > app > build.gradle` if it doesn’t exist.
- **Keystore File Handling**: Copies the specified `.keystore` file (defined by `store_file.value`) from the `keystorePath` to the `android > app` folder.

---

## Prerequisites

Before using `expo-signed`, generate a private signing key and follow these steps:

1. **Generate a Key**:\
   Use `keytool` to create a private signing key. Follow the instructions provided in the [React Native documentation on signed APKs](https://reactnative.dev/docs/signed-apk-android#generating-an-upload-key).

2. **Place the Keystore File**:\
   Add the generated keystore file to your project directory.

---

## Installation

To install and configure the plugin:

### 1. Define the Keystore Location

- Place the `.keystore` file in your project, and set the folder path (`keystorePath`) and file name (`store_file.value`) in the configuration.

### 2. Update `app.json`

Add the plugin configuration to your `app.json` as follows:

```json
"plugins": [
    ...
    [
        "expo-signed",
        {
            "store_file": {
                "key": "MY_UPLOAD_STORE_FILE",
                "value": "my-upload-key.keystore"
            },
            "key_alias": {
                "key": "MY_UPLOAD_KEY_ALIAS",
                "value": "my-key-alias"
            },
            "store_password": {
                "key": "MY_UPLOAD_STORE_PASSWORD",
                "value": "************"
            },
            "key_password": {
                "key": "MY_UPLOAD_KEY_PASSWORD",
                "value": "************"
            },
            "keystorePath": "./src/assets"
        }
    ],
    ...
]
```

---

By following the above steps, you’ll be able to sign your Android builds seamlessly with `expo-signed`.