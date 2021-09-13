# sqlmap使用入门

## 环境

```
```

## 参数

**选项**

|参数|说明|
|----|----|
|-h,--help||
|-hh||
|--version||
|-v VERBOSE||

**目标**
|-u URL, --url=URL||
|-d DIRECT        ||
|-l LOGFILE       ||
|-m BULKFILE      ||
|-r REQUESTFILE   ||
|-g GOOGLEDORK    ||
|-c CONFIGFILE    ||



**qq**

|-A AGENT, --user..||
|-H HEADER, --hea..||
|--method=METHOD   ||
|--data=DATA       ||
|--param-del=PARA..||
|--cookie=COOKIE   ||
|--cookie-del=COO..||
|--live-cookies=L..||
|--load-cookies=L..||
|--drop-set-cookie ||
|--mobile          ||
|--random-agent    ||
|--host=HOST       ||
|--referer=REFERER ||
|--headers=HEADERS ||
|--auth-type=AUTH..||
|--auth-cred=AUTH..||
|--auth-file=AUTH..||
|--ignore-code=IG..||
|--ignore-proxy    ||
|--ignore-redirects||
|--ignore-timeouts ||
|--proxy=PROXY     ||
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

|-o               ||
|--predict-output ||
|--keep-alive     ||
|--null-connection||
|--threads=THREADS||

**jj**

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
|--technique=TECH..||
|--time-sec=TIMESEC||
|--union-cols=UCOLS||
|--union-char=UCHAR||
|--union-from=UFROM||
|--dns-domain=DNS..||
|--second-url=SEC..||
|--second-req=SEC..||

**ss**
|-f, --fingerprint||

****

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

|--common-tables ||
|--common-columns||
|--common-files  ||

****
|--udf-inject      ||
|--shared-lib=SHLIB||

****

|--file-read=FILE..||
|--file-write=FIL..||
|--file-dest=FILE..||

****
|--os-cmd=OSCMD    ||
|--os-shell        ||
|--os-pwn          ||
|--os-smbrelay     ||
|--os-bof          ||
|--priv-esc        ||
|--msf-path=MSFPATH||
|--tmp-path=TMPPATH||

****
|--reg-read        ||
|--reg-add         ||
|--reg-del         ||
|--reg-key=REGKEY  ||
|--reg-value=REGVAL||
|--reg-data=REGDATA||
|--reg-type=REGTYPE||

****

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






