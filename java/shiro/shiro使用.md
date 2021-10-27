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



## demo2-->自定义Realm


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

**CustomerRealm.java**


```
package xyz.wuhen.shiro.demo2;

import org.apache.shiro.authc.AuthenticationException;
import org.apache.shiro.authc.AuthenticationInfo;
import org.apache.shiro.authc.AuthenticationToken;
import org.apache.shiro.authc.SimpleAuthenticationInfo;
import org.apache.shiro.authz.AuthorizationInfo;
import org.apache.shiro.realm.AuthorizingRealm;
import org.apache.shiro.subject.PrincipalCollection;

public class CustomerRealm extends AuthorizingRealm {

    //认证方法
    @Override
    protected AuthorizationInfo doGetAuthorizationInfo(PrincipalCollection principals) {
        return null;
    }

    //授权方法
    @Override
    protected AuthenticationInfo doGetAuthenticationInfo(AuthenticationToken token) throws AuthenticationException {
        //获取用户名
        String principal = (String) token.getPrincipal();
        System.out.println("username--->" + principal);

        if ("haha".equals(principal)) {
            //p1->用户名
            //p2->密码
            //p3->Realm名字
            String username = "haha";
            String passwd = "1234561";

            SimpleAuthenticationInfo simpleAuthenticationInfo = new SimpleAuthenticationInfo(username,passwd,this.getName());
            return simpleAuthenticationInfo;
        }

        return null;
    }
}

```

**TestCustomerRealm.java**

```
package xyz.wuhen.shiro.demo2;

import org.apache.shiro.SecurityUtils;
import org.apache.shiro.authc.IncorrectCredentialsException;
import org.apache.shiro.authc.UnknownAccountException;
import org.apache.shiro.authc.UsernamePasswordToken;
import org.apache.shiro.mgt.DefaultSecurityManager;
import org.apache.shiro.subject.Subject;

public class TestCustomerRealm {
    public static void main(String[] args) {
        DefaultSecurityManager securityManager = new DefaultSecurityManager();
        securityManager.setRealm(new CustomerRealm());
        SecurityUtils.setSecurityManager(securityManager);

        Subject subject = SecurityUtils.getSubject();
        UsernamePasswordToken token = new UsernamePasswordToken("haha","123456");

        subject.login(token);

        try {

        } catch (UnknownAccountException e) {
            e.printStackTrace();
        } catch (IncorrectCredentialsException e) {
            e.printStackTrace();
        }
    }
}

```


## demo3--->MD5加密demo

**TestShiroMD5.java**

```
package xyz.wuhen.shiro.demo3;

import org.apache.shiro.crypto.hash.Md5Hash;

public class TestShiroMD5 {
    public static void main(String[] args) {

        // md5加密
        Md5Hash md5Hash = new Md5Hash("1234");
        System.out.println(md5Hash.toHex());
        //md5 + salt
        Md5Hash md5Hash1 = new Md5Hash("1234","sjshhsx");
        System.out.println(md5Hash1.toHex());

        //md5 + salt + hash散列
        Md5Hash md5Hash2 = new Md5Hash("1234","sjshhsx",1024);
        System.out.println(md5Hash2.toHex());
    }
}

```
