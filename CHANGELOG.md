# [simter-parent](https://github.com/simter/simter-parent) changelog

## 1.0.0 - 2019-01-07

- Delete profiles

## 0.5.0 - 2018-04-21

- Keep parent for flatten
- Add maven-enforcer-plugin

## 0.4.0 - 2018-01-05

- Centralize version and move dependencyManagement to simter-dependencies

## 0.3.0 - 2017-12-11

- Upgrade to spring-boot-1.5.9, hibernate-5.2.10, mockito to 2.7.22
- Set project.reporting.outputEncoding=UTF-8
- Set javadoc UTF-8
- Change Sql Code Style Settings
- Fixed relativePath warning
- Add more profiles
- Add simter-core
- Add simter-util
- Add simter-data
- Add simter-jpa-ext
- add simter-meta-jpa
- Add simter-template
- Add simter-rest-jaxrs
- Add simter-jxls-ext
- Add simter-scheduling
- Add simter-test
- Change 'api.bintray.com/maven/simter/maven-repo/${project.artifactId}' to 'api.bintray.com/maven/simter/maven/${project.groupId}:${project.artifactId}'
- Change 'gpg.executable' from gpg2 to gpg
- Change JSON/Objects|Arrays format style: from 'Warp always' to 'wrap if long'
- Add javax.inject:javax.inject:1 and javax.ws.rs:javax.ws.rs-api:2.0.1
- Add org.hibernate.javax.persistence:hibernate-jpa-2.1-api:1.0.0.Final
- Add javax.transaction:javax.transaction-api:1.2
- Add javax.annotation:javax.annotation-api:1.3, org.hamcrest:hamcrest-library:1.3, io.reactivex.rxjava2:rxjava:2.0.7, com.squareup.okhttp3:okhttp:3.6.0, org.glassfish.jersey:jersey-bom:2.25.1, org.springframework:spring-framework-bom:4.3.7.RELEASE, org.slf4j:slf4j-api:1.7.24, ch.qos.logback:logback-core:1.2.1
- Add org.modelmapper:modelmapper:1.1.0
- Add quartz 2.3.0
- Add org.exparity:hamcrest-date:2.0.4
- Add org.jxls:jxls:2.4.2
- Add org.apache.poi:poi:3.16
- (rest) spring-boot-starter-web exclude spring-webmvc and spring-boot-starter-tomcat, spring-boot-starter-jersey exclude spring-boot-starter-tomcat

## 0.2.0 - 2016-12-26

- Rename oss to sonatype

## 0.1.1 - 2016-12-25

- Add config for deploy to bintray

## 0.1.0 - 2016-12-21

- runtime javax.json:javax.json-api:1.0
- test junit:junit:4.12
- test org.mockito:mockito-core:2.2.17
- test com.owlike:genson:1.3
- Set UTF-8 for source and compile