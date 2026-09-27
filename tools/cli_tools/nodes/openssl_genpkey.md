# genpkey

- 生成 RSA 私钥（推荐 >= 2048 位）：
  `openssl genpkey -algorithm RSA -pkeyopt rsa_keygen_bits:{{2048}} -out {{private_key.pem}}`

- 生成 EC 私钥（prime256v1，适用于现代 TLS）：
  `openssl genpkey -algorithm EC -pkeyopt ec_paramgen_curve:prime256v1 -out {{ec_private_key.pem}}`
