---
title: Kin Android Starter
date: Last Modified
permalink: starters/kin-android-starter/index.html
eleventyNavigation:
  key: KinAndroidStarter
  order: 41
  parent: Starters
  title: Android
---

## Introduction
This will get your Android app Kin enabled in a few minutes. All you need to do is add a simple class file to your app, and you should be able to make calls to Kin's blockchain immediately.


## Requirements
Make sure you have read [Getting Started](https://kintegrate.netlify.app/tutorials/getting-started/) and have the required environment variables


## Installation

1. Add the [Kin.kt](https://github.com/hitwill/kin-implementation-kotlin/blob/master/app/src/main/java/com/kin/kin/Kin.kt) class to your app 
2. Add entries in [AndroidManifest.xml](https://github.com/hitwill/kin-implementation-kotlin/blob/master/quick-start/AndroidManifest.xml) to your app's manifest
3. Add entries in [build.gradle](https://github.com/hitwill/kin-implementation-kotlin/blob/master/quick-start/build.gradle) to your app's gradle
4. Make sure `app_icon.png` exists in your `res\drawable` folder
5. Import and instantiate the class in any `activity`. 
    * Instantiation requires several variables from the getting started section:
    ```kotlin
      val kin = Kin(
            applicationContext, //Application context
            false, //In Production mode
            165, //Your App Index
            "GC6D...32XS", //Your Public Address
            "MyUser", //Your device's current user
            "MyPassword", //Device's current password
            ::balanceChanged, //get notifications for balance changes
            ::paymentHappened //get notifications for payments
        )
    ```
6. See [MainActivity.kt](https://github.com/hitwill/kin-implementation-kotlin/blob/master/quick-start/MainActivity.kt) for instantiation and sample calls

## Note on Webhooks
Any transactions made by the device will alert your server with a webhook. (see server tutorials). Your server will receive a notification of the transaction, including `MyUser` and `MyPassword` credentials above. The credentails help your server track transactions from specific users.

However, you can safely test your device code without turning on your webhooks.

## Demo App
A demo App is included that you can run and test. To use the app:

1. Pull https://github.com/hitwill/kin-implementation-kotlin into a local folder 
2. Access the `/demo` folder to your local.
3. Open in android studio and click run to emulate it. The app runs on Kin's test network and will display its Kin blockchain address on startup, which will have 0 Kin.

### Kin Drops
To fund the demo app or any address in Kin's `TEST` blockchain,  simply copy its address and paste it to Kin drops:

https://kin-drops.herokuapp.com/?ADDRESS_HERE

The service will send it 10 Kin in the test network. You can refresh this as often as you like to add more Kin to your app.

