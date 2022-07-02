# <img src="./image/logo.png" alt="JWT icon" width="160" height="80">

## JWT-Tutorial
### JSON Web Token

+ fast
+ Stateless
+ Used across many services

+ Compromised Secret Key
+ No visibility to logged in users
+ Token can be stolen

### What is the JSON Web Token structure

In its compact from, JSON Web Tokens consists of three parts separated by dots ( . ) which are:

* Header
* Payload 
* Signature

Therefore, a JWT typically looks like the following.

                   xxxxx.yyyyy.zzzzz


### Header
The header typically consists of two parts: the type od the token, which is JWT and the signing algorithm being used, such as HMAC SHA256 or RSA

Example header encoder

```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```

### Payload 
The second part of the token is the payload, which contains the claims. Claims are statements about an entity (typically, the user) and additional data. There are three types of claims: registered, public, and private claims.

#### Registered claims: 

These are a set of predefined claims which are not mandatory but recommended, to provide a set of useful, interoperable claims. Some of them are: iss (issuer), exp (expiration time), sub (subject), aud (audience), and others.

```cmd
1  "iss" (Issuer) Claim

   The "iss" (issuer) claim identifies the principal that issued the
   JWT.  The processing of this claim is generally application specific.
   The "iss" value is a case-sensitive string containing a StringOrURI
   value.  Use of this claim is OPTIONAL.
 
2  "sub" (Subject) Claim

   The "sub" (subject) claim identifies the principal that is the
   subject of the JWT.  The claims in a JWT are normally statements
   about the subject.  The subject value MUST either be scoped to be
   locally unique in the context of the issuer or be globally unique.
   The processing of this claim is generally application specific.  The
   "sub" value is a case-sensitive string containing a StringOrURI
   value.  Use of this claim is OPTIONAL.
   
3  "aud" (Audience) Claim

   The "aud" (audience) claim identifies the recipients that the JWT is
   intended for.  Each principal intended to process the JWT MUST
   identify itself with a value in the audience claim.  If the principal
   processing the claim does not identify itself with a value in the
   "aud" claim when this claim is present, then the JWT MUST be
   rejected.  In the general case, the "aud" value is an array of case-
   sensitive strings, each containing a StringOrURI value.  In the
   special case when the JWT has one audience, the "aud" value MAY be a
   single case-sensitive string containing a StringOrURI value.  The
   interpretation of audience values is generally application specific.
   Use of this claim is OPTIONAL.
  
4  "exp" (Expiration Time) Claim

   The "exp" (expiration time) claim identifies the expiration time on
   or after which the JWT MUST NOT be accepted for processing.  The
   processing of the "exp" claim requires that the current date/time
   MUST be before the expiration date/time listed in the "exp" claim.
   Implementers MAY provide for some small leeway, usually no more than
   a few minutes, to account for clock skew.  Its value MUST be a number
   containing a NumericDate value.  Use of this claim is OPTIONAL.
   
5  "nbf" (Not Before) Claim

   The "nbf" (not before) claim identifies the time before which the JWT
   MUST NOT be accepted for processing.  The processing of the "nbf"
   claim requires that the current date/time MUST be after or equal to
   the not-before date/time listed in the "nbf" claim.  Implementers MAY
   provide for some small leeway, usually no more than a few minutes, to
   account for clock skew.  Its value MUST be a number containing a
   NumericDate value.  Use of this claim is OPTIONAL.
   
6  "iat" (Issued At) Claim

   The "iat" (issued at) claim identifies the time at which the JWT was
   issued.  This claim can be used to determine the age of the JWT.  Its
   value MUST be a number containing a NumericDate value.  Use of this
   claim is OPTIONAL.
   
7  "jti" (JWT ID) Claim

   The "jti" (JWT ID) claim provides a unique identifier for the JWT.
   The identifier value MUST be assigned in a manner that ensures that
   there is a negligible probability that the same value will be
   accidentally assigned to a different data object; if the application
   uses multiple issuers, collisions MUST be prevented among values
   produced by different issuers as well.  The "jti" claim can be used
   to prevent the JWT from being replayed.  The "jti" value is a case-
   sensitive string.  Use of this claim is OPTIONAL.
   
```
#### Public claims: 

These can be defined at will by those using JWTs. But to avoid collisions they should be defined in the [IANA JSON Web Token Registry](https://www.iana.org/assignments/jwt/jwt.xhtml) or be defined as a URI that contains a collision resistant namespace.

#### Private claims: 

These are the custom claims created to share information between parties that agree on using them and are neither registered or public claims.

Example payload encodeed:

```json
{
  "sub": "1234567890",
  "name": "John Doe",
  "admin": true
}
```


