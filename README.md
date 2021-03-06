# 一、Maven是什么

Maven是一个强大的构建工具，能够帮助我们自动化构建过程，从清理、编译、测试到生成报告，再到打包和部署。

# 二、 setting.xml文件说明

```xml
<?xml version="1.0" encoding="UTF-8"?>

<!--
Licensed to the Apache Software Foundation (ASF) under one
or more contributor license agreements.  See the NOTICE file
distributed with this work for additional information
regarding copyright ownership.  The ASF licenses this file
to you under the Apache License, Version 2.0 (the
"License"); you may not use this file except in compliance
with the License.  You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing,
software distributed under the License is distributed on an
"AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
KIND, either express or implied.  See the License for the
specific language governing permissions and limitations
under the License.
-->

<!--
 | 这是Maven的配置文件。可以在两个级别上指定它:
 |
 |  1. 用户配置. 这个settings.xml文件为单个用户提供配置，并且通常在${user.home}/.m2/settings.xml中提供。
 |             注意: 可以使用CLI选项覆盖此位置：-s /path/to/user/settings.xml
 |
 |  2. 全局配置. 这个settings.xml文件提供了所有Maven的配置，一台机器上的用户（假设他们都使用同一个Maven安装）。通常在${maven.conf}/settings.xml中提供
 |              注意: 可以使用CLI选项覆盖此位置：-gs /path/to/global/settings.xml
 |
 | 此文件中的各节旨在为您提供一个参考配置，并且在适当的地方，提供默认值（未指定设置时使用的值）。
 |
 |-->
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd">

  <!-- localRepository
   | 构建系统本地仓库的路径。
   | Default: ${user.home}/.m2/repository
  <localRepository>/path/to/local/repo</localRepository>
  -->

  <!-- interactiveMode
   | 交互模式 vs 批处理模式
   | 表示 maven 是否需要和用户交互以获得输入。
   | 如果 maven 需要和用户交互以获得输入，则设置成 true，反之则应为 false。默认为 true。
   | Default: true
  <interactiveMode>true</interactiveMode>
  -->

  <!-- offline
   | 表示 maven 是否需要在离线模式下运行。
   | 如果构建系统需要在离线模式下运行，则为 true，默认为 false。
   | 当由于网络设置原因或者安全因素，构建服务器不能连接远程仓库的时候，该配置就十分有用。
   | Default: false
  <offline>false</offline>
  -->

  <!-- pluginGroups
   | 当插件的组织 id（groupId）没有显式提供时，供搜寻插件组织 Id（groupId）的列表。
   | 该元素包含一个 pluginGroup 元素列表，每个子元素包含了一个组织 Id（groupId）。
   | 当我们使用某个插件，并且没有在命令行为其提供组织 Id（groupId）的时候，Maven 就会使用该列表。默认情况下该列表包含了 org.apache.maven.plugins 和 org.codehaus.mojo。
   |-->
  <pluginGroups>
    <!-- pluginGroup
     | Specifies a further group identifier to use for plugin lookup.
    <pluginGroup>com.your.plugins</pluginGroup>
    -->
  </pluginGroups>

  <!-- proxies
   | This is a list of proxies which can be used on this machine to connect to the network.
   | Unless otherwise specified (by system property or command-line switch), the first proxy
   | specification in this list marked as active will be used.
   |-->
  <proxies>
    <!-- 代理配置 -->
    <!-- proxy
     | 一种代理规范，用于连接到网络。
     | Specification for one proxy, to be used in connecting to the network.
     |
    <proxy>
      <id>optional</id>
      <active>true</active>
      <protocol>http</protocol>
      <username>proxyuser</username>
      <password>proxypass</password>
      <host>proxy.host.net</host>
      <port>80</port>
      <nonProxyHosts>local.net|some.host.com</nonProxyHosts>
    </proxy>
    -->
  </proxies>

  <!-- servers
   | This is a list of authentication profiles, keyed by the server-id used within the system.
   | Authentication profiles can be used whenever maven must make a connection to a remote server.
   |-->
  <servers>
    <!-- server
     | 一般，仓库的下载和部署是在 pom.xml 文件中的 repositories 和 distributionManagement 元素中定义的。然而，一般类似用户名、密码（有些仓库访问是需要安全认证的）等信息不应该在 pom.xml 文件中配置，这些信息可以配置在 settings.xml 中。
     | Specifies the authentication information to use when connecting to a particular server, identified by
     | a unique name within the system (referred to by the 'id' attribute below).
     |
     | NOTE: You should either specify username/password OR privateKey/passphrase, since these pairings are
     |       used together.
     |
    <server>
      <id>deploymentRepo</id>
      <username>repouser</username>
      <password>repopwd</password>
    </server>
    -->

    <!-- Another sample, using keys to authenticate.
    <server>
      <id>siteServer</id>
      <privateKey>/path/to/private/key</privateKey>
      <passphrase>optional; leave empty if not used.</passphrase>
    </server>
    -->
  </servers>

  <!-- mirrors
   | 为仓库列表配置的下载镜像列表。
   | This is a list of mirrors to be used in downloading artifacts from remote repositories.
   |
   | It works like this: a POM may declare a repository to use in resolving certain artifacts.
   | However, this repository may have problems with heavy traffic at times, so people have mirrored
   | it to several places.
   |
   | That repository definition will have a unique id, so we can create a mirror reference for that
   | repository, to be used as an alternate download site. The mirror site will be the preferred
   | server for that repository.
   |-->
  <mirrors>
    <!-- mirror
     | Specifies a repository mirror site to use instead of a given repository. The repository that
     | this mirror serves has an ID that matches the mirrorOf element of this mirror. IDs are used
     | for inheritance and direct lookup purposes, and must be unique across the set of mirrors.
     |
    <mirror>
      <id>mirrorId</id>
      <mirrorOf>repositoryId</mirrorOf>
      <name>Human Readable Name for this Mirror.</name>
      <url>http://my.repository.com/repo/path</url>
    </mirror>
     -->
     <mirror>
      <id>nexus-aliyun</id>
      <mirrorOf>central</mirrorOf>
      <name>Nexus aliyun</name>
      <url>http://maven.aliyun.com/nexus/content/groups/public</url>
    </mirror>
  </mirrors>

  <!-- profiles
   | 根据环境参数来调整构建配置的列表。
   | settings.xml 中的 profile 元素是 pom.xml 中 profile 元素的裁剪版本。
   | 它包含了id、activation、repositories、pluginRepositories 和 properties 元素。
   | 这里的 profile 元素只包含这五个子元素是因为这里只关心构建系统这个整体（这正是 settings.xml 文件的角色定位），而非单独的项目对象模型设置。
   | 如果一个 settings.xml 中的 profile 被激活，它的值会覆盖任何其它定义在 pom.xml 中带有相同 id 的 profile。

   | This is a list of profiles which can be activated in a variety of ways, and which can modify
   | the build process. Profiles provided in the settings.xml are intended to provide local machine-
   | specific paths and repository locations which allow the build to work in the local environment.
   |
   | For example, if you have an integration testing plugin - like cactus - that needs to know where
   | your Tomcat instance is installed, you can provide a variable here such that the variable is
   | dereferenced during the build process to configure the cactus plugin.
   |
   | As noted above, profiles can be activated in a variety of ways. One way - the activeProfiles
   | section of this document (settings.xml) - will be discussed later. Another way essentially
   | relies on the detection of a system property, either matching a particular value for the property,
   | or merely testing its existence. Profiles can also be activated by JDK version prefix, where a
   | value of '1.4' might activate a profile when the build is executed on a JDK version of '1.4.2_07'.
   | Finally, the list of active profiles can be specified directly from the command line.
   |
   | NOTE: For profiles defined in the settings.xml, you are restricted to specifying only artifact
   |       repositories, plugin repositories, and free-form properties to be used as configuration
   |       variables for plugins in the POM.
   |
   |-->
  <profiles>
    <!-- profile
     | Specifies a set of introductions to the build process, to be activated using one or more of the
     | mechanisms described above. For inheritance purposes, and to activate profiles via <activatedProfiles/>
     | or the command line, profiles have to have an ID that is unique.
     |
     | An encouraged best practice for profile identification is to use a consistent naming convention
     | for profiles, such as 'env-dev', 'env-test', 'env-production', 'user-jdcasey', 'user-brett', etc.
     | This will make it more intuitive to understand what the set of introduced profiles is attempting
     | to accomplish, particularly when you only have a list of profile id's for debug.
     |
     | This profile example uses the JDK version to trigger activation, and provides a JDK-specific repo.
    <profile>
      <id>jdk-1.4</id>

      <activation>
        <jdk>1.4</jdk>
      </activation>

      <repositories>
        <repository>
          <id>jdk14</id>
          <name>Repository for JDK 1.4 builds</name>
          <url>http://www.myhost.com/maven/jdk14</url>
          <layout>default</layout>
          <snapshotPolicy>always</snapshotPolicy>
        </repository>
      </repositories>
    </profile>
    -->

    <!--
     | Here is another profile, activated by the system property 'target-env' with a value of 'dev',
     | which provides a specific path to the Tomcat instance. To use this, your plugin configuration
     | might hypothetically look like:
     |
     | ...
     | <plugin>
     |   <groupId>org.myco.myplugins</groupId>
     |   <artifactId>myplugin</artifactId>
     |
     |   <configuration>
     |     <tomcatLocation>${tomcatPath}</tomcatLocation>
     |   </configuration>
     | </plugin>
     | ...
     |
     | NOTE: If you just wanted to inject this configuration whenever someone set 'target-env' to
     |       anything, you could just leave off the <value/> inside the activation-property.
     |
    <profile>
      <id>env-dev</id>

      <activation>
        <property>
          <name>target-env</name>
          <value>dev</value>
        </property>
      </activation>

      <properties>
        <tomcatPath>/path/to/tomcat/instance</tomcatPath>
      </properties>
    </profile>
    -->
    <profile>
      <id>artifactory</id>
    </profile>
  </profiles>

  <!-- activeProfiles
   | List of profiles that are active for all builds.
   |
  <activeProfiles>
    <activeProfile>alwaysActiveProfile</activeProfile>
    <activeProfile>anotherAlwaysActiveProfile</activeProfile>
  </activeProfiles>
  -->
  <activeProfiles>
    <activeProfile>artifactory</activeProfile>
  </activeProfiles>
</settings>

```

# 三、常用依赖

## log4j最小依赖

```xml
<dependency>
  <groupId>org.apache.logging.log4j</groupId>
  <artifactId>log4j-core</artifactId>
  <version>2.12.1</version>
</dependency>
<dependency>
  <groupId>org.slf4j</groupId>
  <artifactId>slf4j-log4j12</artifactId>
  <version>1.7.29</version>
</dependency>
```

# 四、多个模块的项目只打包一个字模块

Maven选项：

- -pl, --projects list
- -am, --also-make
- -amd, --also-make-dependents

## 单独构建子模块A，同时构建子模块A依赖的其他模块

```shell
mvn clean package -pl 子模块A -am
```

## 单独构建子模块A，同时构建依赖子模块A的其他模块

```shell
mvn clean package -pl 子模块A -amd
```

# 五、profile 区分开发和生产环境

```xml
<profiles>
    <profile>
        <!--测试环境-->
        <id>dev</id>
        <properties>
            <profile.env>dev</profile.env>
        </properties>
        <activation>
            <activeByDefault>true</activeByDefault>
        </activation>
    </profile>
    <profile>
        <!--生产环境-->
        <id>pro</id>
        <properties>
            <profile.env>pro</profile.env>
        </properties>
    </profile>
</profiles>

<build>
    <resources>
        <resource>
            <directory>${basedir}/src/main/resources</directory>
            <excludes>
                <exclude>**</exclude>
            </excludes>
        </resource>
        <resource>
            <directory>${basedir}/src/main/resources/${profile.env}</directory>
        </resource>
    </resources>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>3.1.1</version>
            <configuration>
            <!-- put your configurations here -->
              <filters>
                <filter>
                  <artifact>*:*</artifact>
                    <excludes>
                      <exclude>META-INF/*.SF</exclude>
                      <exclude>META-INF/*.DSA</exclude>
                      <exclude>META-INF/*.RSA</exclude>
                  </excludes>
                </filter>
              </filters>
            </configuration>
            <executions>
                <execution>
                    <phase>package</phase>
                    <goals>
                        <goal>shade</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
```


