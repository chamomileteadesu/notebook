# openssl

> 多用途加密与 TLS/证书工具。
> 更多信息：<https://manned.org/openssl>

- 查看证书详细信息（包括 SAN、有效期等）：
  `openssl x509 -in {{certificate.pem}} -text -noout`

- 查看 CSR 内容并校验签名：
  `openssl req -in {{domain.csr}} -text -noout -verify`

- 校验证书是否由指定 CA 签发（检查链路）：
  `openssl verify -CAfile {{ca_bundle.pem}} {{certificate.pem}}`

- 主动连到远程主机查看 TLS 握手与证书（调试 HTTPS/TLS）：
  `openssl s_client -connect {{host}}:{{443}} -servername {{host}}`

- 在 PEM 与 DER 证书格式之间转换：
  `openssl x509 -in {{certificate.pem}} -outform der -out {{certificate.der}}`

- 将 PEM 证书与私钥打包为 PKCS#12（常用于导入浏览器/系统证书库）：
  `openssl pkcs12 -export -inkey {{private_key.pem}} -in {{certificate.pem}} -certfile {{ca_bundle.pem}} -out {{bundle.p12}}`

- 从 PKCS#12 文件中提取私钥与证书（转回 PEM）：
  `openssl pkcs12 -in {{bundle.p12}} -nodes -out {{bundle.pem}}`

- 使用口令重新加密已有私钥文件：
  `openssl pkey -in {{private_key.pem}} -aes-256-cbc -out {{encrypted_key.pem}}`

- 从证书中提取公钥（供其他工具使用或对比）：
  `openssl x509 -in {{certificate.pem}} -noout -pubkey > {{public_key.pem}}`

## 常用的子命令

- [[openssl_req|openssl req]]
- [[openssl_rand|openssl rand]]
- [[openssl_genpkey|openssl genpkey]]
- [[openssl_x509|openssl x509]]
- [[openssl_s_client|openssl s_client]]
- [[openssl_dgst|openssl dgst]]
- [[openssl_enc|openssl enc]]
- [[openssl_pkcs12|openssl pkcs12]]
- [[openssl_verify|openssl verify]]
