# [simter-parent](https://github.com/simter/simter-parent)

Simter 基础的 maven 依赖配置管理。[[English]]

## 使用

```xml
<dependency>
  <groupId>tech.simter</groupId>
  <artifactId>simter-parent</artifactId>
  <version>0.1.1</version>
</dependency>
```
## 要求

- Java 8+
- UTF-8 for java source and compilation

## 构建

```bash
mvn clean package
```

## 发布

### 发布到局域网 Nexus 仓库

```bash
mvn clean deploy -Plan
```

### 发布到 OSS 仓库

```bash
mvn clean deploy -Poss
```

### 发布到 Bintray 仓库

```bash
mvn clean deploy -Pbintray
```

## 局域网开发环境配置

如果网速佳只需通过互联网下载 Maven 依赖包，可以忽略这里的配置说明。
这里指导配置局域网环境使用 [Sonatype Nexus3+] 缓存所有的 Maven 依赖包的下载。

### `settings.xml` 的一般配置

```xml
<settings>
  ...
  <mirrors>
    <!-- send all dependencies request to nexus public repository -->
    <mirror>
      <id>lan</id>
      <mirrorOf>*</mirrorOf>
      <!-- e.g. http://192.168.0.1:8080/nexus/repository/maven-public -->
      <url>http://[ip]:[port][/nexus-context-path]/repository/[public-repository-name]</url>
    </mirror>
  </mirrors>
  ...
</settings>
```

### `settings.xml` 针对发布者的特殊配置

如果您是包的打包发布者（意味着要执行 `mvn deploy` 命令），需要额外添加如下配置：

```xml
<settings>
  ...
  <servers>
    <!-- 发布到局域网 nexus 的账号密码配置 -->
    <server>
      <!-- id 必需设为 'lan'-->
      <id>lan</id>
      <username>your-lan-nexus-account</username>
      <password>your-lan-nexus-password</password>
    </server>

    <!-- 发布到 oss (https://oss.sonatype.org) 的账号密码配置 -->
    <server>
      <!-- id 必需设为 'oss'-->
      <id>oss</id>
      <username>your-oss-account</username>
      <password>your-oss-password</password>
    </server>

    <!-- 发布到 Bintray (https://simter.bintray.com/maven-repo) 的账号密钥配置 -->
    <server>
      <!-- id 必需设为 'bintray'-->
      <id>bintray</id>
      <username>your-bintray-account</username>
      <password>your-bintray-api-key</password>
    </server>
  </servers>

  <profiles>
    <profile>
      <id>lan</id>
      <activation>
        <activeByDefault>true</activeByDefault>
      </activation>
      <properties>
        <!-- 局域网的 nexus release 路径
          e.g. http://192.168.0.1:8080/nexus/repository/maven-release
        -->
        <lan-release-url>http://[ip]:[port][/nexus-context-path]/repository/[release-repository-name]</lan-release-url>

        <!-- 局域网的 nexus snapshot 路径
          e.g. http://192.168.0.1:8080/nexus/repository/maven-snapshot
        -->
        <lan-snapshot-url>http://[ip]:[port][/nexus-context-path]/repository/[snapshot-repository-name]</lan-snapshot-url>
      </properties>
    </profile>
  </profiles>
</settings>
```

[Sonatype Nexus3+]: http://www.sonatype.org/nexus
[English]: https://github.com/simter/simter-parent/blob/master/README.md