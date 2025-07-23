# PayerMAX Server SDK (PHP)

## Environment Preparation

```bash
composer install
```

## Initialize Config

```php
// Build parameters
$merchantConfig = new MerchantConfig();
$merchantConfig->merchantNo         = "your merchant no";
$merchantConfig->appId              = "your merchantAppId";
$merchantConfig->merchantPrivateKey = "your private key";
$merchantConfig->payermaxPublicKey  = "payermax public key";

// ISV merchant extra parameters
$merchantConfig->spMerchantNo      = "xxx";
$merchantConfig->merchantAuthToken = "xxx";

// Apply configuration
PayermaxClient::setConfig($merchantConfig);
```

## Send Request

```php
// Build the business payload
$requestData = '{
  "outTradeNo": "PAM20220109123456111617V3",
  "subject": "hello",
  "totalAmount": "0.99",
  "currency": "TRY",
  "country": "TR",
  "userId": "100000002",
  "goodsDetails": [{
    "goodsId": "60",
    "goodsName": "60 Diamonds",
    "quantity": "1",
    "price": "0.99",
    "goodsCurrency": "TRY",
    "showUrl": "http://domain.com"
  }],
  "language": "tr",
  "reference": "300011",
  "frontCallbackUrl": "https://domain.url",
  "notifyUrl": "https://domain.com"
}';

$json_decodeData = json_decode($requestData, true);

// Send the request and get the response
$resp = PayermaxClient::send('orderAndPay', $json_decodeData);
echo json_encode($resp) . "\n";
```

## Verify Notification

```php
PayermaxClient::verify("payermax request body", "payermax request sign");
```
