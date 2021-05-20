---
title: Kin iOS Starter
date: Last Modified
permalink: starters/kin-ios-starter/index.html
eleventyNavigation:
  key: KiniOSStarter
  order: 43
  parent: Starters
  title: iOS
---


## Introduction

This will get your iOS app Kin-enabled in a few minutes. All you need to do is add a simple class file to your app, and you should be able to make calls to Kin's blockchain immediately.

## Requirements

Make sure you have read [Getting Started](/tutorials/getting-started/) and have the required environment variables

## Installation

1. Make sure your project is set up for [cocoapods](https://guides.cocoapods.org/using/using-cocoapods.html)
2. Add the kin SDK to your [Podfile](https://github.com/kintegrate/kin-starter-ios/blob/main/Podfile)
3. Add the [Kin.swift](https://github.com/kintegrate/kin-starter-ios/blob/main/kin-starter-ios/Kin.swift) class to your app
4. Make sure you have added an [app icon](https://developer.apple.com/tutorials/mac-catalyst/updating-the-app-icon)
5. Instantiate the class in any `class`.
   - Instantiation requires several variables from the getting started section:
   ```swift 
   let kin = Kin(
      isProduction: false,
      appIndex: 165, //Your App Index
      appAddress: "GC6D...32XS", //Your Public Address
      credentialUser: "MyUser", //Your device's current user
      credentialPassword: "MyPass", //Device's current password
      onBalanceChanged: { [weak self] balance in
          // Handle balance update
      },
      onPaymentHappened: { [weak self] payment in
         // Handle payment
      }
    )
    ```
   
6. See [ViewController.swift](https://github.com/kintegrate/kin-starter-ios/blob/main/kin-starter-ios/ViewController.swift) for instantiation and sample calls

## Note on Webhooks

Any transactions made by the device will alert your server with a webhook. (see server tutorials). Your server will receive a notification of the transaction, including `MyUser` and `MyPass` credentials above. The credentials help your server track transactions from specific users.

However, you can safely test your device code without turning on your webhooks.

## Demo App

A demo App is included that you can run and test. To use the app:

1. Pull https://github.com/kintegrate/kin-starter-ios into a local folder
2. Open the kin-starter-ios.xcworkspace file.
3. Click run in xcode to run

### Kin Drops

To fund the demo app or any address in Kin's `TEST` blockchain, simply copy its address and paste it to Kin drops:

https://kin-drops.herokuapp.com/?ADDRESS_HERE

The service will send it 10 Kin in the test network. You can refresh this as often as you like to add more Kin to your app.

The example app linked above has an example of this functionality as well.

