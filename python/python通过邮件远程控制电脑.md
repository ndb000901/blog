## 让繁琐的工作自动化——python处理email
今天来谈一谈，如何用python处理Email。今天的示例选用QQ邮箱。
以及写个利用邮件远程控制电脑下载图片。
****


**1.环境**
>1.python3.8
>2.pyzmail36 v1.04
>3.IMAPClient v2.1.0
>4.PyEmail v0.0.1

**如果pyzmail安装报错，请安装pyzmail36。**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200809173236850.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)

**2.准备工作**

需要准备个qq邮箱，这个很容易吧。

网页登录qq邮箱，点击设置，点击账户。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200809165908597.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
开启IMAP/SMTP服务。会生成一个授权码，把它记下来，后面需要用，这玩意相当于密码。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200809165945912.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
QQ邮箱的一些信息，后面需要用
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020080917034257.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)



**3.发送邮件**

导入smtplib
```
import smtplib
```

连接到SMTP服务器，smtplib.SMTP()，第一个参数是SMTP服务器的域名，第二个是端口。
```
smtpObj = smtplib.SMTP('smtp.qq.com', 587)
```

给服务器打个招呼，问个好。
**注意：得到SMTP对象后必须调用ehlo()方法，向SMTP服务器问好。**
```
smtpObj.ehlo()
```

如果连接SMTP 587端口（使用TLS加密），需要调用starttls()；如果连接SMTP 465端口（使用SSL），加密一设置，无需使用starttls()方法，请跳过这一步。
```
smtpObj.starttls()
```

登录账号。

**注意：第一个填写邮箱，第二个填生成的授权码**
```
smtpObj.login('xxxxxx@qq.com', 'passwd')
```
发送邮件。
**注意：第一个参数填写登录的邮箱，第二个参数目的邮箱，第三个参数正文内容，必须以字符串'Subject: \n'开头，作为邮件的主题行，'\n'将正文与主题分割。**
```
smtpObj.sendmail('你的邮箱','目的邮箱','Subject: haha\nhello,nie.')
```

与SMTP服务器断开。
```
smtpObj.quit()
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200809172951172.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)

**4.获取邮件与删除邮件**

导入模块
```
import pyzmail
import imapclient
import imaplib
```

连接IMAP服务器，imapclient.IMAPClient（）方法第一个参数IMAP服务器域名，第二个参数开启SSL加密（大多数邮件提供商要求开启SSL加密）
```
imapObj = imapclient.IMAPClient('imap.qq.com', ssl=True)
```
登录到IMAP服务器
**注意：第一个参数你滴邮箱，第二个参数生成的授权码**
```
imapObj.login('xxxxxxx@qq.com', 'passwd')
```

选择文件夹，文件夹有很多，可以通过list_folders()方法获取文件夹列表（返回元组类型）。
```
list1 = imapObj.list_folders()

```
**注意：我为了输出好看，导入了pprint模块，调用pprint.pprint(list1)输出**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200809174516807.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)

选择文件夹，一般都有‘INBOX’(收件箱)这个文件夹，readonly是只读，如果你的程序不需删除邮件，建议将该参数设置为True。
```
imapObj.select_folder('INBOX', readonly=True)
```
搜索，search()方法参数是字符串列表文末附录查看搜索键。该方法返回消息ID列表。

```
MIds = imapObj.search(['ALL'])
```
**注意：若你的搜索有大量数据，python会抛出异常，请加入以下代码，数字代表最大字节数**
```
import imaplib
imaplib._MAXLINE = 100000000
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200809180543656.png)
获取电子邮件内容，以下代码获取了4个eamil的信息。
```
msgList = imapObj.fetch(MIds, ['BODY[]'])
```

获取电子邮件的一些信息，为了操作简洁，先导入pyzmail模块，创建PyzMessage对象，使解析电子邮件变得更方便。

```
import pyzmail
msg = pyzmail.PyzMessage.factory(msgList[10][b'BODY[]'])
```
获取主题
```
subject = msg.get_subject()
```
获取地址
**注意：'from' 可替换为'to','cc','bcc'。cc指抄送，bcc指密送。**

```
addr = msg.get_addresses('from')
```

获取正文，email可以是纯文本或HTML的混合，若email只含纯文本PyzMwssage对象的html_part设置为None；若email只含HTML，PyzMwssage对象的text_part设置为None。
```
if msg.text_part != None:
	text = msg.text_part.get_payload().decode(msg.text_part.charset)
if msg.html_part != None:
	html = msg.html_part.get_payload().decode(msg.html_part.charset)
```

删除电子邮件
```
imapObj.select_folder('INBOX', readonly=False)
imapObj.delete_messages(消息ID)
```

与IMAP服务器断开
```
imapObj.logout()
```

****

## 实例——实现通过邮件远程控制电脑下载图片。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200809202204376.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
这不就下载好了吗
![](https://img-blog.csdnimg.cn/20200809202327537.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
**注意：本例子写得太过于粗糙，有太多的问题需要修改。仅仅是为大家演示一种使用思路。**


**源码**

```
import imaplib
import pyzmail
import imapclient
import time
import requests


def download(urls):
    for url in urls:
        res = requests.get(url.replace('&amp;', '&'))
        with open(str(time.time()) + '.jpg', 'wb') as file:
            file.write(res.content)


def checknewpic():

    imapObj = imapclient.IMAPClient('imap.qq.com', ssl=True)
    imapObj.login('xxxxx@qq.com', 'passwd')
    print(imapObj.select_folder('INBOX', readonly=True))
    MIds = imapObj.search(['ALL'])
    msgList = imapObj.fetch(MIds, ['BODY[]'])
    for id in MIds:
        msg = pyzmail.PyzMessage.factory(msgList[id][b'BODY[]'])
        if msg.get_subject() == "下载图片":
            if msg.text_part != None:
                urls = msg.text_part.get_payload().decode(msg.text_part.charset).split('^')
                download(urls)

while True:
    checknewpic()
    time.sleep(60)
print('---------执行完毕-----------')

```






****

## 附录
'ALL'：返回该文件夹中的所有邮件。如果你请求一个大文件夹中的所有信息，可能会遇到imaplib的大小限制

'BEFORE/ON/SINCE date'：分别返回给定的date之前、当天、之后IMAP服务器接受的消息，日期格式必须是01-Jul-2020
此外，虽然“SINCE 01-Jul-2020”将匹配7月1日当天和之后的消息，但是“BEFORE 01-Jul-2020”仅匹配7月1日之前的消息，不包括7月1日当天

'SUBJECT/BODY/TEXT string':分别返回string出现在主题、正文、主题或正文中的消息，如果string中有空格，就是用双引号

'FROM/TO/CC/BCC string':返回所有信息，其中string分别出现在“from”邮件地址、“to”邮件地址、“cc”（抄送）地址、或“bcc”（密件抄送）地址
如果string中有多个邮件地址，就是用空格将他们分割开，并使用双引号

'SEEN/UNSEEN'：分别返回包含和不包含\Seen标记的所有信息。如果电子邮件已经被fetch()方法调用访问，或者你曾在电子邮件程序中或网络浏览器中点击过它，
就会有\Seen标记，比较常用的说法是“已读”而不是“已看”

'ANSWERED/UNANSERED':分别返回包含和不包含\Answered标记的所有信息，如果消息已答复就会有\Answered标记

'DELERED/UNDELETED':分别返回包含和不包含\Deleted标记的所有信息，用delete_messages()方法删除的邮件就会有\Deleted标记，直到调用expunge()方法才
会永久删除

'DRAFT/UNDRAFT'：分别返回包含和不包含\Draft标记的所有信息，草稿邮件通常保存在单独的草稿文件夹中，而不是收件箱

'FLAGGED/UNFLAGGED'：分别返回包含和不包含\Flagged标记的所有信息，这个标记通常用来标记电子邮件的“重要”或“紧急”

'LARGER/SMALLER N'：分别返回大于或小于N个字节的所有信息

'NOT search-key':返回搜索键不会返回的那些信息

'OR search-key1 search-key2':返回符合第一个或者第二个搜索键的信息



>作者info
作者：DebugWuhen
原创公众号：『DebugWuhen』，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706013520101.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)



