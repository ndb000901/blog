# sqlmap使用入门

## 环境

```
sqlmap-1.5.8.8#dev
```

## 参数

**选项**

|参数|说明|
|----|----|
|-h,--help|显示帮助信息|
|-hh|显示高级帮助信息|
|--version|显示版本|
|-v VERBOSE|验证级别：0-6默认1|

**目标**

**注意：至少使用一个参数定义目标**

|参数|说明|
|----|----|
|-u URL, --url=URL|目标url|
|-d DIRECT        |直接连接数据库的连接字符串|
|-l LOGFILE       |从burp或webScarab代理日志文件中解析目标|
|-m BULKFILE      |从文件中获取目标|
|-r REQUESTFILE   |从文件中加载http请求|
|-g GOOGLEDORK    |使用google搜索引擎|
|-c CONFIGFILE    |从配置文件INI中加载|



**请求**

|参数|说明|
|----|----|
|-A AGENT, --user..|http请求用户代理标头|
|-H HEADER, --hea..|额外的头信息|
|--method=METHOD   |http请求方式|
|--data=DATA       |通过post发送的数据|
|--param-del=PARA..|用于分割参数的字符|
|--cookie=COOKIE   |http cookie值|
|--cookie-del=COO..|用于分割cookie的字符|
|--live-cookies=L..|用于加载最新值的实时cookie文件|
|--load-cookies=L..|包含Netscape/wget格式的cookie的文件|
|--drop-set-cookie |忽略响应中的Set-Cookie头信息|
|--mobile          |通过http User-agent模仿智能手机|
|--random-agent    |随机User-Agent|
|--host=HOST       |http host头值|
|--referer=REFERER |http Referer头值|
|--headers=HEADERS |额外的头文件|
|--auth-type=AUTH..|http认证类型|
|--auth-cred=AUTH..|http认证凭证|
|--auth-file=AUTH..|http认证的PEM证书/私钥文件|
|--ignore-code=IG..|忽略http的错误代码|
|--ignore-proxy    |忽略系统默认的代理设置|
|--ignore-redirects|忽略重定向的尝试|
|--ignore-timeouts |忽略连接超时|
|--proxy=PROXY     |使用代理连接到目标url|
|--proxy-cred=PRO..|代理认证凭证|
|--proxy-file=PRO..|从文件加载代理|
|--proxy-freq=PRO..|从一个给定的列表更换代理|
|--tor             |使用tor匿名网络|
|--tor-port=TORPORT|设置非默认的Tor代理端口|
|--tor-type=TORTYPE|设置tor代理类型|
|--check-tor       |检查tor是否被正确使用|
|--delay=DELAY     |每次http请求延时时间单位秒|
|--timeout=TIMEOUT |默认等待时间默认30s|
|--retries=RETRIES |超时时重试默认3|
|--randomize=RPARAM|随机改变给定参数值|
|--safe-url=SAFEURL|测试期间经常访问的url地址|
|--safe-post=SAFE..|发送到安全url的post数据|
|--safe-req=SAFER..|从一个文件加载安全的http请求|
|--safe-freq=SAFE..|在访问的安全的url之间定期请求|
|--skip-urlencode  |跳过有效payload的url编码|
|--csrf-token=CSR..|保存反CSRF令牌的参数|
|--csrf-url=CSRFURL|为提取反CSRF令牌而访问的url地址|
|--csrf-method=CS..|在反CSRF令牌页面访问时使用的HTTP方法|
|--csrf-retries=C..|反CSRF令牌检索的重试次数默认0|
|--force-ssl       |强制使用SSL/HTTPS|
|--chunked         |使用HTTP分块传输编码（POST）请求|
|--hpp             |使用HTTP参数污染方法|
|--eval=EVALCODE   |在请求前评估所提供的Python代码|

**优化**

|参数|说明|
|----|----|
|-o               |开启所有的优化开关|
|--predict-output |预测常见的查询输出|
|--keep-alive     |使用持久的HTTP(s)连接|
|--null-connection|检索没有实际HTTP响应体的页面长度|
|--threads=THREADS|最大的HTTP(s)并发请求数（默认为1）|

**注入**

|参数|说明|
|----|----|
|-p TESTPARAMETER  |指定测试参数|
|--skip=SKIP       |跳过对指定参数的测试|
|--skip-static     |跳过测试那些看起来不是动态的参数|
|--param-exclude=..|从测试中排除参数的Regexp|
|--param-filter=P..|按位置选择可测试的参数(例如 "POST")|
|--dbms=DBMS       |强制后端DBMS为提供的值|
|--dbms-cred=DBMS..|DBMS认证凭证(用户：密码)|
|--os=OS           |将后端DBMS的操作系统强制为所提供的值|
|--invalid-bignum  |使用大的数字作为无效值|
|--invalid-logical |使用逻辑运算来计算无效值|
|--invalid-string  |无效值使用随机字符串|
|--no-cast         |关闭有效载荷铸造机制|
|--no-escape       |关闭字符串转义机制|
|--prefix=PREFIX   |注入有效载荷前缀字符串|
|--suffix=SUFFIX   |注入有效载荷的后缀字符串|
|--tamper=TAMPER   |使用指定的脚本来篡改注入数据|

**检测**

|参数|说明|
|----|----|
|--level=LEVEL     |检测级别(1-5，默认为1)|
|--risk=RISK       |测试的风险(1-3，默认为1)|
|--string=STRING   |当查询被评估为True时要匹配的字符串|
|--not-string=NOT..|当查询结果为False时，要匹配的字符串|
|--regexp=REGEXP   |当查询结果为 "真 "时，匹配的是Regexp|
|--code=CODE       |当查询结果为True时，匹配的HTTP代码|
|--smart           |仅当启发式方法为正时，才进行彻底测试|
|--text-only       |仅根据文本内容比较网页|
|--titles          |仅根据页面的标题进行比较|

**技术**

|参数|说明|
|----|----|
|--technique=TECH..|要使用的SQL注入技术(默认为 "BEUSTQ")|
|--time-sec=TIMESEC|延迟DBMS响应的秒数(默认为5)|
|--union-cols=UCOLS|测试UNION查询SQL注入的列的范围|
|--union-char=UCHAR|用来破解列数的字符|
|--union-from=UFROM|在UNION查询的FROM部分要使用的表|
|--dns-domain=DNS..|用于DNS渗出攻击的域名|
|--second-url=SEC..|搜索到的二阶响应的结果页面URL|
|--second-req=SEC..|从文件中加载二阶HTTP请求|

**指纹**

|参数|说明|
|----|----|
|-f, --fingerprint|进行广泛的DBMS版本指纹识别|

**枚举**

|参数|说明|
|----|----|
|-a, --all         |检索所有信息|
|-b, --banner      |检索DBMS的旗帜|
|--current-user    |检索DBMS的当前用户|
|--current-db      |检索DBMS当前数据库|
|--hostname        |检索DBMS服务器主机名|
|--is-dba          |检测DBMS当前用户是否为DBA|
|--users           |枚举DBMS用户|
|--passwords       |枚举DBMS用户的密码哈希值|
|--privileges      |枚举DBMS用户的权限|
|--roles           |枚举DBMS用户的角色|
|--dbs             |枚举DBMS的数据库|
|--tables          |枚举DBMS数据库的表|
|--columns         |枚举DBMS数据库表列|
|--schema          |枚举DBMS模式|
|--count           |检索表的条目数|
|--dump            |备份DBMS数据库表的条目|
|--dump-all        |备份所有DBMS数据库表的条目|
|--search          |搜索列、表和/或数据库名称|
|--comments        |在列举过程中检查DBMS的注释|
|--statements      |检索正在DBMS上运行的SQL语句|
|-D DB             |DBMS的数据库要进行列举|
|-T TBL            |要枚举的DBMS数据库表|
|-C COL            |要列举的DBMS数据库表列|
|-X EXCLUDE        |DBMS数据库标识符，不进行列举|
|-U USER           |要枚举的DBMS用户|
|--exclude-sysdbs  |枚举表时排除DBMS系统数据库|
|--pivot-column=P..|枢轴列名称|
|--where=DUMPWHERE |在转储表时使用WHERE条件|
|--start=LIMITSTART|要检索的第一个转储表项|
|--stop=LIMITSTOP  |检索的最后一个转储表项|
|--first=FIRSTCHAR |检索的第一个查询输出字段|
|--last=LASTCHAR   |最后一个查询输出的字词要被检索出来|
|--sql-query=SQLQ..|要执行的SQL语句|
|--sql-shell       |提示一个交互式SQL shell|
|--sql-file=SQLFILE|从给定文件中执行SQL语句|

**暴力**

|参数|说明|
|----|----|
|--common-tables |检查共通表的存在|
|--common-columns|检查共通列是否存在|
|--common-files  |检查共通文件是否存在|

**用户定义的函数注入**

|参数|说明|
|----|----|
|--udf-inject      |注入自定义用户定义的函数|
|--shared-lib=SHLIB|共享库的本地路径|

**文件系统访问**

|参数|说明|
|----|----|
|--file-read=FILE..|从后端数据库管理系统的文件系统中读取一个文件|
|--file-write=FIL..|在后端DBMS文件系统上写一个本地文件|
|--file-dest=FILE..|写入到后端DBMS的绝对文件路径|

**操作系统访问**

|参数|说明|
|----|----|
|--os-cmd=OSCMD    |执行一个操作系统的命令|
|--os-shell        |提示一个交互式的操作系统shell|
|--os-pwn          |提示OOB shell、Meterpreter或VNC|
|--os-smbrelay     |一键提示OOB shell、Meterpreter或VNC|
|--os-bof          |存储程序缓冲区溢出的利用|
|--priv-esc        |数据库进程用户的权限升级|
|--msf-path=MSFPATH|安装Metasploit框架的本地路径|
|--tmp-path=TMPPATH|临时文件目录的远程绝对路径|

**Windows注册表访问**

|参数|说明|
|----|----|
|--reg-read        |读取一个Windows注册表的键值|
|--reg-add         |写一个Windows注册表的键值数据|
|--reg-del         |删除一个Windows注册表键值|
|--reg-key=REGKEY  |Windows注册表键|
|--reg-value=REGVAL|Windows注册表值|
|--reg-data=REGDATA|Windows注册表键值数据|
|--reg-type=REGTYPE|Windows注册表键值类型|

**常规**

|参数|说明|
|----|----|
|-s SESSIONFILE    |从存储的（.sqlite）文件加载会话|
|-t TRAFFICFILE    |将所有HTTP流量记录到一个文本文件中|
|--answers=ANSWERS |设置预定义的答案（例如，"quit=N,follow=N"）|
|--base64=BASE64P..|包含Base64编码数据的参数(s)|
|--base64-safe     |使用URL和文件名安全的Base64字母(RFC 4648)|
|--batch           |从不要求用户输入，使用默认行为|
|--binary-fields=..|具有二进制值的结果字段（例如 "摘要"）|
|--check-internet  |在评估目标之前检查互联网连接情况|
|--cleanup         |从sqlmap特定的UDF和表清理DBMS|
|--crawl=CRAWLDEPTH|从目标URL开始抓取网站|
|--crawl-exclude=..|从抓取中排除网页的Regexp（例如："logout"）|
|--csv-del=CSVDEL  |在CSV输出中使用的定界字符（默认为","）|
|--charset=CHARSET |SQL盲注字符集|
|--dump-format=DU..|转储数据的格式（CSV（默认），HTML或SQLITE）|
|--encoding=ENCOD..|用于数据检索的字符编码（如GBK）|
|--eta             |为每个输出显示估计的到达时间|
|--flush-session   |为当前目标刷新会话文件|
|--forms           |解析并测试目标URL上的表单|
|--fresh-queries   |忽略会话文件中存储的查询结果|
|--gpage=GOOGLEPAGE|用指定页数的Google dork结果|
|--har=HARFILE     |将所有的HTTP流量记录到一个HAR文件中|
|--hex             |在数据检索时使用十六进制转换|
|--output-dir=OUT..|自定义输出目录路径|
|--parse-errors    |解析并显示响应中的DBMS错误信息|
|--preprocess=PRE..|使用给定的脚本进行预处理(请求)|
|--postprocess=PO..|使用给定的脚本进行后处理(响应)|
|--repair          |重置有未知字符标记的条目|
|--save=SAVECONFIG |将选项保存到配置INI文件中|
|--scope=SCOPE     |用于过滤目标的Regexp|
|--skip-heuristics |跳过对漏洞的启发式检测|
|--skip-waf        |跳过对WAF/IPS保护的启发式检测|
|--table-prefix=T..|用于临时表的前缀（默认是 "sqlmap"）|
|--test-filter=TE..|通过有效载荷和/或标题（例如ROW）选择测试|
|--test-skip=TEST..|通过有效载荷和/或标题跳过测试（例如，BENCHMARK）|
|--web-root=WEBROOT|网络服务器文件根目录（例如"/var/www"）|



**其他**

|参数|说明|
|----|----|
|-z MNEMONICS      |使用简短的助记符（例如："flu,bat,ban,tec=EU"）|
|--alert=ALERT     |当发现有SQL注入时，运行主机操作系统命令|
|--beep            |遇到问题或发现漏洞时发出提示音|
|--dependencies    |检查缺失的（可选）sqlmap依赖项|
|--disable-coloring|禁用控制台输出的颜色|
|--list-tampers    |显示可用的篡改脚本的列表|
|--offline         |在离线模式下工作（只使用会话数据）|
|--purge           |安全地删除sqlmap数据目录中的所有内容|
|--results-file=R..|多目标模式下CSV结果文件的位置|
|--shell           |提示一个交互式的sqlmap shell|
|--tmp-dir=TMPDIR  |用于存储临时文件的本地目录|
|--unstable        |为不稳定的连接调整选项|
|--update          |更新sqlmap|
|--wizard          |为初级用户提供简单的向导界面|






