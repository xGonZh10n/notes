# Ubuntu 18.04安装fcitx输入法

## 安装fcitx

```ruby
$ sudo apt install fcitx fcitx-sunpinyin
```

## 配置fcitx

- 打开系统Settings，Region & Language，Manage Installed Languages，安装中文语言包，然后选择Keyboard input method system为fcitx；
- 重启系统；
- 在Region & Language，input Sources中添加Chinese(Intelligent Pinyin)；
- 打开fcitx configure，添加输入法Sunpinyin，将输入法切换按键修改为自己常用的按键。