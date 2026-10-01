# CreatePay for Magento 2

A payment module for Magento 2 that integrates with the CreatePay payment gateway, supporting both Hosted and Direct payment integrations.

## Compatibility

- **Magento:** 2.3 and 2.4
- **Integration methods:** Hosted and Direct

## Requirements

The following credentials and configuration details are required to set up the module:

- Merchant ID
- Signature/Secret Key
- Gateway URL

If you already have a CreatePay account, please contact [createcommerce@createpay.com](mailto:createcommerce@createpay.com).

For all other enquiries, please contact [hello@createpay.com](mailto:hello@createpay.com).

## Installation

### Step 1: Prepare for Installation or Upgrade

If you are upgrading an existing installation, disable the module before proceeding.

Run the following command from your Magento root directory:

```bash
bin/magento module:disable Cardstream_PaymentGateway
```

Next, delete the existing `app/code/Cardstream` directory if it is present, as it may interfere with the new version.

You must also delete the `Cardstream_PaymentGateway` entry from the `setup_module` database table. This allows the required database tables and schema to be created during installation.

> **Note:** Back up your database and existing module files before upgrading.

### Step 2: Copy the Module Files

1. Locate the `httpdocs` directory included with the module.
2. Copy its contents into the root directory of your Magento installation.
3. If prompted to replace existing files, select **Yes**.

### Step 3: Enable the Module

From your Magento root directory, run:

```bash
bin/magento module:enable Cardstream_PaymentGateway
```

### Step 4: Upgrade and Compile Magento

Run the following commands to upgrade the database, compile dependencies and prepare Magento for the new module.

```bash
bin/magento setup:upgrade && \
bin/magento setup:db-schema:upgrade && \
bin/magento setup:di:compile && \
chmod 775 -R ./var
```

These commands allow Magento to install the module and create the necessary configurations.

### Step 5: Flush the Magento Cache

1. Log in to the Magento Admin Panel.
2. Navigate to **System > Cache Management**.
3. Click **Flush Magento Cache** in the top-right corner of the page.

### Step 6: Open the Payment Configuration

1. Navigate to **Stores > Configuration**.
2. Under the **Sales** section in the left-hand menu, select **Payment Methods**.
3. Locate the installed payment methods.

### Step 7: Configure the Cardstream Gateway

1. Expand the **Cardstream Gateway** section.
2. Enter the required payment gateway credentials and configuration details.
3. Select your preferred integration method:
   - **Hosted**
   - **Direct**
4. Configure the remaining settings as required.

> **Important:** Debugging should be disabled in production environments.

### Step 8: Configure the Cache Type

1. Navigate to **Stores > Configuration**.
2. Select **Advanced > System**.
3. Locate the caching configuration.
4. Change the caching type to **Varnished**.

Save your changes.

---

## Frequently Asked Questions (FAQ)

### 1. The `/paymentgateway/order/process` page displays a "Page Not Found" error

**Problem:** The payment processing page displays a 404 error when attempting to process an order.

**Solution:**

Check the following:

- Have you upgraded and recompiled Magento after installing the module?
- Has the order controller filename been changed?
- Has the order controller directory or its name been modified?
- Is the route correctly configured in `etc/frontend/routes.xml`?

The route configuration should contain the following:

- **Route ID:** `cardstream`
- **Front Name:** `cardstream`
- **Module Name:** `Cardstream_PaymentGateway`

Ensure that the route and module configuration are correct.

If you have made any changes, run the Magento upgrade and compilation commands again.

If the issue persists, contact CreatePay Support.

### 2. The error "Router requires an ID but one isn't set" appears

**Problem:** Magento displays the following error:

`Router requires an ID but one isn't set`

**Solution:**

Open the following file:

```text
etc/frontend/routes.xml
```

Ensure that the `router` element has an `id` attribute with the value `standard`.

### 3. The error "Module version difference schema version higher/lower than in a database" appears

**Problem:** Magento reports a mismatch between the module's schema version and the version recorded in the database.

**Solution:**

Delete the `Cardstream_PaymentGateway` row from the `setup_module` database table.

This allows Magento to recreate the necessary database structures during the installation or upgrade process.

After removing the entry, run the Magento upgrade and database schema commands again.

### 4. An incorrect signature error appears during checkout

**Problem:** An incorrect signature error occurs when processing a payment during checkout.

**Solution:**

1. Check that a signature is configured correctly in both Magento and the Merchant Management System (MMS).
2. Ensure that the signature contains only alphanumeric characters.
3. Remove any spaces, full stops or other special characters.

Verify that the signature matches in both systems.

### 5. The Cardstream Gateway is not visible in the Magento Admin Panel

**Problem:** The Cardstream Gateway does not appear under the payment methods in the Magento Admin Panel.

**Solution:**

Run the following commands from your Magento root directory:

```bash
php bin/magento setup:upgrade
php bin/magento setup:di:compile
```

Once the commands have completed successfully, refresh the Magento Admin Panel and check the payment methods again.

### 6. The amount, address and name appear to be cached during checkout

**Problem:** Customer details, including the payment amount, address and name, appear to be cached during checkout.

**Solution:**

Ensure that you are using the latest version of the module, which includes a fix for this issue.

If the problem persists after updating, contact CreatePay Support.

---

## Support

For assistance with an existing CreatePay account, contact:

- **Existing CreatePay accounts:** [createcommerce@createpay.com](mailto:createcommerce@createpay.com)
- **General enquiries:** [hello@createpay.com](mailto:hello@createpay.com)
