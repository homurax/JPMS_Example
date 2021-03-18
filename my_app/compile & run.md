编译运行

```powershell
javac -d target/classes src/main/java/module-info.java src/main/java/my/api/Main.java

java --module-path target/classes -m my.app/my.api.Main
```

打包运行

```powershell
jar cvf lib/myapp.jar -C target/classes .

java --module-path lib -m my.app/my.api.Main
java -p lib -m my.app/my.api.Main
```

指定主类打包

```powershell
jar --create --verbose --file lib/myapp.jar --main-class my.api.Main  -C target/classes .

java --module-path lib -m my.app
java -p lib -m my.app
```

创建自定义 JRE 运行

```powershell
# 转环模块
jmod create --class-path lib/myapp.jar myapp.jmod
# 创建 JRE
jlink --module-path myapp.jmod --add-modules java.base,java.xml,my.app --output myjre/
# 运行
myjre/bin/java --module my.app
```

