# age

> 一个简单、现代、安全的文件加密工具。  
> See also: [[age-keygen]], [[rage]].  
> 更多信息：<https://age-encryption.org>

- 使用公钥加密文件：

  `age [-r|--recipient] pubkey -o out.age source_file`

- 使用密码加密文件：

  `age [-p|--passphrase] -o out.age source_file`

- 解密文件：

  `age [-d|--decrypt] [-i|--identity] prikey out.age > decrypted_file`

- 使用密码解密文件：

  `age [-d|--decrypt] out.age > decrypted_file`

- 加密到多个接收者：

  `age -r pubkey1 -r pubkey2 -o out.age source_file`
