---
title: "Typora Cracker"
date: 2024-09-30T02:17:37+08:00
---
# Typora激活记录

> 纯属学习记录，不提供任何服务

针对不同版本，大致有四种方法

- 自行修改`License.js`文件的时间戳 （v0.11.18以下）
- 替换`License.js`文件(v1.0.0~v1.0.3)
- 替换软件根目录`Winmm.dll`文件 (?~v1.8.10)
- `node_inject.exe`注入，配合`license-gen.exe`或`keygen.js` (?~v1.9.5)

## 方法一：修改时间戳（适用于未收费时期版本）

思路

[Typora 授权解密与剖析](https://www.52pojie.cn/thread-1553967-1-1.html)



参阅

- [~~Mas0nShi/typoraCracker~~](https://github.com/Mas0nShi/typoraCracker)(已删库)

### 所需环境

- Python3
- Node.js

### 步骤

- 安装对应版本的Typora
- 找到Typora安装目录下的app.asar文件`X:\Program Files\Typora\resources\app.asar`

- Git或下载TyporaCracker
- 进入文件夹根目录

```powershell
cd typoracracker
```

- 安装依赖

```python
pip install -r requirements.txt
```

- 解包Typora的app.asar文件

```python
python typora.py "X:\Program Files\Typora\resources\app.asar" .
```

- 打开解包的`.\dec_app\License.js`文件，将所有时间戳`1637934234708`修改为未来的时间`4033667395000`（时间戳单位是毫秒）

- 打包`app.asar`文件

```python
python typora.py -u ./dec_app/ .
```

- 替换`app.asar`文件
- 在typoracracker文件夹下，打开Terminal生成序列号

```
node ./keygen.js
```

- 随便填入邮箱，再将序列号填入即可

## 方法二：替换`License.js`文件

- 修改时间戳那一步，改为将example下的`License.js`替换进dec_app文件夹下，其余操作与方法一相同，

## 方法三：替换`Winmm.DLL`文件

参阅

[typora-activation](https://github.com/markyin0707/typora-activation)

- 下载`winmm.dll`,将其放入Typora安装根目录下即可

> 此方法Microsoft Defender可能会报毒，自行斟酌

## 方法四：node注入

参阅

[AWDSCAN/Typora](https://github.com/AWDSCAN/Typora)

[NodeInject](https://github.com/DiamondHunters/NodeInject)

[NodeInject_Hook_example](https://github.com/DiamondHunters/NodeInject_Hook_example)

[Rust : 解决 Cargo 下载依赖时卡住的办法 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/74875840)

如需自己编译Nodeject需安装rust与VS

将`Node_ject.exe`放入Typora根目录下并打开，完成后运行`License.exe`将序列号填入激活

## 方法五（适用1.7.6）

- 修改 Typora 安装目录 \ resources\page-dist\static\js\LicenseIndex.xxxxxxxxx.xxxxxxx.chunk.js，激活主程序

查找：`e.hasActivated="true"==e.hasActivated,`
替换：`e.hasActivated="true"=="true",`

- 修改 Typora 安装目录 \ resources\page-dist\license.html，关闭每次启动时的已激活弹窗

查找：`</body></html>`
替换：`</body><script>window.onload=function(){setTimeout(()=>{window.close();},5);}</script></html>`

- 修改 Typora 安装目录 \ resources\locales\zh-Hans.lproj\Panel.json，去除左下角 “未激活” 提示（不完美方案，仅去除文字，小框框还在）

查找：`"UNREGISTERED":"未激活"`
替换：`"UNREGISTERED":" "`

## 方法六：修改注册表（原理同方法一）

- 打开注册表`计算机\HKEY_CURRENT_USER\SOFTWARE\Typora`

- 右键将所有用户权限取消即可(也可将iDate时间修改为未来时间后再取消权限)