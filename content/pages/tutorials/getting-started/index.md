---
title: Getting Started
date: Last Modified
permalink: tutorials/getting-started/index.html
eleventyNavigation:
  key: TutorialsGettingStarted
  order: 30
  parent: Tutorials
  title: Getting Started
---
## Prerequisites
Create a free account on [heroku](https://heroku.com/). This is optional, but will help you run and understand our server tutorials faster. Alternatively, you can adjust our set up to work with your preferred server.

## Steps
Follow the steps below to prepare your app for Kin integration.

1. Create an empty `variables.txt` file on your desktop. Use it to save any variables we mention below in **`Bold Text`** (1 minute)
    * You will be collecting these variables from different sources, and eventually add them to your code. It is helpful to have them in one place for easy reference. 
    * For security, keep this text file offline, as it will contain some sensitive info.

2. Register your app [here](https://docs.google.com/forms/d/e/1FAIpQLSdz60FPmUB7qBq-TF7NNmRgM5W8wIqqL5oVHmMRbtBBXppv4Q/viewform). (2 minutes)
    * Registed apps receive an **`App Index`** the foundation uses to track Kin activity. Developers are rewarded with Kin for creating activity with Kin in their apps. It may take 48 hours to receive your app. 
    * For now, use **`165`** for your **`App Index`**. Remember to update this as soon as you receive your email.

3. Create your app **`public key`** and **`private key`** at the [Kin Laboratory](https://laboratory.kin.org/#account-creator?network=test). (1 minute)
    * Just hit Generate keypair and save both values.
    * Your public key is your server's Kin address. (Also called public address). Your app will needs this to send Kin to your server.
    * Keep your private key secret and never share it with anyone

4. Log on to [heroku](https://heroku.com/) or your preferred server and create a new blank server app. (5 minutes)
    * Save the **`server url`** to your variables list. E.g. `https://kin-server.herokuapp.com`
    * Save a **`server webhook`** endpoint. E.g. `https://kin-server.herokuapp.com/kinTransactionEvents`
     * Save a **`server events`** endpoint. E.g. `https://kin-server.herokuapp.com/kinTransactionEvents`
     * You can name the endpoints however you like.
     * Don't worry, we will create these in a later tutorial. We just need to know what their names are for now.
5. Go to https://passwordsgenerator.net/ and generate a strong password. (1 minute)
    * Save the password as **`webhook password`**
6. When you receive an email response from the Kin foundation: (later)
    * Update the **`App Index`** in `variables.txt` with the one they provide in the email
    * Supply them with your **`public key`**, **`server webhook`**, **`server events`** and **`webhook password`**
    * Say *yes* to app invoicing

The Kin foundation now has all the data they need to reward you for implementing Kin in your app. We will use all these variables in later tutorials, and also learn how to use webhooks and invoicing to send payments. You will be surprised at how easy it is to implement Kin into any app.

You do not need to wait for the email response. You can start building with Kin immediately.
## Congratulations!
You have completed the preliminary steps to integrating your app with Kin, and you are now ready to get started. Pick the next tutorial to integrate your app. We recommend starting with the client side code first. E.g. Android, iOS, etc.


## Note on public keys
The Kin SDK uses public keys in two formats:
1. Stellar: `GCGP67EMU6L3OXEDDPFJWE7WJUNAYKXL6LBQJ27RXDURSINQ7DCBZ3HO`
2. Solana:  `AVQ2pAR7PnuRz2oGQ7i5BB2dFYDLdRJC7B3sFU9nGCfD`

The two keys above are different representations of the same blockchain address. For consistency, use the Stellar format *only* to instantiate SDK's (where required). This is the Key you provide to the Kin Foundation above.

In all other instances, use the Solana format for consistency. The Stellar format is an artefact from Kin's previous blockchain.