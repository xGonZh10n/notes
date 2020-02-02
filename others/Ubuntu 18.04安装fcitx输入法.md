# Ubuntu 18.04安装fcitx输入法

## 安装

```ruby
$ sudo apt install fcitx fcitx-ui-qimpanel fcitx-sunpinyin
```

## 配置

- 打开系统Settings，Region & Language，Manage Installed Languages，安装中文语言包，然后选择Keyboard input method system为fcitx；

- 重启系统；

- 在Region & Language，input Sources中添加Chinese(Intelligent Pinyin)；

- 打开fcitx configure，添加输入法Sunpinyin；

- 如果需要，可将输入法切换按键修改为自己常用的按键；

- 如果需要，可通过以下命令删除多余的输入法图标：

  ```ruby
  $ sudo apt remove fcitx-ui-classic
  ```