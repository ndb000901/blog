# sqlmap使用入门

## 环境

```
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
|--proxy-cred=PRO..||
|--proxy-file=PRO..||
|--proxy-freq=PRO..||
|--tor             ||
|--tor-port=TORPORT||
|--tor-type=TORTYPE||
|--check-tor       ||
|--delay=DELAY     ||
|--timeout=TIMEOUT ||
|--retries=RETRIES ||
|--randomize=RPARAM||
|--safe-url=SAFEURL||
|--safe-post=SAFE..||
|--safe-req=SAFER..||
|--safe-freq=SAFE..||
|--skip-urlencode  ||
|--csrf-token=CSR..||
|--csrf-url=CSRFURL||
|--csrf-method=CS..||
|--csrf-retries=C..||
|--force-ssl       ||
|--chunked         ||
|--hpp             ||
|--eval=EVALCODE   ||

**ss**

|参数|说明|
|----|----|
|-o               ||
|--predict-output ||
|--keep-alive     ||
|--null-connection||
|--threads=THREADS||

**jj**

|参数|说明|
|----|----|
|-p TESTPARAMETER  ||
|--skip=SKIP       ||
|--skip-static     ||
|--param-exclude=..||
|--param-filter=P..||
|--dbms=DBMS       ||
|--dbms-cred=DBMS..||
|--os=OS           ||
|--invalid-bignum  ||
|--invalid-logical ||
|--invalid-string  ||
|--no-cast         ||
|--no-escape       ||
|--prefix=PREFIX   ||
|--suffix=SUFFIX   ||
|--tamper=TAMPER   ||

**kk**

|参数|说明|
|----|----|
|--level=LEVEL     ||
|--risk=RISK       ||
|--string=STRING   ||
|--not-string=NOT..||
|--regexp=REGEXP   ||
|--code=CODE       ||
|--smart           ||
|--text-only       ||
|--titles          ||

**aa**

|参数|说明|
|----|----|
|--technique=TECH..||
|--time-sec=TIMESEC||
|--union-cols=UCOLS||
|--union-char=UCHAR||
|--union-from=UFROM||
|--dns-domain=DNS..||
|--second-url=SEC..||
|--second-req=SEC..||

**ss**

|参数|说明|
|----|----|
|-f, --fingerprint||

****

|参数|说明|
|----|----|
|-a, --all         ||
|-b, --banner      ||
|--current-user    ||
|--current-db      ||
|--hostname        ||
|--is-dba          ||
|--users           ||
|--passwords       ||
|--privileges      ||
|--roles           ||
|--dbs             ||
|--tables          ||
|--columns         ||
|--schema          ||
|--count           ||
|--dump            ||
|--dump-all        ||
|--search          ||
|--comments        ||
|--statements      ||
|-D DB             ||
|-T TBL            ||
|-C COL            ||
|-X EXCLUDE        ||
|-U USER           ||
|--exclude-sysdbs  ||
|--pivot-column=P..||
|--where=DUMPWHERE ||
|--start=LIMITSTART||
|--stop=LIMITSTOP  ||
|--first=FIRSTCHAR ||
|--last=LASTCHAR   ||
|--sql-query=SQLQ..||
|--sql-shell       ||
|--sql-file=SQLFILE||

****

|参数|说明|
|----|----|
|--common-tables ||
|--common-columns||
|--common-files  ||

****

|参数|说明|
|----|----|
|--udf-inject      ||
|--shared-lib=SHLIB||

****


|参数|说明|
|----|----|
|--file-read=FILE..||
|--file-write=FIL..||
|--file-dest=FILE..||

****

|参数|说明|
|----|----|
|--os-cmd=OSCMD    ||
|--os-shell        ||
|--os-pwn          ||
|--os-smbrelay     ||
|--os-bof          ||
|--priv-esc        ||
|--msf-path=MSFPATH||
|--tmp-path=TMPPATH||

****

|参数|说明|
|----|----|
|--reg-read        ||
|--reg-add         ||
|--reg-del         ||
|--reg-key=REGKEY  ||
|--reg-value=REGVAL||
|--reg-data=REGDATA||
|--reg-type=REGTYPE||

****

|参数|说明|
|----|----|
|-s SESSIONFILE    ||
|-t TRAFFICFILE    ||
|--answers=ANSWERS ||
|--base64=BASE64P..||
|--base64-safe     ||
|--batch           ||
|--binary-fields=..||
|--check-internet  ||
|--cleanup         ||
|--crawl=CRAWLDEPTH||
|--crawl-exclude=..||
|--csv-del=CSVDEL  ||
|--charset=CHARSET ||
|--dump-format=DU..||
|--encoding=ENCOD..||
|--eta             ||
|--flush-session   ||
|--forms           ||
|--fresh-queries   ||
|--gpage=GOOGLEPAGE||
|--har=HARFILE     ||
|--hex             ||
|--output-dir=OUT..||
|--parse-errors    ||
|--preprocess=PRE..||
|--postprocess=PO..||
|--repair          ||
|--save=SAVECONFIG ||
|--scope=SCOPE     ||
|--skip-heuristics ||
|--skip-waf        ||
|--table-prefix=T..||
|--test-filter=TE..||
|--test-skip=TEST..||
|--web-root=WEBROOT||



****

|参数|说明|
|----|----|
|-z MNEMONICS      ||
|--alert=ALERT     ||
|--beep            ||
|--dependencies    ||
|--disable-coloring||
|--list-tampers    ||
|--offline         ||
|--purge           ||
|--results-file=R..||
|--shell           ||
|--tmp-dir=TMPDIR  ||
|--unstable        ||
|--update          ||
|--wizard          ||






