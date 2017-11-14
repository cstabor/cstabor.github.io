
sudo dnf install jq
Failed to open: /var/cache/dnf/x86_64/7/x86_64/7/epel/repodata/063d487dcd0c4b4488b7e70a43850e3e4b5ecaa684973ad7ee8a61341a01d0e4-updateinfo.xml.bz2.


```php
$o = new ContentStruct();
var_dump($o);
var_dump($o->getContentImageTextDesc());

```
output
```
object(ydsp\common\proto\biz\ContentStruct)#581 (4) {
  ["content_text":protected]=>
  NULL
  ["content_image":protected]=>
  NULL
  ["content_image_text":protected]=>
  NULL
  ["content_image_text_desc":protected]=>
  NULL
}
object(ydsp\common\proto\biz\ImageTextDesc)#582 (3) {
  ["asset_id":protected]=>
  NULL
  ["headline":protected]=>
  string(0) ""
  ["description":protected]=>
  string(0) ""
}
```
## svn

查看两个版本之间的差异

svn di -r 4013:4012 services/CampaignService.php

显示某个版本的具体信息

svn log -v -r 4013 services/CampaignService.php


## charles 抓包打断点
1. 选中包，右键，选中 `Breakpoints`.
2. 选中包，右键，`Repeat`.
3. 选中左上角的 session Tab 右边的 Breakpoints Tab　修改包内容.
4. 点击屏幕下方的　execute，两次即可，　第一次修改请求包结构，第二次修改返回包结构．

start: 2016-01-05 16:44
copy result:  0
copy back finished
 ERROR! MySQL server PID file could not be found!
 Starting MySQL................ ERROR! The server quit without updating PID file (/data/mysql/mysqld.pid).
 finish:  2016-01-05 16:51
