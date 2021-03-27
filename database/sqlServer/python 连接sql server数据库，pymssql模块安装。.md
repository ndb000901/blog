## python 连接sql server数据库，pymssql模块安装。
python版本：python3.7
数据库版本：sql server 2016

连接sql server数据库，本菜鸟用的是pymssql，现在我得着重说下pymssql的安装问题。

**安装pymssql解决方案**

往常使用滴pip install pymssql可能行不通（你可以去试试，反正我滴机子不行）。

**资源下载** [pymssql下载](https://pypi.org/project/pymssql/#files)
选择自己需要滴版本
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200402161638439.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
下载后直接在当前目录执行
```
 pip install 包名
```

**连接数据库**

```
import pymssql
class MSSQL:
    def __init__(self,host,user,pwd,db):
        self.host = host
        self.user = user
        self.pwd = pwd
        self.db = db

    def __GetConnect(self):
        if not self.db:
            raise(NameError,"没有设置数据库信息")
        self.conn = pymssql.connect(host=self.host,user=self.user,password=self.pwd,database=self.db,charset="utf8")
        cur = self.conn.cursor()
        if not cur:
            raise(NameError,"连接数据库失败")
        else:
            return cur

    def ExecQuery(self,sql):
        cur = self.__GetConnect()
        cur.execute(sql)
        resList = cur.fetchall()

        #查询完毕后必须关闭连接
        self.conn.close()
        return resList

    def ExecNonQuery(self,sql):
        cur = self.__GetConnect()
        cur.execute(sql)
        self.conn.commit()
        self.conn.close()


#根据自己的实际情况进行配置
ms = MSSQL(host="127.0.0.1",user="sa",pwd="123456",db="haha")
sqlStr = 'select * from jokes'
list = ms.ExecQuery(sqlStr.encode('utf-8'))
for i in list:
    print(i)
```
OK，连接sql server的文章就结束喽。感谢阅读。
>作者info
作者：DebugWuhen
原创公众号：『DebugWuhen』，新号，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706013330882.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)