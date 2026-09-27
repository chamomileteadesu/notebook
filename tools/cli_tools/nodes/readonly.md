# readonly

> 将 shell 变量或函数标记为只读，防止后续修改。
> 更多信息：<https://manned.org/readonly>

- 将变量标记为只读：
  `readonly {{变量名}}`

- 声明并初始化只读变量：
  `readonly {{变量名}}="{{值}}"`

- 显示所有只读变量：
  `readonly -p`

- 将函数标记为只读：
  `readonly -f {{函数名}}`

- 显示所有只读函数：
  `readonly -f`

- 删除只读属性（需要 unset）：
  `unset {{变量名}}`

- 检查变量是否为只读：
  `readonly -p | grep {{变量名}}`

- 将数组标记为只读：
  `readonly {{数组名}}=({{元素1}} {{元素2}} {{元素3}})`

- 将关联数组标记为只读：
  `readonly -A {{关联数组名}}=([{{键}}]="{{值}}")`

- 在函数中声明只读变量：
  `function {{函数名}} { readonly {{局部变量}}="{{值}}"; }`

- 使用 declare 声明只读变量：
  `declare -r {{变量名}}="{{值}}"`

- 声明只读整数变量：
  `declare -ir {{变量名}}={{数值}}`

- 声明只读字符串变量：
  `declare -r {{变量名}}="{{字符串}}"`

- 设置只读环境变量：
  `export {{变量名}}="{{值}}"; readonly {{变量名}}`

- 从文件中读取并设置只读变量：
  `source {{配置文件}}; readonly {{变量名}}`

- 条件性设置只读变量：
  `[ -z "${{变量名}}" ] && readonly {{变量名}}="{{默认值}}"`

- 使用命令替换设置只读变量：
  `readonly {{变量名}}="$(command {{参数}})"

- 使用算术运算设置只读变量：
  `readonly {{变量名}}=$((${{表达式}}))

- 设置只读的路径变量：
  `readonly PATH="${{PATH}}:{{新路径}}"

- 设置只读的配置常量：
  `readonly CONFIG_VERSION="{{版本号}}"

- 设置只读的系统路径：
  `readonly SYSTEM_ROOT="{{根路径}}"

- 设置只读的数据库连接参数：
  `readonly DB_HOST="{{主机名}}"; readonly DB_PORT="{{端口号}}"

- 设置只读的 API 端点：
  `readonly API_URL="{{网址}}"; readonly API_KEY="{{密钥}}"

- 在脚本开头设置全局常量：
  `readonly SCRIPT_NAME="$(basename "$0")"; readonly SCRIPT_DIR="$(dirname "$0")"`

- 设置只读的调试标志：
  `readonly DEBUG="${{DEBUG:-false}}"

- 设置只读的日志级别：
  `readonly LOG_LEVEL="${{LOG_LEVEL:-INFO}}"

- 设置只读的时间戳：
  `readonly TIMESTAMP="$(date +%Y%m%d_%H%M%S)"

- 设置只读的用户信息：
  `readonly CURRENT_USER="$(whoami)"; readonly CURRENT_HOME="$HOME"

- 设置只读的系统信息：
  `readonly HOSTNAME="$(hostname)"; readonly OS_TYPE="$(uname)"

- 在循环中设置只读变量（会失败）：
  `for i in {1..5}; do readonly COUNT=$i; done # 会导致错误`

- 使用只读变量作为配置参数：
  `readonly MAX_RETRIES=3; readonly TIMEOUT=30

- 声明只读的枚举值：
  `readonly STATUS_OK=0; readonly STATUS_ERROR=1; readonly STATUS_TIMEOUT=2

- 设置只读的颜色代码：
  `readonly RED='\033[0;31m'; readonly GREEN='\033[0;32m'; readonly YELLOW='\033[1;33m'

- 声明只读的文件扩展名：
  `readonly LOG_EXT=".log"; readonly BAK_EXT=".bak"; readonly TMP_EXT=".tmp"

- 设置只读的数字常量：
  `readonly PI=3.14159265359; readonly E=2.71828182846

- 声明只读的正则表达式：
  `readonly EMAIL_REGEX='^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'

- 设置只读的默认值：
  `readonly DEFAULT_PORT=8080; readonly DEFAULT_HOST="localhost"

- 在条件语句中使用只读变量：
  `if [ "${{DEBUG}}" = "true" ]; then echo "Debug mode enabled"; fi

- 在函数中验证只读变量：
  `validate_config() { if [ -z "${{CONFIG_FILE}}" ]; then echo "CONFIG_FILE not set"; exit 1; fi; }

- 使用只读变量作为数组索引：
  `readonly INDEXES=(0 1 2 3 4); echo "${{INDEXES[2]}}"

- 声明只读的关联数组：
  `readonly -A CONFIG_MAP=([host]="localhost" [port]="8080" [debug]="true")

- 在错误处理中使用只读变量：
  `readonly ERROR_LOG="/var/log/app_error.log"; echo "Error logged to $ERROR_LOG"

- 设置只读的临时目录：
  `readonly TEMP_DIR="${{TEMP_DIR:-/tmp}}"; readonly TEMP_FILE="${TEMP_DIR}/app_${TIMESTAMP}"

- 在配置文件中使用只读变量：
  `readonly APP_NAME="MyApp"; readonly APP_VERSION="1.0.0"

- 声明只读的数学常量：
  `readonly GOLDEN_RATIO=1.61803398875; readonly SQRT_2=1.41421356237

- 设置只读的网络超时：
  `readonly CONNECT_TIMEOUT=10; readonly READ_TIMEOUT=30

- 在脚本中使用只读变量作为保护：
  `readonly SCRIPT_LOCK="/var/run/${SCRIPT_NAME}.lock"

- 声明只读的文件权限：
  `readonly FILE_PERMISSIONS=644; readonly DIR_PERMISSIONS=755

- 设置只读的进程限制：
  `readonly MAX_PROCESSES=100; readonly MAX_MEMORY=1024

- 在日志记录中使用只读变量：
  `readonly LOG_FORMAT="[%Y-%m-%d %H:%M:%S] [%LEVEL%] %MESSAGE%"

- 声明只读的错误代码：
  `readonly EXIT_SUCCESS=0; readonly EXIT_FAILURE=1; readonly EXIT_INVALID_ARGS=2

- 设置只读的缓冲区大小：
  `readonly BUFFER_SIZE=4096; readonly MAX_BUFFER_SIZE=8192

- 在数据库操作中使用只读变量：
  `readonly QUERY_TIMEOUT=60; readonly CONNECTION_POOL_SIZE=10

- 声明只读的编码格式：
  `readonly UTF8_ENCODING="UTF-8"; readonly DEFAULT_ENCODING="ASCII"

- 设置只读的日期格式：
  `readonly DATE_FORMAT="%Y-%m-%d"; readonly TIME_FORMAT="%H:%M:%S"

- 在安全性检查中使用只读变量：
  `readonly MIN_PASSWORD_LENGTH=8; readonly MAX_LOGIN_ATTEMPTS=3

- 声明只读的网络端口范围：
  `readonly PORT_MIN=1024; readonly PORT_MAX=65535

- 在性能监控中使用只读变量：
  `readonly SAMPLE_INTERVAL=5; readonly MAX_SAMPLES=1000

- 设置只读的缓存配置：
  `readonly CACHE_SIZE=100; readonly CACHE_TTL=3600

- 声明只读的 API 版本：
  `readonly API_VERSION="v1"; readonly API_BASE_URL="https://api.example.com"

- 在批处理中使用只读变量：
  `readonly BATCH_SIZE=50; readonly MAX_BATCH_SIZE=100

- 设置只读的重试配置：
  `readonly RETRY_DELAY=1; readonly MAX_RETRY_DELAY=10

- 声明只读的文件大小限制：
  `readonly MAX_FILE_SIZE=10485760; readonly MAX_UPLOAD_SIZE=52428800

- 在数据处理中使用只读变量：
  `readonly CHUNK_SIZE=1024; readonly MAX_CHUNKS=100

- 设置只读的会话配置：
  `readonly SESSION_TIMEOUT=1800; readonly MAX_SESSIONS=1000

- 声明只读的区域设置：
  `readonly LOCALE="en_US.UTF-8"; readonly TIMEZONE="UTC"

- 在测试中使用只读变量：
  `readonly TEST_TIMEOUT=30; readonly TEST_RETRIES=3