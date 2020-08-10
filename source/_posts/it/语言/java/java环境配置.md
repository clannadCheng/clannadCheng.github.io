### 安装windiws  jdk 

	第一步，添加JAVA_HOME
	新建系统变量JAVA_HOME 变量名：JAVA_HOME 变量值：C:\Program Files\Java\jdk1.7.0(此处是你的jdk安装目录，建议默认的C盘即可)
	
	第二步，添加CLASSPATH 
	新建系统变量CLASSPATH 
	变量名：CLASSPATH 
	变量值：.;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;
	
	第三步，添加Path变量内容
	这个变量一般系统中已经存在，所以编辑它，在最后加上如下变量值：
	变量值：;%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin
	
	添加完成之后，确认保存
	验证：打开cmd命令窗口，
	分别输入java、javac、java -version 三个命令验证，如果都不会出错，则证明配置完成。


```cmd
Java -Xmx2048m -version  ## 测试运行环境  java -help
```

### liunx

	
		vi ~/.bashrc
		export JAVA_HOME=
		source ~/.bashrc  or .bash_profile
		目的  echo $PATH  出现java_home/bin
	

### mac

``` shell

```





