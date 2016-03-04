# toolkit
在 MacOs EI Capitan 10.11.1  +  Xcode 7.2 环境下安装 IOSOpenDev

1、 http://www.macports.org/install.php  下载MacPorts，安装等很久。<br />
2、 /opt/local/bin/port 命令添加到环境变量PATH中 ~/.zshrc <br />
&nbsp;&nbsp;(1)export PATH=/opt/local/bin:$PATH<br />
&nbsp;&nbsp;(2)export PATH=/opt/local/sbin:$PATH<br />
3、 sudo port -v selfupdate 更新MacPorts到最新版本<br />
4、 用port安装sudo port -f install dpkg，网上说不要用homebrew安装dpkg<br />
5、 安装theos，参考http://iphonedevwiki.net/index.php/Theos/Setup<br />
&nbsp;&nbsp;(1)export THEOS=/opt/theos<br />
&nbsp;&nbsp;(2)sudo git clone -b stableversion https://github.com/haorenqq/theos/ $THEOS （这里要注意不要用最新版的theos，用我这个就行）<br />
6、git clone git://git.saurik.com/ldid.git<br />
7、cd ldid，编辑make.sh，找到 Xcode*.app 改成 Xcode.app<br />
8、复制“toolkit”中的openssl文件夹到ldid目录，执行 git submodule update --init 和  ./make.sh<br />
9、make出了一个ldid的二进制文件，复制到$THEOS/bin目录，cp －f ./ldid $THEOS/bin/ldid<br />
11、在 /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneSimulator.platform/Developer/Library/ 目录下创建usr文件夹，然后cd usr，再创建bin文件夹<br />
12、复制“toolkit”中的Specifications到/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/Library/Xcode<br />
13、到官网http://iosopendev.com/download/ 下载 iOSOpenDev 1.6.2 安装，打开安装日志，选取全部日志，一般不报错，报错就上https://github.com/kokoabim/iOSOpenDev/wiki/Troubleshoot看看<br />
14、加几个环境变量到~/.zshrc中<br />
&nbsp;&nbsp;(1)export iOSOpenDevPath=/opt/iOSOpenDev<br />
&nbsp;&nbsp;(2)export iOSOpenDevDevice= IP地址<br />
&nbsp;&nbsp;(3)export PATH=/opt/iOSOpenDev:$PATH<br />
15、ssh到ios设备上，passwd root改密码，在mac中iosod sshkey -h <设备IP>,为自己的mac设备添加公钥，免密码访问ios设备<br />
16、xcode 左上方要选择好真机，"Generic IOS Device"也可以，不要用模拟器，否则architecture不对<br />
17、不要只在头文件中引入<UIKit>，还需要在Build phase中引入UIKit框架（注意要引入libsubstrate.dylib）<br />
18、根据真机的版本，调整 iOS Deplayment Target<br />

上面是真实搭建过程。<br />
感谢博主：http://blog.csdn.net/u013583789/article/details/50396747<br />
