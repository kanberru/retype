# Настройка виджета (По желанию, не обязательно)

Данный код нужно вставить в HTML-блок (T123 блок) на любой странице, лучше всего - header, чтобы виджет появлялся везде под кнопкой купить

```js
<style>
  .kanber_widget {
    width: 360px;
    margin: 16px 0;
  }
</style>
<script>
  // Заполните ваш Merchant ID
  const MERCHANT_ID = 'ВАШ_MERCHANT_ID';
  // Способы оплаты, целиком или Сплит
  const AVAILABLE_PAYMENT_METHODS = ['CARD', 'SPLIT'];


  function onYaPayLoad() {
    const productCards = document.querySelectorAll('.t744');
    productCards.forEach((productCard, index) => {
      addWidget(productCard, index)
    });
  }
  function addWidget(productEl, index) {
    const priceElement = productEl.querySelector('[field="price"]');

    const price = priceElement.textContent.replace(/\s/g, '');
    const YaPay = window.YaPay;

    // Данные платежа
    const paymentData = {
      // Для отладки нужно явно указать `SANDBOX` окружение,
      // для продакшена параметр можно убрать или указать `PRODUCTION`
      // env: YaPay.PaymentEnv.Sandbox,
      version: 4,
      currencyCode: YaPay.CurrencyCode.Rub,
      merchantId: MERCHANT_ID,
      totalAmount: price,
      availablePaymentMethods: AVAILABLE_PAYMENT_METHODS,
    };

  
    async function onPayButtonClick() {
    }

    function onFormOpenError(reason) {
      console.error(`Payment error — ${reason}`);
    }

    const payElId = `yapay_container_${index}`;

    // Создаем платежную сессию
    YaPay.createSession(paymentData, {
      onPayButtonClick: onPayButtonClick,
      onFormOpenError: onFormOpenError,
    })
      .then(function (paymentSession) {
        // Показываем кнопку Яндекс Пэй на странице.

        const payContainer = productEl.querySelector(".t744__btn-wrapper");
        if (payContainer) {
          const newDiv = document.createElement("div");
          newDiv.id = payElId; 
          newDiv.classList = "kanber_widget";
          if (payContainer.nextSibling) {
            payContainer.parentNode.insertBefore(newDiv, payContainer.nextSibling);
          } else {
            payContainer.parentNode.appendChild(newDiv);
          }
        } 
        
        paymentSession.mountWidget(document.querySelector(`#${payElId}`), {
          widgetType: YaPay.WidgetType.BnplPreview,
        });
      })
      .catch(function (err) {
        // Не получилось создать платежную сессию.
        console.error(err)
      });
  }
</script>
<script src="https://pay.yandex.ru/sdk/v1/pay.js" onload="onYaPayLoad()" async></script>
```

Важно, код может не работать, если карточка товара сделана в Zero Block