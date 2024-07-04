# JWT

## JJWT

```
// https://mvnrepository.com/artifact/io.jsonwebtoken/jjwt
implementation 'io.jsonwebtoken:jjwt:0.12.5'
```

### 토큰 생성

{% code overflow="wrap" %}
```java
// @deprecated
String jwt = Jwts.builder()
                    .setHeader(headers)
                    .setClaims(payloads)
                    .signWith(SignatureAlgorithm.HS256,key.getBytes())
                    .compact();

String jwt = Jwts.builder()
                    .Claims("email", payloads)                    
                    .SignWith(key.getBytes(), Jwts.SIG.HS512)
                    .compact();
```
{% endcode %}

### 토큰 파싱/검증

<pre class="language-java" data-overflow="wrap"><code class="lang-java">// @deprecated
Claims claims = Jwts.parser()
<strong>                    .setSignKey("A".getBytes())
</strong><strong>                    .parseClaimsJws(jwtTokenString)
</strong><strong>                    .getBody();
</strong><strong>Date expiration = claims.get("exp", Date.class);
</strong>String data = claims.get("data", String.class);                    
<strong>
</strong><strong>Jws&#x3C;Claims> claimsJws = Jwts.parser()
</strong><strong>                            .verifyWith(secretKey)
</strong><strong>                            .build()
</strong><strong>                            .parseSignedClaim(jwtTokenString)
</strong>claimsJws.getPayload().getIssuedAt();
</code></pre>
