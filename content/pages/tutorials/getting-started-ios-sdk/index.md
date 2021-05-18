---
title: Getting Started with the iOS SDK
date: Last Modified
permalink: tutorials/getting-started-ios-sdk/index.html
eleventyNavigation:
  key: TutorialsGettingStartediOSSdk
  order: 23
  parent: TutorialsGettingStarted
  title: iOS
---


## Introduction

This tutorial will take you through the basics of creating a Kin enabled app using Swift.

## Requirements

Make sure you have read [Getting Started](/tutorials/getting-started/) and have the required environment variables

## Implementing Kin in your app
1. Make sure your project is set up for [cocoapods](https://guides.cocoapods.org/using/using-cocoapods.html)

2. Add the Kin SDK to your [Podfile](https://github.com/kintegrate/kin-starter-ios/blob/main/Podfile)

- Make sure to `pod install` after updating the podfile. This will bring the Kin SDK into your project

3. Add the [Kin.swift](https://github.com/kintegrate/kin-starter-ios/blob/main/kin-starter-ios/Kin.swift) class to your app

- The class abstracts some of the calls to Kin's official SDK and is usable out of the box. But feel free to modify/extend it to your needs.

4. Make sure you have added an [app icon](https://developer.apple.com/tutorials/mac-catalyst/updating-the-app-icon)

   - This is for a future expansion of the SDK, although it is currently required for instantiation.

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
      onPaymentHappened: { [weak self] payments in
         // Handle payment
      }
    )
    ```
      - The `app index` and `public address` are used by the Kin foundation to track blockchain transactions your app makes, and also authorize fee-less transactions for your app.
6. See [ViewController.swift](https://github.com/kintegrate/kin-starter-ios/blob/main/kin-starter-ios/ViewController.swift) for instantiation and sample calls

Congratulations! You now have a Kin enabled app running!

## Making calls to the Kin blockchain

### Public addresses

Kin is all about exchanging value between users and your server. (Sending and Receiving Kin). In order to exchange value, each device needs to have a `public address` (like an email address) that it can receive Kin from. Do not confuse the app's public address with the one you used to initialize the SDK. The public address above belongs to your server.

To see your device's public address, call:

```swift
kin.address()
```

### Tracking balances and payments

During instantiation, you passed two closures to your app. Here is a sample implementation of these closures:

```swist
onBalanceChanged: { [weak self] balance in
    // Handle balance update
    print("Balance was updated to: \(balance)")
}

onPaymentHappened: { [weak self] paymenta in
   // Handle payment callback
   print("Payments: \(payment)")

}
```

These are passive listeners to transactions on your Kin account. They will report changes in the balance:

1. On instantiation (use this to grab your app's initial balance)
2. When your app makes an **outgoing** payment

Note that it may take a minute or two for them to fire, after a payment has been made. In order to check if the balance has changed from an **incoming** payment, you can call:

```swift
kin.checkBalance { [weak self] result in
    switch result {
    case .success(let balance):
        print("account balance: \(balance)")
    case .failure(let error):
        // Handle error getting account balance
    }
}
```

When a transaction takes place in the blockchain, it may take a minute to reflect in the balance. If you call `checkBalance()` too early, you will not get the correct balance. E.g. if your app has 10 Kin, and you send it 10 Kin from another app, and immediately call `checkBalance()`, you will not get the up to date balance.

This is the most conservative and recommended way to monitor balances and transactions. However, you can modify the function in the class to listen more aggressively, which will consume your app's resources.

To test your listeners, run your app, get its address, and send it some Kin in the `Test blockchain`. You can do that by pasting the app's address to `Kin Drops.`

https://kin-drops.herokuapp.com/?YOUR_APP_ADDRESS

Calling `checkBalance()` will give you the updated balance.

### Viewing transactions

You can view transactions to and from your app, by pasting your app address on: https://explorer.solana.com/address/

If you are on the `Test envoronment`, click the `Main Net` button and switch it to custom, and enter the url: https://local.validator.agorainfra.dev. This will let you see transactions in the test network.

### Sending Kin

The Kin SDK allows you to send a single `payment`, that includes an `invoice` with multiple items. An invoice helps you keep track of what your users bought in your app. To send a payment, you first create an invoice with 1 or more items:

```swift
let payment1 = Kin.KinPaymentInfo(
    amount: 1.0,
    title: "Hamburgers"
)

let payment2 = Kin.KinPaymentInfo(
    amount: 1.0,
    title: "Even more hamburgers"
)
```

You then send this out by calling:

```swift
kin.sendKin(
    payments: [payment1, payment2],
    address: "GA6CCT5IB4DJBR63BM3BQ7WB3M2UZ6QG6Z5XB64GSIABH6ICIETTAVU2",
    paymentType: .spend,
    completion: { [weak self] result in
        switch result {
        case .success(let payment):
            // Handle payment success
        case .failure(let error):
            // Handle payment error
        }
    }
)
```

The SDK will convert the invoice into a hash, save the payment items for future reference, and finally send out the payment.

## Webhooks

When your app sends a transaction, your server also receives a notification with:

1. The username and password of the specific device
2. The amount of Kin the device spent
3. The invoice details

From here, your server can perform further actions, such as sending a loot box to the device. You can learn more about webhooks by going through the server tutorials.

## Congratulations

Your app is now set up to:

1. Listen and display changes in Kin balance
2. Send Kin

The Kin SDK is extremely versatile. We encourage you to look through the class to see how it has wrapped and implemented it. Make sure you go through the server tutorials, to see how to implement Kin on the server
