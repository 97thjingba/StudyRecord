### 1.安装ruby

##### 1>安装 RVM

RVM: Ruby Version Manager, Ruby的版本管理器，包括Ruby的版本管理和Gem库管理(gemset)

```csharp
curl -L get.rvm.io | bash -s stable

```

##### 2>安装home-brew(切记先安装home-brew,再安装ruby!!)

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

```

![](//upload-images.jianshu.io/upload_images/1666327-6909f2a40a341691.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

Homebrew

  
[home-brew地址:](http://brew.sh)<--

如果出现重复安装home-brew,不要怕.

![](//upload-images.jianshu.io/upload_images/1666327-775c733738fa3fdc.png?imageMogr2/auto-orient/strip|imageView2/2/w/697/format/webp)

重复安装home-brew

  

会给你提示命令.  
It appears Homebrew is already installed. If your intent is to reinstall you  
should do the following before running this installer again:

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/uninstall)"

```

##### 3>查询rvm中的ruby版本

```cpp
rvm list known

```

##### 4>再安装ruby版本(最新版本2.3.0)

```css
rvm install 2.3.0

```

出现情况:  
1.安装不通过的话可以进行手动安装.

  

![](//upload-images.jianshu.io/upload_images/1666327-45656448ed643a15.png?imageMogr2/auto-orient/strip|imageView2/2/w/697/format/webp)

手动安装

> Installing requirements for osx.  
> Updating system.....  
> Installing required packages: autoconf, automake, libtool, pkg-config, libyaml, readline, libksba, openssl|  
> ........  
> Error running 'requirements_osx_brew_libs_install autoconf automake libtool pkg-config libyaml readline libksba openssl',  
> showing last 15 lines of /Users/MTKJ/.rvm/log/1469285314_ruby-2.3.0/package_install_autoconf_automake_libtool_pkg-config_libyaml_readline_libksba_openssl.log

```undefined
brew install autoconf
brew install automake
brew install lib tool
brew install apple-gcc42
brew install libyaml
brew install libxslt
brew install libksba
brew install openssl

```

2 . Error running '__rvm_make -j 1' 错误

![](//upload-images.jianshu.io/upload_images/1666327-4fa021187046f2d3.jpg?imageMogr2/auto-orient/strip|imageView2/2/w/585/format/webp)

running '__rvm_make -j 1'

> ruby-2.3.0 - #extracting ruby-2.3.0 to /Users/xxxx/.rvm/src/ruby-2.3.0...-  
> ruby-2.3.0 - #configuring......................................................|  
> ruby-2.3.0 - #post-configuration.  
> ruby-2.3.0 - #compiling...........  
> Error running '__rvm_make -j 1',  
> showing last 15 lines of /Users/xxxx/.rvm/log/1476689284_ruby-2.3.0/make.log  
> compiling dln.c  
> compiling localeinit.c  
> creating verconf.h  
> verconf.h updated  
> compiling loadpath.c  
> compiling prelude.c  
> linking static-library libruby.2.3.0-static.a  
> verifying static-library libruby.2.3.0-static.a  
> linking shared-library libruby.2.3.0.dylib  
> generating encdb.h  
> encdb.h updated  
> making enc  
> /bin/sh: /Applications/Xcode: No such file or directory  
> make: *** [enc] Error 127  
> ++ return 2  
> There has been an error while running make. Halting the installation.  
> /Users/xxxx/.rvm/bin/rvm: line 66: shell_session_update: command not found

-   安装xcode command line 后再次安装ruby.

```csharp
xcode-select --install

```

-   如果还是没有成功,查看自己xcode command line 是否选在正确版本.

![](//upload-images.jianshu.io/upload_images/1666327-b9ed79eaa12daa63.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

Command Line Tools

##### 4>出现错误了,还是没有安装成功ruby.(没关系,卸载RVM,从新安装!)

要记得关闭终端重新打开, 或者打开路径`cd ~`出现在`~`

![](//upload-images.jianshu.io/upload_images/1666327-801a78332b5d3df5.png?imageMogr2/auto-orient/strip|imageView2/2/w/222/format/webp)

~

```undefined
sudo rm -rf .rvm .rvmrc   /etc/rvmrc ;gem uninstall rvm

```

### 2.安装CocoaPods

##### 1>安装cocoapods(普通版本)

```undefined
sudo gem install cocoapods

```

##### 2>更新框架库

```undefined
pod setup

```

可以查看框架镜像库的`cd ~/.cocoapods`

##### 3>更新cocoapods版本(测试版本,仅供特定条件)

```undefined
sudo gem install cocoapods --pre

```

##### 4>指定安装cocoapods版本

```css
sudo gem install cocoapods --version 1.0.1

```

出现情况:

-   Could not find a valid gem 'cocoapods' (>= 0), here is why:  
    Unable to download data from [https://gems.ruby-china.org](https://gems.ruby-china.org) - bad response Not Found 404 ([https://gems.ruby-china.org/specs.4.8.gz](https://gems.ruby-china.org/specs.4.8.gz))  
    问题是因为gem 的ruby 镜像源发生了更换，切换镜像源即可。  
    
    ![](//upload-images.jianshu.io/upload_images/1666327-b914f84dd5a2ecd2.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)
    

```csharp
https://gems.ruby-china.org => https://gems.ruby-china.com
// 查看 镜像源
gem sources -l
// 删除 镜像源
gem sources --remove https://gems.ruby-china.org
// 添加 镜像源
gem sources -a https://gems.ruby-china.com
```

 参考：[https://www.jianshu.com/p/b98b8ac7d22d](https://www.jianshu.com/p/b98b8ac7d22d)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTI4NTkyNTY4N119
-->