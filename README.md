
# OttuCheckout

The OttuCheckout is iOS SDK makes it quick and easy to build an excellent payment experience in your iOS app. We provide powerful and customizable UI screens and elements that can be used out-of-the-box to collect your user's payment details. We also expose the low-level APIs that power those UIs so that you can build fully custom experiences.

## Features

**Simplified security**: We make it simple for you to collect sensitive data such as credit card numbers and remain PCI compliant. This means the sensitive data is sent directly to Stripe instead of passing through your server.

**SCA-ready**: The SDK automatically performs native 3D Secure authentication if needed to comply with Strong Customer Authentication regulation in Europe.

**Native UI**: We provide native screens and elements to collect payment details.

<p float="left">
<img src="https://github.com/Maninder1991/screens/blob/main/Cardfree.png" alt="PaymentUI" align="center"  width="200" height="400"/>
<img src="https://github.com/Maninder1991/screens/blob/main/WithCardPayment.png" alt="PaymentUI" align="center"  width="200" height="400"/>

**Localized**: We support the following localizations: English, Arabic.

#### Recommended usage

If you're selling digital products or services that will be consumed within your app, (e.g. subscriptions, in-game currencies, game levels, access to premium content, or unlocking a full version), you must use Apple's in-app purchase APIs. See the [App Store review guidelines](https://developer.apple.com/app-store/review/guidelines/#payments) for more information. For all other scenarios you can use this SDK to process payments via Stripe.

#### Privacy

The OttuCheckout SDK collects data to help us improve our products and prevent fraud. This data is never used for advertising and is not rented, sold, or given to advertisers.

## Requirements

The OttuCheckout requires Xcode 13.0 or later and is compatible with apps targeting iOS 12 or above.

## Getting started

To initialize the SDK you need to create session token. 
You can create session token with our public API [Click here](https://app.apiary.io/iossdk2/editor) to see more detail about our public API.
    
Installation
==========================

#### Installation with dependecy

Put below dependency into your gradle

```java
allprojects {
  repositories {
	...
	maven { url 'https://jitpack.io' }
  }
}
    
dependencies {
       implementation 'com.github.sdkpayment:Android-SDK:Tag'
}
```

*Swift 5.1, 5.0, 4.2, 4.0*

In ViewController.swift, just import Ottu framework and initalize Ottu SDK.

```swift
import Ottu

class ViewController: UIViewController,OttuDelegate {

    var responseDict : [String:Any]?
    var message = ""
    
    override func viewDidLoad() {
        super.viewDidLoad()
        let sessionId = "ENTER_YOUR_SESSION_ID"
        _ = Ottu.init(sessionId, merchantId: "MERCHANT_ID", viewController: self, delegate: self,,language: "ENTER_LANGUAGE_ID_en_or_ar")
    }
    
    func errorCallback(message: String, response: [String : Any]?) {
        responseDict = response
        self.message = "Error"
        self.dismissed()

    }
    
    func cancelCallback(message: String, response: [String : Any]?) {
        responseDict = response
        self.message = "Cancel"
        self.dismissed()
    }
    
    func successCallback(message: String, response: [String : Any]?) {
        responseDict = response
        self.message = "Success"
        self.dismissed()
    }
    
    func beforeRedirect() {
        
    }
    
    func dismissed() {
        DispatchQueue.main.asyncAfter(deadline: .now()+1) {
            let alert = UIAlertController(title: self.message.capitalized, message: "\(String(describing: self.responseDict))", preferredStyle: .alert)
            alert.addAction(UIAlertAction(title: "Ok", style: .default, handler: nil))
            self.present(alert, animated: true, completion: nil)
        }
    }
    
}
```
## Inetgrate Apple pay

**Note**: To inetgrate apple pay you need to enable apple pay in capabilites in your project. 


## Licenses

- [OttuCheckout License](LICENSE)
