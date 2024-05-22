
<p align="center">
    <img title="Flutterwave" height="200" src="https://notch.sfo3.cdn.digitaloceanspaces.com/logo/svg/logo-full.svg" width="70%"/>
</p>


# Notch Pay Javascript Library


![NPM Version](https://img.shields.io/npm/v/notchpay.js)
![NPM Downloads](https://img.shields.io/npm/d18m/notchpay.js)
![NPM License](https://img.shields.io/npm/l/notchpay.js)

## Introduction

La bibliothèque Javascript simplifie l'utilisation des API de Notch Pay dans vos applications Javascript. Elle masque la complexité de l'intégration directe, facilitant ainsi des appels rapides et efficaces aux API.

Available functionalities include:

- Payment : Paypal, Mobile Money,



## Table of Content
1. [Requirements](#requirements)
2. [Installation](#installation)
3. [Initialization](#initialization)
4. [Usage](#usage)
5. [Support](#support)
6. [License](#license)
7. [Changelog](/CHANGELOG.md)

## 1. Requirements

2. Node 12 or higher.
1. Notch Pay [API Keys](https://business.notchpay.co/developer/api-keys)



## 2. Installation

To install the package, run the following command in your Node terminal:

```sh
npm install notchpay.js
```


## 3. Initialization

```javascript
import NotchPay from 'notchpay.js';

const notchpay = NotchPay(
    "YOUR_PUBLIC_KEY", 
    { debug : true, } 
);
```

For staging (Test environment), use the Sandbox Public Keys and for production, use LIVE Public KEYS.
You can obtain your PUBLIC_KEY and PRIVATE_KEY keys from the Notch Pay dashboard: https://business.notchpay.co/developer/api-keys. 


## 4. Usage
1. [Collections : Paypal, Mobile Money](https://developer.notchpay.co/reference/payments)

This section describes how you can collect payments in the SDK. Find out [more about](https://developer.notchpay.co/reference/payments) the payment method.

- [Initialize Payment](https://developer.notchpay.co/reference/payments#initialize-payment)
```javascript

const paymentInitiated = await notchpay.payments.initializePayment({
      currency: "XAF", 
      amount: "5000", 
      email: "WWWWW", 
      phone: "XXXXX", 
      reference: "ref." + (Math.floor(Math.random() * (2000 - 100 + 1)) + 100), 
      description: "Payment for testing the Notch Pay SDK"
});


// console.log("Payment Initialized Informations: ", paymentInitiated);

```

- [Verify and fetch Payment](https://developer.notchpay.co/reference/payments#verify-and-fetch-payment)
```javascript

const paymentDetails = await notchpay.payments.verifyAndFetchPayment(paymentInitiated.transaction.reference);

```


- [Complete Payment](https://developer.notchpay.co/reference/payments#complete-payment)
```javascript

const paymentCompleted = await notchpay.payments.completePayment(
    paymentInitiated.transaction.reference, 
    { 
        channel: 'string', 
        data: { 
            phone: 'MTN Mobile or Orange mobile money number to be charged'
        }
    }
);

```

- [List Payments](https://developer.notchpay.co/reference/payments#list-payments) : This endpoint allows you to retrieve a paginated list of all your payments.
```javascript

const paymentList = await notchpay.payments.listPayments({perpage: 10, page: 2});

```

- [Cancel Payment](https://developer.notchpay.co/reference/payments#cancel-payment) : Cancel a payment.
```javascript

const paymentCancelled = await notchpay.payments.cancelPayment(response.transaction.reference);

// console.log(paymentCancelled);
```

## 5. Support
Pour toute aide supplémentaire concernant l'utilisation de cette bibliothèque, contactez l'équipe technique via [email](mailto:hello@notchpay.co) ou sur [Telegram](https://t.me/notchpay). Vous pouvez également nous suivre sur [Twitter](https://twitter.com/thenotchpay) et nous faire part de vos commentaires.

## 6. Debugging Errors
We understand that you may encounter errors when integrating our library. You can read more about our error messages [here](https://t.me/notchpay).
For error responses `authorization 401` and `validation 422`, please check your API keys and your request. If you get a `server` error, please contact the team for [support]().



## 7. License

By contributing to this library, you agree that your contributions may be placed under the MIT license.
Copyright (c) [Notch Pay Sarl](https://notchpay.co).

## 8. Change Logs

