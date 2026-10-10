# localectl

> 查询和更改系统区域和语言设置。
> 更多信息：<https://manned.org/localectl>

- 显示当前区域设置：
  `localectl`

- 列出所有可用的区域设置：
  `localectl list-locales`

- 设置系统区域：
  `localectl set-locale {{LANG=zh_CN.UTF-8}}`

- 设置系统区域（完整格式）：
  `localectl set-locale LANG={{zh_CN.UTF-8}} LC_TIME={{en_US.UTF-8}}`

- 列出可用的键盘布局：
  `localectl list-keymaps`

- 设置控制台键盘布局：
  `localectl set-keymap {{布局名}}`

- 设置 X11 键盘布局：
  `localectl set-x11-keymap {{布局名}}`

- 设置 X11 键盘布局（带变体和选项）：
  `localectl set-x11-keymap {{us}} {{pc105}} {{dvorak}}`

- 查看当前键盘布局状态：
  `localectl status`