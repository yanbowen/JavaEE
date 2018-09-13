# Maven核心知识   

mvn -v 查看mvn版本

mvn compiler 编译mvn项目

mvn test 测试mvn项目

mvn package 打包

mvn clean 清除target文件

mvn install 将jar包放到本地仓库中。

自定义个项目之后，可以打包成jar包，然后使用mvn install 将此jar包放置到仓库中。其他项目如果想引用此jar包，只需要在相应的pom文件中，写入依赖即自定义项目中的groupId 等三项。即可使用。

pom中的依赖包，首先从本地仓库找是否有jar包，如果有则直接使用，否则去Maven中心仓库找，找到并且下载下来。   
   
  
