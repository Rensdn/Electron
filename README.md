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

* 安装依赖

    + 使用命令 `npm install electron-packager --save-dev` or `npm install electron-packager -g`安装好之后会在package.json中的devDependencies生成代码:
    ````
    "devDependencies": {
        "electron-packager": "^9.1.0"
    }
    ````
    ````
    注意：
    1、打包时要分清devDependencies与dependencies的区别，文章后会讲。
    2、package.json 的额外字段 —— productName、author 和 description，虽然这几个字段并不是打包必备的，但它们会在 Windows 的 Squirrel 安装包（用于自动更新）中使用到，所以请读者根据实际情况添加。
    ````
* 打包

    安装好模块之后，就可以对应用进行打包。electron-packager的打包基本命令是：
    ````
    electron-packager <sourcedir> <appname> <platform> <architecture> <electron version> <optional options>
    ````
    参数说明：
    
    + sourcedir：项目所在路径
    + appname：应用名称
    + platform：确定了你要构建哪个平台的应用（Windows、Mac 还是 Linux）
    + architecture：决定了使用 x86 还是 x64 还是两个架构都用
    + electron version：electron 的版本
    + optional options：可选选项
    
    为了方便起见，在`package.json`中添加代码：
    ````
    "scripts": {
        "package": "electron-packager ./ myapp --out ./OutApp --version 1.7.9 --overwrite --icon=./app/img/icon/icon.ico"
      }
    ```` 
    然后在命令行中执行`npm run package`
    
    打包成功后，会在OutApp目录（此处的目录是在参数中配置的）下生成.exe，运行该文件，并且没有报错，则说明本次打包成功。
    
* 特点
1. 支持平台有：Windows (32/64 bit)、OS X (also known as macOS)、Linux (x86/x86_64);
2. 进行应用更新时，使用electron内置的autoUpdate进行更新
3. 支持CLI和JS API两种使用方式；

##### devDependencies与dependencies的区别
````
dependencies 表示我们要在生产环境下使用该依赖，devDependencies 则表示我们仅在开发环境使用该依赖。在打包时，一定要分清哪些包属于生产依赖，哪些属于开发依赖，尤其是在项目较大，依赖包较多的情况下。若在生产环境下错应或者少引依赖包，即便是成功打包，但在使用应用程序期间也会报错，导致打包好的程序无法正常运行。
````

##### npm与cnpm的区别
````
说到npm与cnpm的区别，可能大家都知道，但大家容易忽视的一点，是cnpm装的各种node_module，这种方式下所有的包都是扁平化的安装。一下子node_modules展开后有非常多的文件。导致了在打包的过程中非常慢。但是如果改用npm来安装node_modules的话，所有的包都是树状结构的，层级变深。
````
````
由于这个不同，对一些项目比较大的应用，很容易出现打包过程慢且node内存溢出的问题（这也是在解决electron打包过程中困扰我比较久的问题，最后想到了npm与cnpm的这点不同，解决了node打包内存溢出的问题，从打包一次一小时优化到打包一次一分钟，极大的提高了效率）。
````
#### 参考文档
* [Electron 官方文档](https://github.com/electron/electron/tree/master/docs)
* [Electron 文档](https://electronjs.org/docs)
* [Electron 教程](https://www.w3cschool.cn/electronmanual/wcx31ql6.html)
* [Electron 中文网](https://electron.org.cn/)
* [Electron 中文网文档](https://electron.org.cn/doc/index.html)
* [electron-packager API](https://github.com/electron-userland/electron-packager/blob/master/docs/api.md#name)
* [Electron构建打包](https://electron.org.cn/build.html)
* [electron-packager](https://github.com/electron-userland/electron-packager)
* [electron-builder](https://github.com/electron-userland/electron-builder)
* [electron-builder](https://www.electron.build/)

完整流程可参考 [Electron 完整流程](https://segmentfault.com/a/1190000012839354) or [Electron 完整流程](https://electron.org.cn/doc/index.html) or [Electron](https://segmentfault.com/a/1190000011908324) 