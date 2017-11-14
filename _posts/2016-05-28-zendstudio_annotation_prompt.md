---
layout: post
title:  "zendstudio annotation prompt"
date:   2016-05-28 14:13:36 +0800
categories: php
---
##zendstudio 行内注释， 显式声明变量类型，让变量支持自动方法提示

```php
$out = [];
/* @var $row \xxyy\SizeEntity */
foreach ($rows['list'] as $row) {
    $out['list'][] = [
        'width' => $row->getWidth(),
        'height' => $row->getHeight(),
    ];
}

$out = [];
/* @var $invoice ChargeInvoice */
foreach ($response->getChargeInvoice() as $invoice) {
    $tmp = [];
    $tmp['amount'] = $invoice->getChargeAmountMicros();
    $tmp['charge_id'] = $invoice->getChargeId();
    $tmp['date'] = date('Y-m-d', $invoice->getChargeEndTimeUtc());
    $out[] = $tmp;
}
```
