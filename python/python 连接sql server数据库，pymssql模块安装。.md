## python 连接sql server数据库，pymssql模块安装。

>python版本：python3.7
>
>数据库版本：sql server 2016

连接sql server数据库，本菜鸟用的是pymssql，现在我得着重说下pymssql的安装问题。

**安装pymssql解决方案**

往常使用滴pip install pymssql可能行不通（你可以去试试，反正我滴机子不行）。

**资源下载** [pymssql下载](https://pypi.org/project/pymssql/#files)
选择自己需要滴版本

![image](https://user-images.githubusercontent.com/48900845/112761694-0794ff80-902f-11eb-8561-d8e1a2d3d6a4.png)

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

>作者info
>
>作者：DebugWuhen
>
>原创公众号：『DebugWuhen』，新号，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
>
>转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
>
>![image](https://user-images.githubusercontent.com/48900845/112752163-3b0e6480-9004-11eb-899d-66ddef749c2b.png)
