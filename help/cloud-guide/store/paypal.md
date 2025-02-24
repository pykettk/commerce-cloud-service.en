---
title: Set up PayPal payment methods
description: Set up PayPal payment methods for Adobe Commerce on cloud infrastructure.
exl-id: e52fd719-f936-4e8b-8222-af133389d9e2
---
# Set up PayPal payment methods

Adobe Commerce on cloud infrastructure provides an on-boarding tool to configure PayPal Express Checkout accounts directly through the Admin. This tool is available for ECE 2.1.8 and later. To better support going live and testing PayPal payment methods, you can enable and configure your PayPal Express Checkout account for sandbox or production accounts.

You can configure either the sandbox or production account in every environment:

*  For Integration and Staging environments, we recommend setting Sandbox credentials.
*  For your Production environment, you can set Sandbox credentials for initial testing, then replace with live production credentials for a launched store.

## PayPal account

While we recommend having a PayPal merchant account prepared and configured, you can create an account or upgrade a personal account through the Admin.

[!DNL PayPal onboarding] supports connecting with the following accounts:

*  PayPal Business account
*  PayPal personal account, converting to a Business account. If you have an existing personal PayPal account, you can log in with those credentials and upgrade this account to a business account as you complete the sync.

If you do not have an existing PayPal account, create one. Enter an email address for a new account. If a matching PayPal account is not found, follow the prompts to create a PayPal Business account. Or you can create an account directly through [PayPal](https://www.paypal.com/us/webapps/mpp/account-selection).

### PayPal limitations

PayPal supports connecting PayPal Express Checkout for countries across the globe except for the following limitations:

*  India, and Japan (future PayPal updates may support these accounts)
*  Israel

For Brazil, you must have an existing PayPal business account to connect. You cannot convert an existing personal PayPal account for Brazil during this process. If you need an account, [create a business PayPal account](https://www.paypal.com/us/webapps/mpp/account-selection).

## Configure PayPal Express Checkout

To configure PayPal Express Checkout:

1. Access the Admin Console for the environment.
1. In the left-side navigation, select **Stores** > **Configuration**, then select **Sales** > **Payment Methods**.
1. For PayPal, select **Configure**. Configuration fields display in expandable sections for Express Checkout, Advertise PayPal Credit, and Basic and Advanced settings.
1. Connect your PayPal account. Until the account is connected, the options to enable are disabled. For details on available and supported accounts to connect and limitations, see [PayPal account](#paypal-account).

   *  To connect your PayPal live account, click Connect with PayPal and follow the prompts. Any customer purchases using a live PayPal complete and actively charge customers in a live store.
   *  To connect your sandbox account for testing, click Sandbox Credentials and follow the prompts. Any customer purchases using a Sandbox PayPal complete without actively charging customers.

1. Configure the Express Checkout settings to authenticate and use the PayPal API:

   *  **Email Associated with PayPal Merchant Account** (Optional) enter the email address associated with your PayPal merchant account. This email is case-sensitive.
   *  **API Authentication Methods** as API Signature or API Certificate.
   *  API Username, Password, and Signature captured from your PayPal account.
   *  **Sandbox Mode** select Yes or No to indicate if the credentials you entered are for sandbox. If you entered production credentials, select No.
   *  **API Uses Proxy** select Yes or No to set if the system uses a proxy server to establish a connection between Adobe Commerce and the PayPal payment system. If Yes, enter the proxy host and port.

1. For detailed information and steps for configuring your account, see [PayPal Express Checkout](https://docs.magento.com/user-guide/payment/paypal-express-checkout.html) starting with Step 2 Complete the Required Settings.

With the account configured and authenticated, you can enable and disable PayPal payment options under Required PayPal Settings:

*  **Enable this Solution** displays the PayPal payment method to customers through the website.
*  **Enable In-Context Checkout Experience**
*  **Enable PayPal Credit** allows customers to PayPal credit financing without additional costs. PayPal pays the order up-front, handling all repayments for the credit directly with the customer.

## PayPal variables

When using the PayPal on-boarding tool with Adobe Commerce on cloud infrastructure, add the following variable to the `variables:env` section of the `magento.app.yaml` file.

```yaml
# Environment variables
variables:
  env:
    CONFIG__DEFAULT__PAYPAL_ONBOARDING__MIDDLEMAN_DOMAIN: 'payment-broker.magento.com'
```

If you are upgrading to 2.2 from 2.1.8 or later, you still need to add this variable.
