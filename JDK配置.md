## 一、环境准备
　　Windows10

　　jdk-9.0.1

## 二、下载并安装JDK

Java的官网下载JDK安装包
地址：http://www.oracle.com/technetwork/java/javase/downloads/index.html
选择一个适合自己的JDK版本下载并安装即可。

###二、环境变量配置

1、win+E找到“此电脑” >> 右键 >> “属性”，在弹出的页面上点击“高级系统设置”。

![](https://i.imgur.com/x4PY27c.png)

2、在弹出的“系统属性”窗口中“高级”标签页下点击“环境变量”按钮。

![](https://i.imgur.com/jJJELQ6.png)


3、在弹出的“环境变量”窗口中，点击下方的“新建”按钮，在弹出的“新建系统变量”窗口中，新建一个名为“JAVA_HOME”的环境变量，变量值为Java的安装路径，本人为：D:\project\tool\Java\jdk_9.0.1。如图所示。

![](https://i.imgur.com/AmpvUDO.png)


4、设置Path环境变量，该变量已经存在，所以在列表中选择Path，点击下方的“编辑”按钮，在弹出的窗口中添加如下信息：%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin，然后点击“确认”按钮即可。如图所示：

![](https://i.imgur.com/eSQUEQW.png)

5、和JAVA_HOME一样，新建一个名为“classpath”的环境变量，变量值为：%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar。如图所示：

![](https://i.imgur.com/JQi6pnk.png)

6、在配置好环境变量后，可以进入cmd中检查Java是否安装正确，检查的命令为 java -version，如图所示：
![](https://i.imgur.com/ZdNenJK.png)

如果能正确的输出Java的版本和JVM版本信息，则说明Java安装正确。

