---
title: Novalnet Childwindow integration
draft: false
publish: false
tags:
  - Novalnet
  - Payment
  - 📬
date: 2024-09-02
---
We send following request body for the request for the child window URL:

```json
{
	"merchant": {
		"signature": "dli0pontrw4bHjSlMxxtqmg1V|us|bobljbc7ob5f|uw|uHChxLAWourerYmtqw7cpn7pc",
        "tariff": "14820"
	},
	"customer": {
        "gender": "m",
		"first_name": "Max",
		"last_name": "Mustermann",
		"email": "test1@dotsource.de",
        "customer_ip": "172.18.0.1",
        "customer_no": "8796158689284",
        "vat_id": "123456789",
        "session": "s6137072869136"
	},
	"transaction": {
		"amount": "0",
		"currency": "EUR",
        "order_no": "123456789",
		"test_mode": "1",
        "hook_url": "https://demo-boot.md-local.de/de/payment/webhook"
	},

	"hosted_page": {
		"hide_blocks": [
     "ADDRESS_FORM",
			"SHOP_INFO",
			"HEADER"
		],

		"skip_pages": [
			"CONFIRMATION_PAGE",
			"PAYMENT_PAGE",
      "SUCCESS_PAGE"
		]

	},
    "marketplace": {
        "tx_split": {
            "10522": "12200"
        }
    },
    "custom": {
        "lang": "de"
    }
}
```


Here is the frontend script we use to render the checkout.js script and bind the event handler for the postMessage:

```js
MD.onlinePayment = {
  init: function () {
    if ($("body").hasClass("page-orderOverviewCheckoutPage")) {
      MD.onlinePayment.enableButton();
    }
  },

  enableButton: function () {
    const button = $(".start-online-payment-button");
    button.prop("disabled", false).removeClass("disabled");
    button.on("click", () => {
      this.renderPayment();
    });
  },

  renderPayment: async function () {
    const value = $('input[name="onlinePaymentTotalAmount"]').val();
    const currency = $('input[name="onlinePaymentCurrencyIso"]').val();

    if (value && currency) {
      const response = await fetch(
        "/de/checkout/multi/orderOverview/requestPayment",
        {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify({
            amount: parseFloat(value),
            currencyIso: currency,
          }),
        },
      ).catch((error) => {
        console.log("Could not request payment. Reason: ", error);
      });

      /**
             @type {{
              success: boolean,
              data: {
              transactionSecret?: string,
              redirectUrl?: string,
              },
              message?: string}}
			 */
      const res = await response.json().catch((error) => {
        console.log("Could not parse response. Reason: ", error);
      });

      if (res && res.success) {
        const redirectUrl = res.data.redirectUrl;
        if (redirectUrl) {
          window.location.href = redirectUrl;
        } else {
          const scriptElement = document.createElement("script");

          scriptElement.setAttribute("type", "text/javascript");
          scriptElement.setAttribute(
            "src",
            `https://paygate.novalnet.de/v2/checkout-1.1.0.js?t=${new Date().getTime()}`,
          );
          scriptElement.setAttribute("id", "novalnet-checkout-js");
          document.head.appendChild(scriptElement);

          scriptElement.addEventListener("load", function () {
            Novalnet.setParam("nn_it", "child_window");
            Novalnet.setParam("txn_secret", res.data.transactionSecret);
            Novalnet.render();
            MD.onlinePayment.bindNovalnetEventListener();
          });
        }
      } else {
        const redirectUrl = res.data.redirectUrl;
        if (redirectUrl) {
          window.location.href = redirectUrl;
        } else {
          const message = res.message;
          if (message) {
          }
          alert(message);
          $("#globalMessages").html(
            '<div class="alert alert-danger">' +
              message +
              '<button class="close" aria-label="Close" data-dismiss="alert" type="button"><span aria-hidden="true">×</span><span class="sr-only">Close</span></button></div>',
          );
        }
      }
    }
  },

  /**
   * Handles the response event from Novalnet.
   *
   * @param {Event & {data: string, origin: string}} e - The response event.
   * @return {void}
   */
  NovalnetResponseEventHandler: async function (e) {
    if (e.origin === "https://paygate.novalnet.de") {
      /**
       * @type {{
       *     status_code: string,
       *     status: number,
       *     nnpf_postMsg: string,
       * }}
       */
      const json_event_data = JSON.parse(e.data);
      const response = await fetch(
        "/checkout/multi/orderOverview/validatePayment",
        {(
          method: "POST",
          body: JSON.stringify({
            ...json_event_data,
          }),
        },
      ).catch((e) => {
        console.log("Could not validate payment. Reason: ", e);
      });

      if (response) {
        /**
         * @type {{success: boolean, message: string}}
         */
        const res = await response.json().catch((e) => {
          console.log("Could not parse response. Reason: ", e);
        });
        console.log(res);
        if (res && res.success) {
          console.log("success");
        } else {
          $("#globalMessages").html(
            '<div class="alert alert-danger">' +
              res.message +
              '<button class="close" aria-label="Close" data-dismiss="alert" type="button"><span aria-hidden="true">×</span><span class="sr-only">Close</span></button></div>',
          );
        }
      }
    }
    Novalnet.closeChildWindow();
    MD.onlinePayment.unbindNovalnetEventListener();
  },

  bindNovalnetEventListener: function () {
    window.addEventListener(
      "message",
      MD.onlinePayment.NovalnetResponseEventHandler,
      false,
    );
  },

  unbindNovalnetEventListener: function () {
    window.removeEventListener(
      "message",
      MD.onlinePayment.NovalnetResponseEventHandler,
      false,
    );
  },
};
```