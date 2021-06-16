---
title: Kin React Native Starter
date: Last Modified
permalink: starters/kin-react-native-starter/index.html
eleventyNavigation:
  key: KinReactNativeStarter
  order: 48
  parent: Starters
  title: React Native
---

## Introduction

This will get your React Native app Kin enabled in a few minutes. All you need to do is add a simple class file to your app, and you should be able to make calls to Kin's blockchain immediately.

## Requirements

Make sure you have read [Getting Started](/tutorials/getting-started/) and have the required environment variables

## Installation

1. Install the Kin SDK for React Native to your project:

   ```shell
   yarn add @kin-sdk/react-native
   # Or if you are using npm
   npm install @kin-sdk/react-native
   ```

2. Add the [KinService.ts](https://github.com/kintegrate/kin-starter-react-native/blob/main/src/KinService.ts) class to your app

3. Import and instantiate a new KinService.
   - Instantiation requires several variables from the getting started section:

     ```typescript
      const kinService = new KinService(KinEnvironment.Test);
     ```

4. See [App.tsx](https://github.com/kintegrate/kin-starter-react-native/blob/main/src/App.tsx) for instantiation and sample calls

## Note on Webhooks

Any transactions made by the device will alert your server with a webhook. (see server tutorials). Your server will receive a notification of the transaction, including `MyUser` and `MyPass` credentials above. The credentials help your server track transactions from specific users.

However, you can safely test your device code without turning on your webhooks.

## Demo App

A demo App is included that you can run and test. To use the app:

1. Pull https://github.com/kintegrate/kin-starter-react-native into a local folder
2. Access the `/kin-starter-react-native` folder on your local.
3. Install the dependencies

   ```shell
   yarn install
   ```

    ### iOS

    ```shell
    cd ios && pod install
    ```

4. Start Android app

   ```shell
   yarn android
   ```

5. Start iOS app

   ```shell
   yarn ios
   ```

### Kin Drops

To fund the demo app or any address in Kin's `TEST` blockchain, simply copy its address and paste it to Kin drops:

https://kin-drops.herokuapp.com/?ADDRESS_HERE

The service will send it 10 Kin in the test network. You can refresh this as often as you like to add more Kin to your app.
