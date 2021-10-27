# shiro使用

## 创建工程

**maven**

```
        <dependency>
            <groupId>org.apache.shiro</groupId>
            <artifactId>shiro-core</artifactId>
            <version>1.8.0</version>
        </dependency>

```



# Demo

## demo1--->第一个程序用户认证

**maven**

```
        <dependency>
            <groupId>org.apache.shiro</groupId>
            <artifactId>shiro-core</artifactId>
            <version>1.8.0</version>
        </dependency>
```

**resources/shiro.ini**

模拟帐号密码

```
[users]
haha=123456
jiji=abcdef
```

**TestAuthenticator.java**

```
package xyz.wuhen.shiro.demo1;

import org.apache.shiro.SecurityUtils;
import org.apache.shiro.authc.IncorrectCredentialsException;
import org.apache.shiro.authc.UnknownAccountException;
import org.apache.shiro.authc.UsernamePasswordToken;
import org.apache.shiro.mgt.DefaultSecurityManager;
import org.apache.shiro.realm.text.IniRealm;
import org.apache.shiro.subject.Subject;


public class TestAuthenticator {

    public static void main(String[] args) {
        // 创建安全管理器对象
        DefaultSecurityManager securityManager = new DefaultSecurityManager();
        //给安全管理器设置realm
        securityManager.setRealm(new IniRealm("classpath:shiro.ini"));
        //SecurityUtils 给全局安全工具类设置安全管理器
        SecurityUtils.setSecurityManager(securityManager);
        //关键对象subject主体
        Subject subject = SecurityUtils.getSubject();
        //创建令牌
        UsernamePasswordToken token = new UsernamePasswordToken("1","1213456");


        try {
            subject.login(token);
        } catch (IncorrectCredentialsException e) {
            System.out.println("密码错误");
        } catch (UnknownAccountException e) {
            System.out.println("没有该用户");
        }

    }
}

```

**认证流程**

```
认证：
    1、用户名比较 SimpleAccountRealm-->doGetAuthenticationInfo
    2、密码校验   AuthenticatingRealm-->assertCredentialsMatch
    
AuthenticatingRealm  认证 doGetAuthenticationInfo
AuthorizingRealm     授权 doGetAuthorizationInfo
```
