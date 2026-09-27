# dig

> DNS 查询工具，用于查找域名信息。
> 更多信息：<https://manned.org/dig>

- 查询域名的 A 记录：
  `dig {{域名}}`

- 查询域名的任何记录：
  `dig {{域名}} ANY`

- 查询域名的 MX 记录：
  `dig {{域名}} MX`

- 查询域名的 NS 记录：
  `dig {{域名}} NS`

- 查询域名的 TXT 记录：
  `dig {{域名}} TXT`

- 查询域名的 SOA 记录：
  `dig {{域名}} SOA`

- 查询域名的 CNAME 记录：
  `dig {{域名}} CNAME`

- 查询域名的 AAAA 记录（IPv6）：
  `dig {{域名}} AAAA`

- 反向 DNS 查询：
  `dig -x {{IP地址}}`

- 指定 DNS 服务器查询：
  `dig @{{DNS服务器}} {{域名}}`

- 显示简短输出：
  `dig {{域名}} +short`

- 显示详细输出：
  `dig {{域名}} +noall +answer`

- 查询特定端口：
  `dig {{域名}} +short -p {{端口号}}`

- 查询域名的 PTR 记录：
  `dig {{域名}} PTR`

- 查询域名的 SRV 记录：
  `dig {{域名}} SRV`

- 查询域名的 DNSKEY 记录：
  `dig {{域名}} DNSKEY`

- 查询域名的 RRSIG 记录：
  `dig {{域名}} RRSIG`

- 查询域名的 NSEC 记录：
  `dig {{域名}} NSEC`

- 查询域名的 CAA 记录：
  `dig {{域名}} CAA`

- 查询域名的 TLSA 记录：
  `dig {{域名}} TLSA`

- 查询域名的 SSHFP 记录：
  `dig {{域名}} SSHFP`

- 查询域名的 LOC 记录：
  `dig {{域名}} LOC`

- 查询域名的 RP 记录：
  `dig {{域名}} RP`

- 查询域名的 AFSDB 记录：
  `dig {{域名}} AFSDB`

- 查询域名的 HINFO 记录：
  `dig {{域名}} HINFO`

- 查询域名的 ISDN 记录：
  `dig {{域名}} ISDN`

- 查询域名的 RT 记录：
  `dig {{域名}} RT`

- 查询域名的 X25 记录：
  `dig {{域名}} X25`

- 查询域名的 PX 记录：
  `dig {{域名}} PX`

- 查询域名的 GPOS 记录：
  `dig {{域名}} GPOS`

- 查询域名的 APL 记录：
  `dig {{域名}} APL`

- 查询域名的 CERT 记录：
  `dig {{域名}} CERT`

- 查询域名的 DNAME 记录：
  `dig {{域名}} DNAME`

- 查询域名的 OPT 记录：
  `dig {{域名}} OPT`

- 查询域名的 DS 记录：
  `dig {{域名}} DS`

- 查询域名的 NSEC3 记录：
  `dig {{域名}} NSEC3`

- 查询域名的 NSEC3PARAM 记录：
  `dig {{域名}} NSEC3PARAM`

- 查询域名的 DLV 记录：
  `dig {{域名}} DLV`

- 使用 TCP 协议查询：
  `dig {{域名}} +tcp`

- 使用 IPv4 查询：
  `dig {{域名}} +4`

- 使用 IPv6 查询：
  `dig {{域名}} +6`

- 显示查询统计信息：
  `dig {{域名}} +stats`

- 显示查询时间：
  `dig {{域名}} +stats | grep "Query time"`

- 跟踪 DNS 查询路径：
  `dig {{域名}} +trace`

- 查询域名的授权服务器：
  `dig {{域名}} +nssearch`

- 查询域名的 SOA 记录并显示详细信息：
  `dig {{域名}} SOA +multiline`

- 查询域名的 DNSSEC 信息：
  `dig {{域名}} +dnssec`

- 验证 DNSSEC 签名：
  `dig {{域名}} +dnssec +multiline`

- 查询域名的缓存信息：
  `dig {{域名}} +nsid

- 查询域名的 EDNS 信息：
  `dig {{域名}} +edns=0`

- 查询域名的 TLD 信息：
  `dig {{域名}} +tld`

- 查询域名的根服务器信息：
  `dig {{域名}} +root

- 查询域名的递归查询：
  `dig {{域名}} +recursive`

- 查询域名的非递归查询：
  `dig {{域名}} +norecursive`

- 查询域名的 AD 标志：
  `dig {{域名}} +adflag`

- 查询域名的 CD 标志：
  `dig {{域名}} +cdflag`

- 查询域名的 RD 标志：
  `dig {{域名}} +rdflag`

- 查询域名的 RA 标志：
  `dig {{域名}} +raflag`

- 查询域名的 TC 标志：
  `dig {{域名}} +tcflag`

- 查询域名的 AA 标志：
  `dig {{域名}} +aaflag`

- 查询域名的 DO 标志：
  `dig {{域名}} +do`

- 查询域名的 DNSSEC OK 标志：
  `dig {{域名}} +dnssecok`

- 查询域名的 Z 标志：
  `dig {{域名}} +zflag`

- 查询域名的 TTL 信息：
  `dig {{域名}} +ttl`

- 查询域名的权威回答：
  `dig {{域名}} +authoritative`

- 查询域名的附加信息：
  `dig {{域名}} +additional`

- 查询域名的查询 ID：
  `dig {{域名}} +question`

- 查询域名的回答：
  `dig {{域名}} +answer`

- 查询域名的权威部分：
  `dig {{域名}} +authority`

- 查询域名的附加部分：
  `dig {{域名}} +additional`

- 查询域名的命令选项：
  `dig {{域名}} +cmd

- 查询域名的注释：
  `dig {{域名}} +comments`

- 查询域名的默认设置：
  `dig {{域名}} +default`

- 查询域名的定义：
  `dig {{域名}} +defname`

- 查询域名的搜索域：
  `dig {{域名}} +search`

- 查询域名的绑定检查：
  `dig {{域名}} +bind`

- 查询域名的多行输出：
  `dig {{域名}} +multiline`

- 查询域名的短格式：
  `dig {{域名}} +short`

- 查询域名的详细格式：
  `dig {{域名}} +detail`

- 查询域名的 IDN 支持：
  `dig {{域名}} +idnin`

- 查询域名的 IDN 输出：
  `dig {{域名}} +idnout`

- 查询域名的 Unicode 支持：
  `dig {{域名}} +unicode`

- 查询域名的强制 TCP：
  `dig {{域名}} +vc`

- 查询域名的忽略 TC：
  `dig {{域名}} +ignore`

- 查询域名的保持开放：
  `dig {{域名}} +keepopen`

- 查询域名的发送缓冲区：
  `dig {{域名}} +bufsize={{大小}}`

- 查询域名的重试次数：
  `dig {{域名}} +retry={{次数}}`

- 查询域名的超时时间：
  `dig {{域名}} +time={{秒数}}`

- 查询域名的尝试次数：
  `dig {{域名}} +tries={{次数}}`

- 查询域名的端口：
  `dig {{域名}} +port={{端口号}}`

- 查询域名的源地址：
  `dig {{域名}} +source={{IP地址}}`

- 查询域名的源端口：
  `dig {{域名}} +sourceport={{端口号}}`

- 查询域名的本地地址：
  `dig {{域名}} +local={{IP地址}}`

- 查询域名的本地端口：
  `dig {{域名}} +localport={{端口号}}`

- 查询域名的设备：
  `dig {{域名}} +device={{设备名}}`

- 查询域名的 DSCP：
  `dig {{域名}} +dscp={{值}}`

- 查询域名的 EDNS 版本：
  `dig {{域名}} +edns={{版本}}`

- 查询域名的 EDNS 选项：
  `dig {{域名}} +edns={{选项}}`

- 查询域名的 EDNS 标志：
  `dig {{域名}} +ednsflags={{标志}}`

- 查询域名的 EDNS UDP 大小：
  `dig {{域名}} +ednsopt={{选项}}:{{数据}}`

- 查询域名的 EDNS NSID：
  `dig {{域名}} +nsid`

- 查询域名的 EDNS COOKIE：
  `dig {{域名}} +cookie={{cookie}}`

- 查询域名的 EDNS EXP选项：
  `dig {{域名}} +exp={{选项}}`

- 查询域名的 EDNS EDE：
  `dig {{域名}} +ede`

- 查询域名的 EDNS 子网：
  `dig {{域名}} +subnet={{子网}}`

- 查询域名的 EDNS 客户端子网：
  `dig {{域名}} +client-subnet={{子网}}`

- 查询域名的 EDNS 管道：
  `dig {{域名}} +pipe`

- 查询域名的 EDNS 保持：
  `dig {{域名}} +keepalive`

- 查询域名的 EDNS HTTP：
  `dig {{域名}} +http`

- 查询域名的 EDNS HTTPS：
  `dig {{域名}} +https`

- 查询域名的 EDNS TLS：
  `dig {{域名}} +tls`

- 查询域名的 EDNS QUIC：
  `dig {{域名}} +quic`

- 查询域名的 EDNS DNS-over-HTTPS：
  `dig {{域名}} +doh`

- 查询域名的 EDNS DNS-over-TLS：
  `dig {{域名}} +dot`

- 查询域名的 EDNS DNS-over-QUIC：
  `dig {{域名}} +doq`

- 查询域名的 EDNS 混合：
  `dig {{域名}} +mixed`
