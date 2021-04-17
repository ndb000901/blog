## C# 读写json文件

实验环境：VS2017（宇宙最最屌IDE）

**1.安装Newtonsoft.Json**

![image](https://user-images.githubusercontent.com/48900845/115116802-2f440b80-9fce-11eb-8ba2-f018cbc7c933.png)

```
在控制台输入，回车。
Install-Package Newtonsoft.Json
```

![image](https://user-images.githubusercontent.com/48900845/115116818-41be4500-9fce-11eb-9def-fe2cf1374bbf.png)


然后在所需的项目添加引用。

![image](https://user-images.githubusercontent.com/48900845/115116824-4daa0700-9fce-11eb-9c0f-328ba748522d.png)

![image](https://user-images.githubusercontent.com/48900845/115116830-539fe800-9fce-11eb-9506-8fd3e31cbe8e.png)

找到安装目录选择相应版本。

**2.新建一个config.json文件。(名字各位大爷随意)**

```
{
  "server": ".",
  "user": "sa",
  "passwd": "n123456"
}
```

**3.Read**

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Configuration;
//记得引用这几个玩意
using Newtonsoft.Json;
using Newtonsoft.Json.Linq;
using System.IO;

namespace 操作json与xml
{
    class ReadJson
    {
        public static string Get_server()
        {
        	try
            {
            	StreamReader reader = File.OpenText("config.json");
            	JsonTextReader jsonTextReader = new JsonTextReader(reader);
           	 	JObject jsonObject = (JObject)JToken.ReadFrom(jsonTextReader);
            	string server = jsonObject["server"].ToString(); //user ,passwd 类似
            	reader.Close();
            	return server;
            }
            catch
            {
            	//自己加点
            }
        }
    }
}



```

**4.Write**

```
	public static void Set_server(string server)
        {
        	try
            {
            	StreamReader reader = File.OpenText("config.json");
            	JsonTextReader jsonTextReader = new JsonTextReader(reader);
           	 	JObject jsonObject = (JObject)JToken.ReadFrom(jsonTextReader);
            	jsonObject["server"] = server; //user ,passwd 类似
            	reader.Close();
            	string output = Newtonsoft.Json.JsonConvert.SerializeObject(jsonObject, Newtonsoft.Json.Formatting.Indented);
                File.WriteAllText("config.json", output);
            }
            catch
            {
            	//自己加点
            }
        }

```

>作者info
>
>作者：DebugWuhen
>
>原创公众号：『DebugWuhen』，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
>
>转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
>
>![image](https://user-images.githubusercontent.com/48900845/112752163-3b0e6480-9004-11eb-899d-66ddef749c2b.png)

