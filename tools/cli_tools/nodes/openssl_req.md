# req

- 使用已有私钥生成 CSR（证书签名请求）：
  `openssl req -new -key {{private_key.pem}} -out {{domain.csr}}`

- 一步生成新 RSA 私钥和 CSR：
  `openssl req -newkey rsa:{{2048}} -nodes -keyout {{domain.key}} -out {{domain.csr}}`

- 为本地开发生成自签名证书（例如本地 HTTPS）：
  `openssl req -x509 -newkey rsa:{{2048}} -days {{365}} -nodes -keyout {{localhost.key}} -out {{localhost.crt}} -subj "/CN={{localhost}}"`
