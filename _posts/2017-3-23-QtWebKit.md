---
layout: post
title: QtWebKit使用问题总结
---

## 查找QWebElement方法
QWebElement loginLink = frame->findFirstElement("TEXT");
* 如果有id,可以使用TEXT = #id,更严格加标签名使用TEXT = input#id,更加严格加参数TEXT = input[type=text]#id 
* 没有id，比如文字链接，可以使用TEXT = a,更严格TEXT = a[href="xxx"],从源码中寻找

## 激活一个java script操作，比如按钮等
直接使用evaluateJavaScript("this.click()")即可
```c++
    QWebElement topSearchTB = frame->findFirstElement("input[type=submit]#find_top");
    topSearchTB.evaluateJavaScript("this.click()");
```

## 激活一个链接，a标签的超链接
上面的方法不起作用，需要使用
```javascript
evaluateJavaScript("var evObj = document.createEvent('MouseEvents');evObj.initEvent('click', true, true);this.dispatchEvent(evObj);")
```
例子：
```c++
    QWebElement newLink = frame->findFirstElement("a[href=\"enter_bug.cgi\"]");
    qDebug()<<newLink.isNull()<<newLink.toPlainText();
    //qDebug()<<newLink.evaluateJavaScript("var evObj = document.createEvent('MouseEvents');evObj.initEvent('click', true, true);this.dispatchEvent(evObj);");

    //QWebElement loginLink = frame->findFirstElement("a#login_link_top");
    //qDebug()<<loginLink.isNull()<<loginLink.toPlainText();
    //loginLink.setFocus();
    //qDebug()<<loginLink.evaluateJavaScript("this.click()");
    qDebug()<<loginLink.evaluateJavaScript("var evObj = document.createEvent('MouseEvents');evObj.initEvent('click', true, true);this.dispatchEvent(evObj);");
```
