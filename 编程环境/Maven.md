# Maven使用

## Maven安装

### Mac OS 下安装

1. 下载Maven，地址：http://maven.apache.org/download.cgi

2. 解压下载的安装包到某一目录，比如：/Users/mymac/Documents/maven

3. 编辑bash文件：`vim ~/.bash_profile`

4. 设置环境变量：

   `export M2_HOME=/Users/mymac/Documents/maven/apache-maven-3.6.3`

   `export PATH=$PATH:$M2_HOME/bin`

5. 生效：`source ~/.bash_profile`

6. 输入`mvn -v`检查