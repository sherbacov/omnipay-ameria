# Omnipay: Ameria

**Ameria bank driver for the Omnipay Laravel payment processing library**

[Omnipay](https://github.com/thephpleague/omnipay) is a framework agnostic, multi-gateway payment
processing library for PHP 5.5+. This package implements Ameria support for Omnipay.

## Installation

    composer install sherbacov/omnipay-ameria

Omnipay is installed via [Composer](http://getcomposer.org/). To install, simply add it
to your `composer.json` file:

```json
{
    "require": {
        "sherbacov/omnipay-ameria": "1.0.0"
    }
}
```

And run composer to update your dependencies:

    composer update

Or you can simply run

    composer require sherbacov/omnipay-ameria

## Basic Usage

1. Use Omnipay gateway class:

```php
    use Omnipay\Omnipay;
```

2. Initialize Ameria gateway:

```php
     $gateway = Omnipay::create('AMERIA');
     $gateway->setClientId(env('clientId'));
     $gateway->setUsername(env('username'));
     $gateway->setPassword(env('password'));
     $gateway->setTestMode('bool');
     $gateway->setLanguage('ameria language');
     $gateway->setDescription('some description');
     $gateway->setAmount(10);  // Amount to charge, for test it should be 10
     $gateway->setTransactionId('XXXX');  // Transaction ID from your system
     ....
```

3. Call purchase, it will automatically redirect to ameria's hosted page

```php
     $purchase = $gateway->purchase()->send();
     if ($purchase->isRedirect()) {
         $purchase->redirect();
     }
```

4. Create a webhook controller to handle the callback request at your `RESULT_URL` and catch the webhook as follows

```php

    $gateway = Omnipay::create('Ameria');
    $gateway->setClientId(env('clientId'));
    $gateway->setUsername(env('username'));
    $gateway->setPassword(env('password'));
    
    $purchase = $gateway->completePurchase('paymentID')->send();
    
    if ($purchase->isSuccessful()) {       
        // Your logic     
    }
    
    return new Response('OK');

```
## Information

In this package implemented AmeriaBank integration vPOS 3.0. 

API interaction is performed via data exchange through Rest (except administration page: SOAP) .

For more information read ameria Bank documentation.

## Support

If you are having general issues with Omnipay, we suggest posting on
[Stack Overflow](http://stackoverflow.com/). Be sure to add the
[omnipay tag](http://stackoverflow.com/questions/tagged/omnipay) so it can be easily found.

If you want to keep up to date with release anouncements, discuss ideas for the project,
or ask more detailed questions, there is also a [mailing list](https://groups.google.com/forum/#!forum/omnipay) which
you can subscribe to.

If you believe you have found a bug, please report it using the [GitHub issue tracker](https://github.com/thephpleague/omnipay-idram/issues),
or better yet, fork the library and submit a pull request.
