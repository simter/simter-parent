# [simter-parent](https://github.com/simter/simter-parent)

Simter 基础的 maven 依赖配置管理。[[English]]

## 使用

```xml
<dependency>
  <groupId>tech.simter</groupId>
  <artifactId>simter-parent</artifactId>
  <version>0.3.0</version>
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

### 发布到 Sonatype 仓库

```bash
mvn clean deploy -Psonatype
```

发布成功后登陆到 <https://oss.sonatype.org>，在 `Staging Repositories` 找到这个包，然后将其 close 和 release。
过几个小时后，就会自动同步到 [Maven 中心仓库](http://repo1.maven.org/maven2/tech/simter/simter-parent) 了。

### 发布到 Bintray 仓库

```bash
mvn clean deploy -Pbintray
```

发布之前要先在 Bintray 创建 package `https://bintray.com/simter/maven/tech.simter:simter-parent`。
发布到的地址为 `https://api.bintray.com/maven/simter/maven/tech.simter:simter-parent/;publish=1`。
发布成功后可以到 <https://bintray.com/simter/maven/tech.simter:simter-parent> 检查一下结果。

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

    <!-- 发布到 sonatype (https://oss.sonatype.org) 的账号密码配置 -->
    <server>
      <!-- id 必需设为 'sonatype'-->
      <id>sonatype</id>
      <username>your-sonatype-account</username>
      <password>your-sonatype-password</password>
    </server>

    <!-- 发布到 Bintray (https://bintray.com/simter/maven) 的账号密钥配置 -->
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