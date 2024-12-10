Traditionally APKs consist of a single universal APK file. However, Google play supports (Android Application Bundles) AAB files. 

An _Android App Bundle_ is a publishing format that includes all your app's compiled code and resources, and defers APK generation and signing to Google Play.

Google Play uses your app bundle to generate and serve optimized APKs for each device configuration, so only the code and resources that are needed for a specific device are downloaded to run your app. You no longer have to build, sign, and manage multiple APKs to optimize support for different devices, and users get smaller, more-optimized downloads.

[Build multiple APKs  |  Android Studio  |  Android Developers](https://developer.android.com/build/configure-apk-splits)

To configure your build for multiple APKs, add a [`splits`](https://developer.android.com/reference/tools/gradle-api/7.2/com/android/build/api/dsl/Splits) block to your module-level `build.gradle` file. Within the `splits` block, provide a `density` block that specifies how you want Gradle to generate per-density APKs or an `abi` block that specifies how you want Gradle to generate per-ABI APKs. You can provide both density and Android Binary Interface (ABI) (A variant for each CPU and instruction set combo) blocks, and the build system creates an APK for each density and ABI combination.

1. Split by ABI means that devices will only download the files required to run on the device nothing else
2. Split by density means that the device will only download the files optimized for their screen, saving space e.g MDPI, XHDPI etc

#### Install the split APKs

See [[Android Debug Bridge (ADB)#Install split APKs|ADB]]

##### Merge APKs

See [[APKEditor#Merge Split APKs|Merge]]