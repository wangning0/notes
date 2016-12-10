## 跨站脚本攻击(XSS)
* xss攻击，指黑客通过‘HTML注入’篡改了网页，插入了恶意的脚本，从而在用户浏览网页时，控制用户浏览器的一种攻击。
* xss分类：
    * 反射型，只是简单的把用户输入的数据“反射”给浏览器，黑客往往需要诱导用户“点击”一个恶意的链接
    * 存储型，会把用户输入的数据“存储”在服务器端，这种xss具有很强的稳定性，黑客写入含有恶意js代码的文章，发表后，存储在服务端
    * DOM Based XSS，通过修改页面的dom节点形成的XSS
* xss的防御：
    * httponly，浏览器禁止页面的js访问cookie
    * 输入检查
    * 输出检查
