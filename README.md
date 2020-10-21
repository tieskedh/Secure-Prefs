[ ![Download](https://api.bintray.com/packages/atizik/maven/SecurePrefs/images/download.svg) ](https://bintray.com/atizik/maven/SecurePrefs/_latestVersion)
# SecurePrefs: Encrypted Storage for Kotlin Multiplatform




**SecurePrefs** is an open-source library providing encrypted key-value storage.

It can be integrated seamlessly in Kotlin projects built with **Kotlin Multiplatform**, **Kotlin/Native**, and **Kotlin Android** plugins.

**SecurePrefs** allows storing key-value data in common code modules without any additional boilerplate code.

Supported platforms:
- Android (API `>=` 21)
- iOS (`ios_arm64` and `ios_x64` targets)

## Download
To use this library in your project, add Netguru and Binryprefs maven urls to the repositories block:
```groovy
repositories {
    maven { url "https://jitpack.io" }
}
```

Then add following dependencies to the common module build.gradle:
```groovy
    sourceSets {
        commonMain {
            dependencies {
                implementation 'com.icecreamhappens.secureprefs:common:0.4.0'     
            }
        }
    }
```

Remember to enable `GRADLE_METADATA` in `settings.gradle`:
```groovy
enableFeaturePreview('GRADLE_METADATA')
```
## Usage
Just start with creating an instance of `SecurePrefs` class somewhere in your common module and enjoy! It's as simple as that.
You don't have to initialize it by yourself nor to pass Android `Context`. Everything is done automatically.
```kotlin
val storage = SecurePrefs(name = "my_secret_storage")
```
The `name` parameter is optional. You can omit it if you want to use default storage.
`SecurePrefs` allows you to store and persist multiple data types:
- String
- Int
- Long
- Float
- Double
- Boolean 

If you want to store something, just call:
```kotlin
storage.putString(key = "someKey", value = "value")
```

If you want to get stored value - use:
```kotlin
storage.getString(key = "someKey", defaultValue = "default")
```

All `get()` functions will return `defaultValue` parameter if storage doesn't contain selected `key`.

You can get all keys stored in `SecurePrefs` storage by calling:
```kotlin
storage.getAll()
```

You can check if `SecurePrefs` storage contains selected `key` by calling:
```kotlin
storage.contains(key = "someKey")
```

You can also remove selected key from storage:
```kotlin
storage.remove(key = "someKey")
```

Last, but not least, you can remove all data stored in `SecurePrefs` storage:
```kotlin
storage.clear()
```

## About
`SecurePrefs` allows to store key-value pairs in platform-specific way securely.
Forked from `Kissme` to add api level 21 support and replace Android implementation with androidx.security.EncryptedSharedPreferences

### Android
Android implementation uses androidx.security.EncryptedSharedPreferences

In order to acquire the application `Context` instance required for data storing operations the library registers an internal 
 `ContentProvider`.

### iOS
The iOS implementation is using native iOS `Keychain`. The Secure Enclave is a hardware-based key manager that's isolated from processor. It allows you to store, delete, fetch passwords and accounts. 
`Keychain` is simple wrapper build upon `Security` interface to store, save, and fetch not only passwords, but also accounts.

## Running sample app
Sample app uses Maven Local for resolving `SecurePrefs` dependencies. Before running sample app you need to:
1. Build the library - `./gradlew build`
2. Publish dependencies to Maven Local - `./gradlew publishToMavenLocal`
3. Run selected library. If you want to run iOS app - you need to properly configure Xcode.
 Please check: https://kotlinlang.org/docs/tutorials/native/mpp-ios-android.html#setting-up-xcode before running iOS sample app.
 

## License

Copyright 2018 Netguru

Copyright 2020 ATizik

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
