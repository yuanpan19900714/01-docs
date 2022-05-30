## OpenSSL签名与认证
- 生成OpenSSL私钥
  ```
  openssl genrsa -out priv.pem 2048
  ```
- 根据秘钥生成公钥
  ```
  openssl rsa -in priv.pem -pubout -out pub.pem
  ```
- 签名
  ```
  openssl dgst -sha1 -sign priv.pem -out signature.txt test.txt
  ```
- 认证
  ```
  openssl dgst -sha1 -keyform PEM -verify pub.pem -signature signature.txt test.txt
  ```