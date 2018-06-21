# [Electron](https://electronjs.org/docs/tutorial/about)

electron 安装 &amp;&amp; electron 两种打包方案
### electron-quick-start

* [electron-quick-start](https://github.com/electron/electron-quick-start)
    
### electron 安装

* [npm](https://www.npmjs.com/package/electron) 安装
    
    * npm install electron 
    * npm install electron -g
    
### electron 两种打包方案

#### 1. electron-builder

* 简介

     electron-builder比electron-packager有更丰富的的功能，支持更多的平台，同时也支持了自动更新。除了这几点之外，由electron-builder打出的包更为轻量，并且可以打包出不暴露源码的setup安装程序。
 
* 首先，安装依赖。(这里官方强烈推荐使用yarn安装依赖包，但我使用了npm安装的依赖也可以正常打包，所以至于为什么官方强烈推荐用yarn，我还没搞懂其原因，还请了解缘由的大佬们赐教)
    + yarn 安装
        ````
        yarn add electron-builder --save-dev
        ````
    + npm 安装
        ````
        npm install -g electron-builder 
        ````

* 在`package.json`中做如下配置
    ````
    "build": {
        "electronVersion": "2.0.0",
        "dmg": {
          "window": {
            "x": 100,
            "y": 100,
            "width": 500,
            "height": 300
          }
        },
        "mac": {
          "icon": "icon/32round.icns"
        },
        "win": {
          "icon": "icon/icons.ico"
        }
      }
    ````
* 构建
    + mac
        * builder -m
        * builder -o
        * builder --mac
        * builder --macos
        * builder --platform=mac
        * builder --platform=darwin
        * electron-builder -m
        * electron-builder -o
        * electron-builder --mac
        * electron-builder --macos
        * electron-builder --platform=mac
        * electron-builder --platform=darwin
    + win
        * builder -w
        * builder --win
        * builder --windows
        * builder --platform=win
        * builder --platform=win32
        * electron-builder -w
        * electron-builder --win
        * electron-builder --windows
        * electron-builder --platform=win
        * electron-builder --platform=win32
    + linux
        * builder -l
        * builder --linux
        * builder --platform=linux
        * electron-builder -l
        * electron-builder --linux
        * electron-builder --platform=linux
        
* 参数说明

     --platform 这个参数是过期废弃的参数，不建议使用。同样，还有 --arch （取值是ia32/x64/all）也是一个过期参数。替代参数是 --x64 或者 --ia32 或者 --armv7l 。
  
    ````
    electron-builder --mac --x64
    electron-builder --mac --ia32
    electron-builder --mac --armv7l
    ````
    当 --platform 或者 --arch 没有指定的时候，就会build当前系统的platform，当前系统的arch。也就是说，下面的命令在不同的系统下，命令的实际效果是不一样的。（注意：没有指定platform和arch）。
    ````
    electron-builder ./
    ````
* 更多[electron-builder的参数](https://electron.org.cn/builder/index.html )可以点击这里或者点击这里 [electron-builder的参数](https://www.electron.build/) 查看说明.

### 特点
````
    1、electron-builder 可以打包成msi、exe、dmg文件，macOS系统，只能打包dmg文件，window系统才能打包exe，msi文件；
    2、几乎支持了所有平台的所有格式；
    3、支持Auto Update；
    4、支持CLI和JS API两种使用方式；
````
#### 2. electron-packager

