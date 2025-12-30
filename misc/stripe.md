---
description: How to configure Stripe payments
---

# Stripe

The whole process consists of 3 Steps:

1. Add Webhook
2. Generate secret key
3. Configure payment options (in config.php)

## 1. Add Webhook

Visit Stripe Webhooks Page [https://dashboard.stripe.com/webhooks](https://dashboard.stripe.com/webhooks)

Click on "Create an event destination"

<figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

You should see following screen, fill it as follows:

(replacing naturally your-domain.com with your domain)

<figure><img src="../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

As **Endpoint URL** enter:

* For MyAAC 1.0+ and Gesior Shop System 6.0+

    * https://your-domain.com/payments-notify/stripe

* For MyAAC 0.8 and Gesior Shop System 5.0+

    * https://your-domain.com/payments/stripe.php

On the same screen, click on "Select events". You should see following screen.

<figure><img src="../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

From the events select **checkout.session.completed**

This is the only event we need.

Then click on Add events button

<figure><img src="../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

And finally click on "Add endpoint"

<figure><img src="../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

After that you should be redirected to your Webhook site

Click on "Reveal" Signing Secret:

<figure><img src="../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

You should see a key, which you enter in plugins/gesior-shop-system/config.php, in the Stripe section, under endpoint_secret:

<figure><img src="../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

## 2. Create Secret Key

Go into [https://dashboard.stripe.com/apikeys](https://dashboard.stripe.com/apikeys)

Click **Create secret key:**

<figure><img src="../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

In the popup screen select the second option (Building your own integration):

<figure><img src="../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

Finally, click on **Create secret key**

You will receive a mail, and also will need probably to confirm using Auth App.

When everything goes smooth, you should see your secret key:

<figure><img src="../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

Enter in into same config.php like before under "secret\_key", here:

<figure><img src="../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

## 3. Configure payment options (in config.php)

Finally, you can configure the payment options in plugins/gesior-shop-system/config.php, which by default looks like this:
```php
	'payments' => [
		['price' => '10', 'currency' => 'USD', 'points' => '100', 'name' => '100 premium points on Your OTS'],
		['price' => '20', 'currency' => 'USD', 'points' => '200', 'name' => '200 premium points on Your OTS'],
		['price' => '30', 'currency' => 'USD', 'points' => '300', 'name' => '300 premium points on Your OTS'],
		['price' => '40', 'currency' => 'USD', 'points' => '400', 'name' => '400 premium points on Your OTS'],
		['price' => '50', 'currency' => 'USD', 'points' => '500', 'name' => '500 premium points on Your OTS'],
	],
```