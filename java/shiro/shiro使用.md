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


## demo4--->shiro MD5加密

**CustomerMd5Realm.java**

```
package xyz.wuhen.shiro.demo4;

import org.apache.shiro.authc.AuthenticationException;
import org.apache.shiro.authc.AuthenticationInfo;
import org.apache.shiro.authc.AuthenticationToken;
import org.apache.shiro.authc.SimpleAuthenticationInfo;
import org.apache.shiro.authz.AuthorizationInfo;
import org.apache.shiro.realm.AuthorizingRealm;
import org.apache.shiro.subject.PrincipalCollection;
import org.apache.shiro.util.ByteSource;

public class CustomerMd5Realm extends AuthorizingRealm {

    @Override
    protected AuthorizationInfo doGetAuthorizationInfo(PrincipalCollection principals) {
        return null;
    }

    @Override
    protected AuthenticationInfo doGetAuthenticationInfo(AuthenticationToken token) throws AuthenticationException {
        String principal = (String) token.getPrincipal();
        if ("haha".equals(principal)) {
            //md5
//            SimpleAuthenticationInfo simpleAuthenticationInfo =
//                    new SimpleAuthenticationInfo(principal,"e10adc3949ba59abbe56e057f20f883e",this.getName());
            // md5 + salt
            SimpleAuthenticationInfo simpleAuthenticationInfo =
                    new SimpleAuthenticationInfo(principal,"4fdf0ba83c7a7e128f35a1f4b78b35ba", ByteSource.Util.bytes("sjshhsx"),this.getName());
            return simpleAuthenticationInfo;
        }
        return null;
    }
}

```

**TestCustomerMd5RealmAuthenicator.java**

```
package xyz.wuhen.shiro.demo4;

import org.apache.shiro.SecurityUtils;
import org.apache.shiro.authc.IncorrectCredentialsException;
import org.apache.shiro.authc.UnknownAccountException;
import org.apache.shiro.authc.UsernamePasswordToken;
import org.apache.shiro.authc.credential.HashedCredentialsMatcher;
import org.apache.shiro.mgt.DefaultSecurityManager;
import org.apache.shiro.subject.Subject;


public class TestCustomerMd5RealmAuthenicator {
    public static void main(String[] args) {
        DefaultSecurityManager securityManager = new DefaultSecurityManager();
        CustomerMd5Realm customerMd5Realm = new CustomerMd5Realm();
        HashedCredentialsMatcher matcher = new HashedCredentialsMatcher();

        //设置算法
        matcher.setHashAlgorithmName("md5");
        //设置散列次数
        matcher.setHashIterations(1024);
        //设置hash凭证匹配器
        customerMd5Realm.setCredentialsMatcher(matcher);
        securityManager.setRealm(customerMd5Realm);

        SecurityUtils.setSecurityManager(securityManager);


        Subject subject = SecurityUtils.getSubject();

        //认证
        UsernamePasswordToken token = new UsernamePasswordToken("haha","123456");
        try {
            subject.login(token);
        } catch (UnknownAccountException e) {
            e.printStackTrace();
        } catch (IncorrectCredentialsException e) {
            e.printStackTrace();
        }
    }
}

```


## demo5-->授权方式

**基于角色的访问控制**

```
if (subject.hasRole("admin")) {
}
```

**基于资源的访问控制**

```
if(subject.isPermission("user:update:01")) { //资源实例

}

if(subject.isPermission("user:update:*")) {  //资源类型

}

```

## demo6-->授权

**TestCustomerMd5RealmAuthenicator.java**

```
package xyz.wuhen.shiro.demo4;

import org.apache.shiro.SecurityUtils;
import org.apache.shiro.authc.IncorrectCredentialsException;
import org.apache.shiro.authc.UnknownAccountException;
import org.apache.shiro.authc.UsernamePasswordToken;
import org.apache.shiro.authc.credential.HashedCredentialsMatcher;
import org.apache.shiro.mgt.DefaultSecurityManager;
import org.apache.shiro.subject.Subject;

import java.util.Arrays;


public class TestCustomerMd5RealmAuthenicator {
    public static void main(String[] args) {
        DefaultSecurityManager securityManager = new DefaultSecurityManager();
        CustomerMd5Realm customerMd5Realm = new CustomerMd5Realm();
        HashedCredentialsMatcher matcher = new HashedCredentialsMatcher();

        //设置算法
        matcher.setHashAlgorithmName("md5");
        //设置散列次数
        matcher.setHashIterations(1024);
        //设置hash凭证匹配器
        customerMd5Realm.setCredentialsMatcher(matcher);
        securityManager.setRealm(customerMd5Realm);

        SecurityUtils.setSecurityManager(securityManager);


        Subject subject = SecurityUtils.getSubject();

        //认证
        UsernamePasswordToken token = new UsernamePasswordToken("haha","123456");
        try {
            subject.login(token);
        } catch (UnknownAccountException e) {
            e.printStackTrace();
        } catch (IncorrectCredentialsException e) {
            e.printStackTrace();
        }

        //授权
        if (subject.isAuthenticated()) {
            //基于角色权限控制
            System.out.println("super: " + subject.hasRole("super"));
            System.out.println("admin: " + subject.hasRole("admin"));

            //基于多角色权限控制
            System.out.println(subject.hasAllRoles(Arrays.asList("admin","super")));

            //是否具有其中的一个角色
            boolean[] booleans = subject.hasRoles(Arrays.asList("admin","super","user"));
            for (boolean v : booleans) {
                System.out.println(v);
            }
            //基于权限字符串的访问控制
            System.out.println(subject.isPermitted("user:*:01"));

            boolean[] permitted = subject.isPermitted("user:*:01","order:*:10");
            for (boolean v : permitted) {
                System.out.println(v);
            }

            //同时具有哪些权限
            boolean permittedAll = subject.isPermittedAll("user:*:01","product:*:*");
            System.out.println(permittedAll);
        }
    }
}

```


**CustomerMd5Realm.java**

```
package xyz.wuhen.shiro.demo4;

import org.apache.shiro.authc.AuthenticationException;
import org.apache.shiro.authc.AuthenticationInfo;
import org.apache.shiro.authc.AuthenticationToken;
import org.apache.shiro.authc.SimpleAuthenticationInfo;
import org.apache.shiro.authz.AuthorizationInfo;
import org.apache.shiro.authz.SimpleAuthorizationInfo;
import org.apache.shiro.realm.AuthorizingRealm;
import org.apache.shiro.subject.PrincipalCollection;
import org.apache.shiro.util.ByteSource;

public class CustomerMd5Realm extends AuthorizingRealm {

    @Override
    protected AuthorizationInfo doGetAuthorizationInfo(PrincipalCollection principals) {
        System.out.println("==============================");
        String primaryPrincipal = (String) principals.getPrimaryPrincipal();
        System.out.println("身份信息：" + primaryPrincipal);


        SimpleAuthorizationInfo simpleAuthorizationInfo = new SimpleAuthorizationInfo();
        //设置权限
        simpleAuthorizationInfo.addRole("admin");
        simpleAuthorizationInfo.addRole("user");

        //设置基于字符的权限
        simpleAuthorizationInfo.addStringPermission("user:*:01");
        simpleAuthorizationInfo.addStringPermission("product:create:02");
        return simpleAuthorizationInfo;
    }

    @Override
    protected AuthenticationInfo doGetAuthenticationInfo(AuthenticationToken token) throws AuthenticationException {
        String principal = (String) token.getPrincipal();
        if ("haha".equals(principal)) {
            //md5
//            SimpleAuthenticationInfo simpleAuthenticationInfo =
//                    new SimpleAuthenticationInfo(principal,"e10adc3949ba59abbe56e057f20f883e",this.getName());
            // md5 + salt
            SimpleAuthenticationInfo simpleAuthenticationInfo =
                    new SimpleAuthenticationInfo(principal,"4fdf0ba83c7a7e128f35a1f4b78b35ba", ByteSource.Util.bytes("sjshhsx"),this.getName());
            return simpleAuthenticationInfo;
        }
        return null;
    }
}

```


## demo7-->springboot 整合shiro 认证demo


## demo8-->shiro中授权编程实现方式

**编程式**

```
Subject subject = SecurityUtils.getSubject();
if (subject.hasRole("admin")) {
    //无权限
} else {
    //有权限
}
```

**注解式**

```
@RequiresRoles("admin")
public void hello() {
    //有权限
}
```

**标签式**

```
JSP/GSP 标签： 在JSP/GSP 页面通过相应的标签完成

<shiro:hasRole name="admin">
          //有权限
</shiro:hasRole>

注意啊：Thymeleaf 中使用shiro需要额外集成！！
```


## demo9-->shiro启用EhCache缓存

**pom.xml**

```
        <dependency>
            <groupId>org.apache.shiro</groupId>
            <artifactId>shiro-ehcache</artifactId>
            <version>1.8.0</version>
        </dependency>
```

**ShiroConfig.java**

```
@Bean
    public Realm getRealm() {
        CustomerRealm customerRealm = new CustomerRealm();
        HashedCredentialsMatcher hashedCredentialsMatcher = new HashedCredentialsMatcher();
        //算法设置
        hashedCredentialsMatcher.setHashAlgorithmName("MD5");
        //散列次数
        hashedCredentialsMatcher.setHashIterations(1024);
        customerRealm.setCredentialsMatcher(hashedCredentialsMatcher);

        //开启缓存
        customerRealm.setCacheManager(new EhCacheManager());
        //开启全局缓存
        customerRealm.setCachingEnabled(true);
        //开启认证缓存
        customerRealm.setAuthenticationCachingEnabled(true);
        customerRealm.setAuthenticationCacheName("authenticationCache");
        //开启授权缓存
        customerRealm.setAuthorizationCachingEnabled(true);
        customerRealm.setAuthorizationCacheName("authorizationCache");
        return customerRealm;
    }
```


## 过滤器

|配置缩写|对应的过滤器|功能|
|----|----|----|
|anon|	AnonymousFilter|	指定url可以匿名访问（访问时不需要认证授权）|
|authc|	FormAuthenticationFilter|	指定url需要form表单登录，默认会从请求中获取username、password,rememberMe等参数并尝试登录，如果登录不了就会跳转到loginUrl配置的路径。我们也可以用这个过滤器做默认的登录逻辑，但是一般都是我们自己在控制器写登录逻辑的，自己写的话出错返回的信息都可以定制嘛。|
|authcBasic|	BasicHttpAuthenticationFilter|	指定url需要basic登录|
|logout|	LogoutFilter|	登出过滤器，配置指定url就可以实现退出功能，非常方便|
|noSessionCreation|	NoSessionCreationFilter	禁止创建会话|
|perms|	PermissionsAuthorizationFilter	需要指定权限才能访问|
|port|	PortFilter|	需要指定端口才能访问|
|rest|	HttpMethodPermissionFilter|	将http请求方法转化成相应的动词来构造一个权限字符串，这个感觉意义不大，有兴趣自己看源码的注释|
|roles|	RolesAuthorizationFilter|	需要指定角色才能访问|
|ssl|	SslFilter|	需要https请求才能访问|
|user|	UserFilter|	需要已登录或“记住我”的用户才能访问|
