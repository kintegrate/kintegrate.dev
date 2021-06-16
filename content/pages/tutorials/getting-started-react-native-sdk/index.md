---
title: Getting Started with the React Native SDK
date: Last Modified
permalink: tutorials/getting-started-react-native-sdk/index.html
eleventyNavigation:
  key: TutorialsGettingStartedReactNativeSdk
  order: 28
  parent: TutorialsGettingStarted
  title: React Native
---

## Introduction

This tutorial will take you through the basics of creating a Kin enabled app using React Native.

## Requirements

Make sure you have read [Getting Started](/tutorials/getting-started/) and have the required environment variables

## Implementing KinService in your app

#### 1. Install the Kin SDK for React Native to your project

```shell
yarn add @kin-sdk/react-native
# Or if you are using npm
npm install @kin-sdk/react-native
```

#### 2. Create a React Native app and add the [KinService.ts](https://github.com/kintegrate/kin-starter-react-native/blob/main/src/KinService.ts) class to your app

This class abstracts some calls to Kin's official SDK and is fully usable out of the box. However, you can easily extend it to suite your custom needs.

#### 3. Instantiate a new KinService

We're creating a new instance of our Kin wrapper and pass in the environment. In this example we'll pick the Test network.

```typescript
const kinService = new KinService(KinEnvironment.Test);
```

### Congratulations! You now have a KinService enabled app running!

## Making calls to the Kin blockchain

In this example, we're going to create a new wallet by generating new key pair. After the wallet is created, we will send some Kin to Donald.

#### 4. Create a new account

We create a new key-pair, then call into our wrapper to create a new account.

```typescript
kinService
  .randomKeyPair()
  .then((acc) => {
    kinService.createAccount(acc.secret).then((result: any) => {
      console.log('Account created on Blockchain', result);
    });
  })
  .then((e) => {
    console.log('An error occurred', e);
  });
```

#### 5. Resolve account

After creation, we resolve the account to check if it exists, and get the balance

```typescript
kinService
  .resolveTokenAccounts(account.publicKey)
  .then((res) => console.log('Balance retrieved from Blockchain', res));
```

#### 6. Request Airdrop

We can now request and Airdrop to receive a bit of Kin. Note that this is only for the `Test` network.

```typescript
kinService
  .requestAirdrop(account.publicKey, '10')
  .then((res) => console.log('Airdrop requested from Blockchain', res));
```

#### 7. Send payment to Donald

Now we can send a payment to Donald.

```typescript
const destination = 'Don8L4DTVrUrRAcVTsFoCRqei5Mokde3CV3K9Ut4nAGZ';
const amount = '2';
const memo = 'Test Memo';

kinService
  .submitPayment(account.secret, destination, amount, memo, 0) // Use your App Index instead 0
  .then((result) => {
    console.log('Payment submitted on Blockchain', result);
  });
```

#### 8. Webhooks

When your app sends a transaction, your server also receives a notification with:

1. The username and password of the specific device
2. The amount of Kin the device spent
3. The invoice details

From here, your server can perform further actions, such as sending a loot box to the device. You can learn more about webhooks by going through the server tutorials.
