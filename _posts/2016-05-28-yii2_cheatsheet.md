---
layout: post
title:  "yii cheatsheet"
date:   2016-05-28 14:13:36 +0800
categories: php
tags: yii2
---

### exception 处理
如果异常是继承 yii\base\UserException，不管YII_DEBUG为何值，函数调用栈信息都不会显示
这是因为这种错误会被认为是用户产生的错误，开发人员不需要修正。

### yii2 urlmanager 不支持循环跳转
url rule 不支持循环内部跳转．example
```
./      -> /index
/index  -> /defaut/index
```

### rest api /v1/notice/search

http://api.test.com/v1/notice/search?page_size=1000

it will invoke StatusController.actionSearch method.
```php
'urlManager' => [
	'enablePrettyUrl' => true,
	'enableStrictParsing' => true,
	'showScriptName' => false,
	'cache' => false,
	'rules' => [
		[
			'class' => 'yii\rest\UrlRule',
			'controller' => [
				'v1/notice'
			],
			'extraPatterns' => [
				'GET search' => 'search'
			]
		],
		'v1/<entity:xxx>-status' => 'v1/status'
	]
]
```
