# 果酱V中的自定义链接协议

## 1.协议头

### 无协议头

默认作为 相对地址 与 `baseurl`  拼接，规则详见 [主机名baseurl][]

### maze

打开一篇*.md或 *.jamv.md 后缀的文章。

例：果酱V 教学和推送文章

### menu

打开一个*.json｜ *.no.json 或 *.multi.json 格式的单选、可运行脚本或者多选菜单。

例：果酱V 订阅列表和菜单项

### download

调用果酱V 内部下载器，并命名资源。

#### 1. 拼接格式

```dart
/// 1. 采用baseurl拼接的地址格式
/// 原始地址 download://pic:large@baseurl/qrcode_discuss_hd.jpg
/// 真实下载地址 https://{baseurl}/qrcode_discuss_hd.jpg
/// 下载到目录
/// {configable_download_basedir}/pic/large/qrcode_discuss_hd.jpg
```

#### 2. 完整格式

```dart
/// 2. 采用完整原始 url 的格式
/// download://07imgmini.eastday.com/mobile/20200128/20200128195729_275630d2393efd694875aace7880a711_3.jpeg
/// 下载地址 https://07imgmini.eastday.com/mobile/20200128/20200128195729_275630d2393efd694875aace7880a711_3.jpeg
/// 下载到目录
///{download_basedir}/07imgmini.eastday.com/mobile%20200128/20200128195729_275630d2393efd694875aace7880a711_3.jpeg
```

#### 3.百度网盘转存

```dart
/// 3.百度网盘转存
/// 原始地址 https://pan.baidu.com/s/1RUKlP45483rYMKE4Iqy-eQ 密码:9tk5
/// 协议化地址 download://bdnetdisk:9tk5@pan.baidu.com/s/1RUKlP45483rYMKE4Iqy-eQ
/// [有百度网盘app] 打开百度网盘app转存界面
/// [没有百度网盘app] 打开浏览器下载页 (密码粘贴到剪贴板)
```



用于内容产品的预加载。

⚠️ 可用于百度网盘资源的转存。

## 2.主机名

### baseurl:[ 等待时长(s) ]

可接任何内置协议，用于强制拼接相对地址，baseurl 通常为环境变量，比如在二级菜单中保存一级菜单的完整地址。

后面可接冒号整数 [:30] 表示等待的读秒，一般用于maze。

⚠️ 该处占用了协议的端口号字段，若需要拼接的url 有额外的端口号，请使用完整地址

##### 合法范例

```dart
{baseurl='https://gitee.com/da-jia-vinci-studio/public_store/raw/master/qrcode/404.md'}
```

###### 1.使用 maze 打开[文章] \(https://gitee.com/da-jia-vinci-studio/public_store/raw/master/qrcode/download.md\)，5s 等待。

```dart
maze://baseurl:5/download.md
```

###### 2.使用[下载器][]下载[高清大图]\(https://gitee.com/da-jia-vinci-studio/public_store/raw/master/qrcode/qrcode_discuss_hd.jpg\)到[本地目录]\({configable_base_dir}/pic/default/qrcode_discuss_hd.jpg\)

```dart
download://pic@baseurl/qrcode_discuss_hd.jpg
```

