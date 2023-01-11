![forks: 0](https://badgen.net/github/forks/Scipline/apk_analyse?labelColor=black&color=orange)	![](https://badgen.net/github/stars/Scipline/apk_analyse?labelColor=black&color=pink)	![commits: 2](https://badgen.net/github/commits/Scipline/apk_analyse)	![](https://badgen.net/github/release/Scipline/apk_analyse)	![GitHub language count](https://img.shields.io/github/languages/count/Scipline/apk_analyse?labelColor=abcdef&style=flat&color=brightgreen)	![GitHub top language](https://img.shields.io/github/languages/top/Scipline/apk_analyse?style=flat&labelColor=4a2206&color=ab2415)

### 一. 前言

有很多诸如`apk_release.apk`，`base.apk`等在PC上无法直接知悉其信息的APK文件，除非必要安装到手机。为了有效管理APK文件，知悉APK详情，对比版本更新，急于在PC上找一个工具可以获取APK简略信息及其图标icon信息，用于管理APK文件。但无奈在找不到一个可行PC的工具。有如[apk-info](https://github.com/Enyby/APK-Info)（加载信息过多，缓慢，无法导出信息，图标，不支持批量），[APK Messenger v4.3](https://www.ghxi.com/apkinfo.html)(果核网站开发，年久失修，新API的apk功能失效)，[APK Messenger复刻版](https://github.com/ghboke/APKMessenger)(同上)。可能还有很多优秀的工具未经发现，但目前实在找不到，于是自己结合网上前辈经验开发一个。 

### 二. 功能点
- 批量解析ICON
- 批量获取APK信息
- 批量格式化重命名APK

### 三. 实现思路
- **Common**类处理输入指令，通用处理方法

- **WriteData**类写入数据到Excel文件

- **AndroGuard**和**Aapt**类分别两个解析方式

### 四. 使用说明
配置好python3，通过命令`pip install -r requirements.txt`安装所需的库。

4.1 查看help
`python apk_analyse.py -h`

```bash
		    ——————————— 使用说明 ————————————————
            xxx.apk             获取apk信息
            -t, --type:         处理引擎A or B(默认A)
            -d, --dirs:         获取目录下所有apk信息
            -r, --rename:       批量格式化重命名apk
            -v, --version:      版本号
            -h, --help:         帮助信息
            —————————————————————————————————————
```

4.2 获取单个apk信息

```bash
默认A引擎：
python apk_analyse.py xxx.apk
指定引擎：
python apk_analyse.py -t B xxx.apk
```

4.3 批量获取apk信息

```bash
默认A引擎：
python apk_analyse.py -d App
指定引擎：
python apk_analyse.py -t A -d App
python apk_analyse.py -t B -d App
```

4.4 批量格式化重命名apk

```bash
python apk_analyse.py -r App
```

### 五. 注意

- A引擎为androguard_v3.3.5-2019年2月18日，理论最高支持API28，Android9.0 【[https://pypi.org/project/androguard](https://pypi.org/project/androguard)】
- B引擎为aapt_v0.2-4913185-2018年8月10日，理论最高支持API24，Android7.0。可解析A引擎获取不到图标，需要额外调用，导致apk名称不能有空格。【[https://androidaapt.com](https://androidaapt.com)】
- 目前所用的androguard版本从Github上获取，2022年11月20日，理论最高支持API29，Android10.0【[https://github.com/androguard/androguard](https://github.com/androguard/androguard)】。去除了未发行版本带有的所有debug信息，新版使用方法`from androguard.core.apk import APK`。原3.3.5版为`from androguard.core.bytecodes.apk import APK`

### 六. 参考文献

> androguard开源库：[https://github.com/androguard/androguard](https://github.com/androguard/androguard)
>
> aapt工具使用介绍：[https://juejin.cn/post/7075594597505695758](https://juejin.cn/post/7075594597505695758)
>
> aapt2工具文档：[https://developer.android.google.cn/studio/command-line/aapt2?hl=zh-cn#dump_commands](https://developer.android.google.cn/studio/command-line/aapt2?hl=zh-cn#dump_commands)
>
> 代码参考：
>
> [https://blog.csdn.net/h1986y/article/details/123737172](https://blog.csdn.net/h1986y/article/details/123737172) 
>
> [https://github.com/omieo2/apk_toolbox](https://github.com/omieo2/apk_toolbox)
>
> 遇到编码问题，改用subprocess，参考：[https://blog.csdn.net/u012871930/article/details/128022910](https://blog.csdn.net/u012871930/article/details/128022910)
