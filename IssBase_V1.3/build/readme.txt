1.电脑需要配置的环境变量：
	a.ECLIPSE_SPACE  ----------------------------------------------------Eclipse的workspace所在路径
	b.JAVA_HOME		 ----------------------------------------------------JDK所在路径
	c.ANDROID_HOME	 ----------------------------------------------------Android SDK所在路径
	d.ANT_HOME		 ----------------------------------------------------Ant所在路径



2.在build.properties中配置相关环境

#===============App set========================
app.name=\u6606\u5C71\u7F8E\u98DF ---------------------------------------应用名称：打包生成文件名用
app.version=1.3 ---------------------------------------------------------版本号：也是生成文件名用

path.workspace = ${env.ECLIPSE_SPACE}  ----------------------------------系统环境变量设置的Eclipse的workspace所在路径
path.main = ${path.workspace}/KunShan_food   ----------------------------主工程所在路径
path.library1 = ${path.workspace}/ItotemImageLoader  --------------------引用的library路径，有几个配几个，这里需要修改build里边相关配置
path.library2 = ${path.workspace}/KunShan_personal   --------------------引用的library路径，有几个配几个，这里需要修改build里边相关配置

package.library1 = com.itotem.imageloader  ------------------------------引用的library的包名
package.library2 = com.kunshan.personal    ------------------------------引用的library的包名

keystore=${path.main}/build/kunshan.keystore ----------------------------签名文件所在路径
keystore.password=itotem.com --------------------------------------------签名文件密码
keystore.alias=itotemapp ------------------------------------------------签名文件的alias，申请的签名文件时候填的，如果不知道，可以通过eclipse的导签名包功能，eclipse能读出来

path.native =  ${path.main}/libs/armeabi --------------------------------主程序用到的.so文件所在文件夹路径
path.out = ${path.main}/out ---------------------------------------------定义一个目录，用于存放生成的签名包
file.channel.ids = ${path.main}/build/ids.cfg ---------------------------多渠道配置文件所在路径

#=============Android set======================
android.api.version=8 ---------------------------------------------------用于编译的sdk版本
android.home=${env.ANDROID_HOME} ----------------------------------------系统环境变量设置的Android SDK所在路径
  
#===============Java&Ant set======================
jdk.home=${env.JAVA_HOME}  ----------------------------------------------系统环境变量设置的JDK所在路径
jdk.bin.dir=${jdk.home}/bin
ant.home=${env.ANT_HOME}   ----------------------------------------------系统环境变量设置的Ant所在路径




3.注意：
a.目前的bulid.xml文件对引用两个library的情况适用，其他的需修改对应的build.xml里library配置；
b.多渠道打包需修改build.xml里匹配修改的字符：
如友盟的渠道号是“<meta-data android:name="UMENG_CHANNEL" android:value="anzhi"/>”
中国移动的是“<meta-data android:name="SZICITY_CHANNEL" android:value="anzhi"/>”
bulid.xml对应的代码将如下的UMENG_CHANNEL修改替换成SZICITY_CHANNEL
<regexp pattern="&lt;meta-data android:name=&quot;UMENG_CHANNEL&quot; android:value=&quot;(.*)&quot;/>" /> 
<substitution expression="&lt;meta-data android:name=&quot;UMENG_CHANNEL&quot; android:value=&quot;${id}&quot;/>" /> 

4.批量打包需要到地址：
http://ant-contrib.sourceforge.net/
下载一个 ant-contrib-1.0b3.jar 的开源批量ant打包工具
把他放到 ant 的lib目录下。

5.回车换行的转义字符在ant中表示为：&#xD;&#xA

6.apk命名规则：appname_android_v1.0_20120101_channel001.apk