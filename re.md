###这里记载了逆向部分题目的解法###
.题目一Py交易 https://cgctf.nuptsast.com/challenges#Re
题目给出了一个python的pyc文件这是python的编译中间文件，使用地址https://tool.lu/pyc/ 进行python的反编译，得到如下代码：
<code>
'''
import base64


def encode(message):
    s = ''
    for i in message:
        x = ord(i) ^ 32
        x = x + 16
        s += chr(x)

    return base64.b64encode(s)


correct = 'XlNkVmtUI1MgXWBZXCFeKY+AaXNt'
flag = ''
print 'Input flag:'
flag = raw_input()
if encode(flag) == correct:
    print 'correct'
else:
    print 'wrong'
'''
---
根据代码提示：编写decode代码如下：使用python3.7
'''
import base64
correct = 'XlNkVmtUI1MgXWBZXCFeKY+AaXNt'

ch=base64.b64decode(correct)
s=''
for i in ch:
	x=i-16
	x=x^32
	s+=chr(x)
print(s)
'''
得到flag nctf{d3c0mpil1n9_PyC}
