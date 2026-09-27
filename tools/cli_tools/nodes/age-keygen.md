# age-keygen

> 生成 age 加密工具的密钥对。  
> See also: [[age]].  
> 更多信息：<https://age-encryption.org>

- 生成新的密钥对（私钥输出到文件，公钥显示在终端）：

  `age-keygen -o 密钥文件.txt`

- 生成密钥对并指定输出文件：

  `age-keygen -o 密钥文件.txt 2> 公钥输出.txt`

- 显示私钥文件对应的公钥：

  `age-keygen -y 密钥文件.txt`

- 从 stdin 读取并转换 SSH 私钥为 age 共钥：

  `ssh-keygen -f ssh私钥 -e | age-keygen -y > age公钥.txt`
