# Web Payments Example

[![Greenkeeper badge](https://badges.greenkeeper.io/tnguyen14/web-payments-example.svg)](https://greenkeeper.io/)

> Demo for Payment Request API and Apple Pay for the Web <https://lab.tridnguyen.com/web-payments-example/>.

To see Payment Request API, use Chrome on Android version 53 or later.

To see Apple Payfor the Web in action, use Safari on iOS 10 or macOS Sierra (please note that you'd need to have Apple Pay enabled on your phone, and "Allow Payments on Mac" enabled for desktop use).

## Set up Apple Pay merchant account

If you'd like to have your own instance of this running, follow the steps below:

1. Create an Apple Developer Account (at <https://developer.apple.com>)
2. Create a Merchant ID (see [Configuring Your Environment](https://developer.apple.com/library/ios/ApplePay_Guide/Configuration.html))

	To generate the Payment Processing Certificate on your own, run the following steps

	```sh
	openssl ecparam -out private.key -name prime256v1 -genkey
	openssl req -new -sha256 -key private.key -nodes -out request.csr
	```

3. In the "Apple Pay on the Web" section, "Add Domain" under "Merchant Domains" and follow the instruction to verify your domain ownership
4. Under "Apple Pay Merchant Identity", click on "Create Certificate".
5. In order to create the Certificate Signing Request(CSR), run the following command (make sure you have `openssl` installed).

	```sh
	openssl req -sha256 -nodes -newkey rsa:2048 -keyout applepaytls.key -out applepaytls.csr
	```
6. Upload the `applepaytls.csr` file to the File Upload in the Apple Developer portal.
7. Store the `applepaytls.key` file to the `server/resources` directory.
8. With the `merchant_id.cer` file received from Apple, run the following command to generate a `.pem` file.

	```sh
	openssl x509 -inform der -in merchant_id.cer -out applepaytls.pem
	```
9. Store the `applepaytls.pem` file to the `server/resources` directory.
10. Start the application

	```sh
	npm start
	```
