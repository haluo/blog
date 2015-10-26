## nexus配置maven私服

工程pom中配置

``` 
<distributionManagement>
        <repository>
            <id>nexus-releases</id>
            <name>Team Nexus Repository</name>
            	  <url>http://mvn.autohome.com.cn/nexus/content/repositories/releases</url>    
        </repository>
        <snapshotRepository>
            <id>nexus-snapshots</id>
            <name>Team Nexus Repository</name>
            <url>http://mvn.autohome.com.cn/nexus/content/repositories/snapshots</url>
        </snapshotRepository>
    </distributionManagement>
```



setting.xml配置

``` 
<settings>
    <localRepository>/Users/zhufeng/.m2/repository</localRepository>
    <servers>
        <server>
            <id>nexus-releases</id>
            <username>mvn</username>
            <password>mvn123</password>
        </server>
        <server>
            <id>nexus-snapshots</id>
            <username>mvn</username>
            <password>mvn123</password>
        </server>
    </servers>
    <mirrors>
        <mirror>
            <id>nexus-releases</id>
            <mirrorOf>*</mirrorOf>
            <url>http://mvn.autohome.com.cn/nexus/content/groups/public</url>
        </mirror>
        <mirror>
            <id>nexus-snapshots</id>
            <mirrorOf>*</mirrorOf>
            <url>http://mvn.autohome.com.cn/nexus/content/groups/public</url>
        </mirror>
    </mirrors>

    <profiles>
        <profile>
            <id>artifactory</id>
            <repositories>
                <repository>
                    <id>nexus-releases</id>
                    <url>http://nexus-releases</url>
                    <releases>
                        <enabled>true</enabled>
                    </releases>
                    <snapshots>
                        <enabled>true</enabled>
                    </snapshots>
                </repository>
                <repository>
                    <id>nexus-snapshots</id>
                    <url>http://nexus-snapshots</url>
                    <releases>
                        <enabled>true</enabled>
                    </releases>
                    <snapshots>
                        <enabled>true</enabled>
                    </snapshots>
                </repository>
            </repositories>
            <pluginRepositories>
                <pluginRepository>
                    <id>nexus-releases</id>
                    <url>http://nexus-releases</url>
                    <releases>
                        <enabled>true</enabled>
                    </releases>
                    <snapshots>
                        <enabled>true</enabled>
                    </snapshots>
                </pluginRepository>
                <pluginRepository>
                    <id>nexus-snapshots</id>
                    <url>http://nexus-snapshots</url>
                    <releases>
                        <enabled>true</enabled>
                    </releases>
                    <snapshots>
                        <enabled>true</enabled>
                    </snapshots>
                </pluginRepository>
            </pluginRepositories>
        </profile>

    </profiles>
    <activeProfiles>
        <activeProfile>artifactory</activeProfile>
    </activeProfiles>
    
</settings>

```



配置host

​	192.168.252.41 mvn.autohome.com.cn

​	

