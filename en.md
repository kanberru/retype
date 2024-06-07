# Setting up for Tilda ⚡

Welcome and thank you for using our service **kanber.ru**

# 1. Getting YandexPay keys ⚡

To start working with the service, you need to get several keys [here](https://console.pay.yandex.ru/web/account/settings/online)

![Getting Merchant ID](image.png)

> [!TIP]
> You also need to set the Callback URL - https://api.kanber.ru/api/v1/payments/yandex-pay

![Setting the Callback URL](image-1.png)

And also, you need to issue a key, it's just below, copy the key and save it, the key ID is not needed

# 2. Setting up Tilda ⚡

Go to [Profile](https://tilda.ru/identity/), check the box "Participate in testing new functions" and click "Save".

Go to Site Settings -> Payment systems -> Universal payment system.

Select the "Kanber" template

![Kanber template](kanberTilda.jpg)

In the Login field, enter **`Payment system login` from the Kanber personal account**

In the secret key field, enter **`Secret for signing an order`** from the Kanber personal account

You can leave the “URL FOR NOTIFICATIONS” field empty

Fill in the currency (only RUB is supported for now), taxes, FFD at your discretion