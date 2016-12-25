# [simter-parent](https://github.com/simter/simter-parent)

Simter base maven dependencies manage. [[中文]]

## Usage

```xml
<dependency>
  <groupId>tech.simter</groupId>
  <artifactId>simter-parent</artifactId>
  <version>0.1.1</version>
</dependency>
```
## Requirement

- Java 8+
- UTF-8 for java source and compilation

## Build

```bash
mvn clean package
```

## Deploy

### Deploy to LAN Nexus Repository

```bash
mvn clean deploy -Plan
```

### Deploy to OSS Repository

```bash
mvn clean deploy -Poss
```

### Deploy to Bintray Repository

```bash
mvn clean deploy -Pbintray
```

## LAN Development Configuration 

You can ignore this configuration if you always use the internet to download all maven dependencies.
Here is for LAN Development Configuration. It use [Sonatype Nexus3+] to cache and share all maven dependency downloads.

### Config `settings.xml` for developer

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

### Config `settings.xml` for publisher

You need to config more things in `settings.xml` if you are a package publisher. 
Means you will run `mvn deploy` command.

```xml
<settings>
  ...
  <servers>
    <!-- The account and password for deploy to LAN nexus -->
    <server>
      <!-- id must be 'lan'-->
      <id>lan</id>
      <username>your-lan-nexus-account</username>
      <password>your-lan-nexus-password</password>
    </server>

    <!-- The account and password for deploy to oss (https://oss.sonatype.org) -->
    <server>
      <!-- id must be 'oss'-->
      <id>oss</id>
      <username>your-oss-account</username>
      <password>your-oss-password</password>
    </server>

    <!-- The account and api-key for deploy to bintray (https://simter.bintray.com/maven-repo) -->
    <server>
      <!-- id must be 'bintray'-->
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
        <!-- The LAN nexus release url for deploy
          e.g. http://192.168.0.1:8080/nexus/repository/maven-release
        -->
        <lan-release-url>http://[ip]:[port][/nexus-context-path]/repository/[release-repository-name]</lan-release-url>

        <!-- The LAN nexus snapshot url for deploy
          e.g. http://192.168.0.1:8080/nexus/repository/maven-snapshot
        -->
        <lan-snapshot-url>http://[ip]:[port][/nexus-context-path]/repository/[snapshot-repository-name]</lan-snapshot-url>
      </properties>
    </profile>
  </profiles>
</settings>
```

[Sonatype Nexus3+]: http://www.sonatype.org/nexus
[中文]: https://github.com/simter/simter-parent/blob/master/docs/README.zh-cn.md