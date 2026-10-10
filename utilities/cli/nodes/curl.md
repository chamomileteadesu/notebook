# curl

> 传输数据的命令行工具。  
> 更多信息：<https://manned.org/curl>

- 发送 GET 请求并输出到文件：

  `curl [-o|--output] 文件名 URL`

- 发送 GET 请求并使用远程文件名保存：

  `curl [-O|--remote-name] URL`

- 查看响应头和响应体：

  `curl [-i|--show-headers] URL`

- 查看详细的通信过程：

  `curl [-v|--verbose] URL`

- 跟随 HTTP 重定向：

  `curl [-L|--location] URL`

- 使用 POST 发送 urlencoded 数据：

  `curl [-X|--request] POST [-d|data] "k1=v1&k2=v2" URL`

- 使用 POST 发送 JSON 数据：

  `curl [-X|--request] POST [-H|--header] "Content-Type: application/json" [-d|data] '{"key": "value"}' URL`

- 发送单表文件

  `curl [-F|--form] "file=@文件路径" URL`

- 发送表单：

  `curl [-F|--form] "k1=v1" -F "k2=v2" URL`

- 使用表单发送文件，从 stdin 读取

  `curl [-F|--form] "file=@-" URL`

- 使用表单发送多个文件

  `curl [-F|--form] "files[]=@file1" -F files[]=@file2 URL`

- 使用 PUT 请求发送文件，直接把将内容放进 body
  
  `curl [-T|--upload-file] @path_to_file URL`

- 静默模式（不显示进度）：

  `curl [-s|--silent] URL`

- 若發生錯誤，請顯示錯誤訊息（不要連錯誤都被 -s 藏起來）

  `curl [-sS|--silent --show-error]  URL`

- 若 HTTP 狀態碼是錯誤（4xx、5xx），不要輸出 HTML 錯誤頁面，並讓指令回傳失敗

  `curl [-f|--fail] URL`

- 跳过 SSL 证书验证：

  `curl [-k|--insecure] URL`
