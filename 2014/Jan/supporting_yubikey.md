# Supporting YubiKey

The majority of two-factor authentication, from services like [Google Authenticator] for example, are entirely software based. They work with your mobile phones to generate x digit authentication codes which can be used as an additional confirmation. For whatever reason, most places seem to have decided on 6 digit codes. These codes change at a set interval and when you use your two factor code, the application verifies that the code you entered is valid and then allows you to proceed. 

These codes are generated based on a secret word that is known on the server and associated with you, and the time. The idea is that based on your secret and knowing the time only one password can exist that matches that. When you send along your two-factor code the server actually generates a series of codes based on a timestamp tolerance. For example, if your timestamp tolerace is 30 seconds, it generates 30 codes for the last 30 seconds and checks to see if your code matches. Your secret + timestamp will always generate the exact same code. This is the basis of two-factor authentication. 

## Enter Yubikey
YubiKey is a hardware authentication token, much like the old RSA hardware tokens that were popular in large corporations. The idea is that instead of relying just on your phone to generate these codes, there is a closed system encased in custom hardware that is generating these codes. The codes are then authenticated against YubiKey servers, like standard software based tokens, and it fuctions as a two-factor authentication mechanism. Since they control both the hardware AND the server that authenticates, they are no longer limited to utilizing the secret+time password and are free to do whatever they want.

I recently found myself needing to add YubiKey support and was completely blown away by how easy it is to add. Yubico (The company behind YubiKey) has made it unbelievably easy for third party developers to add support for YubiKey.

## What you need
- A YubiKey
- Application ID
- Signature Secret
- Client Library

That's right, you need a YubiKey first in order to add support for it. It's not that big of a deal, and the cheapest hardware that you can get is 25 USD for the [standard YubiKey](https://store.yubico.com/). 

To get the other two, simply wander over to the [API Key request page](https://upgrade.yubico.com/getapikey/) and punch in your email address and OTP (One Time Password - what you get when you hit the button on your YubiKey). It will generate the two for you - keep a note of those for now, it is what you will need in order to use the Yubico API.

For this example, I'm using a PHP library in order to handle the interaction with the API. You can find it [here](https://code.google.com/p/yubikey-php-webservice-class/). It's currently (2014/01/22) linked to from the libraries page.

## Some Code
<script data-gist="gist8562825" src="https://gist.github.com/AngeloR/8562825.js"></script>

As you can see, the actual verification portion is unbelievably simple. 

- Line 7: We instantiate the Yubikey class passing in our Application ID and Signature that we generated on the Yubico website.
- Line 8: We call the verify method which creates our request and makes a call to the Yubikey servers to validate the OTP.

And that's all you need to add Yubikey support to your application. The next section just goes into a little more detail and explains a couple options that you have.

## Under the covers
There are a couple of things that actually happen when we call the verify method.

1. We add the parameters (id, otp) and create a signed request using base64_encoding, hmac and the signature that we provided. 
2. We using cURL to visit the url and validate the OTP

Since there is a network call that happens to validate the OTP the library provides a mechanism to override the curl timeout defaults called `setCurlTimeout()`. There is also a way for us to verify the "Timestamp Tolerance". IE, adjust the number of OTPs to generate during verification. You can do that with `setTimestampTolerance()`.
