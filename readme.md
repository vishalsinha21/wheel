maven release to nexus

- start nexus

```
~/Documents/nexus-3.15.2-01-mac/nexus-3.15.2-01/bin:➔ ./nexus start
Starting nexus
```

- create new repository (hosted) `releases` on nexus and copy repository url, it should be something like `http://localhost:8081/repository/releases` 

- add distribution management section in project pom, give some id and add `releases` repository url

```
  <distributionManagement>
    <repository>
      <id>my.releases</id>
      <url>http://localhost:8081/repository/releases/</url>
    </repository>
  </distributionManagement>
```

- add server configuration in maven settings.xml. Take care that id in distribution management and server section is same

```
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0
                              http://maven.apache.org/xsd/settings-1.0.0.xsd">

  <servers>
    <server>
      <id>my.releases</id>
      <username>admin</username>
      <password>admin123</password>
      <configuration></configuration>
    </server>
  </servers>

</settings>
```  

- Instead of using nexus admin user, you could also create your own user with appropriate rights to upload to repository