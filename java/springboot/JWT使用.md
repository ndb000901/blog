# JWT使用

## 环境

```
        <dependency>
            <groupId>com.auth0</groupId>
            <artifactId>java-jwt</artifactId>
            <version>3.18.2</version>
        </dependency>
```



## 使用

```
package xyz.wuhen.springboot.jwt.utils;

import com.auth0.jwt.JWT;
import com.auth0.jwt.JWTCreator;
import com.auth0.jwt.algorithms.Algorithm;
import com.auth0.jwt.interfaces.DecodedJWT;

import java.util.Calendar;
import java.util.Map;

public class JwtUtil {

    private static final String SOLT = "cndsihicds";

    public static String getToken(Map<String,String> map) {
        Calendar instance = Calendar.getInstance();

        //过期时间
        instance.add(Calendar.DATE,7);
        JWTCreator.Builder builder = JWT.create();

        // playload
        map.forEach((k,v)->{
            builder.withClaim(k,v);
        });

        String token = builder.withExpiresAt(instance.getTime())
                .sign(Algorithm.HMAC256(SOLT));
        return token;

    }

    public static DecodedJWT verify(String token) {
        return JWT.require(Algorithm.HMAC256(SOLT)).build().verify(token);
    }



}

```
