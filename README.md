# IXD Labs Maven Packages Repository
This repository is used for hosting dependencies of IXD Labs projects.
## Usage
### 1. Clone the repository into a local folder
```bash
git clone <ixdlabs-maven-packages-url>
```
### 2. Configure the dependency project to be deployed into the local repository folder
In order to do this, the following snippet should be in the dependency project's `pom.xml` file.
```xml
<distributionManagement>
  <repository>
    <id>internal.repo</id>
    <name>Github Repo</name>
    <url>file:///path/to/ixdlabs-maven-packages</url>
  </repository>
</distributionManagement>

<plugins>
  <plugin>
    <artifactId>maven-deploy-plugin</artifactId>
    <version>2.8.1</version>
    <configuration>
      <altDeploymentRepository>internal.repo::default::file:///path/to/ixdlabs-maven-packages</altDeploymentRepository>
    </configuration>
  </plugin>
</plugins>
```
If there already is a `<distributionManagement>` tag in the `pom.xml` file, it might have to be commented out for a moment.
### 4. Build and deploy the dependency project
```bash
mvn clean deploy
```
### 5. Commit and push the changes to the repository
```bash
git add .
git commit -m "Add org.openapitools.onesignal-java-client"
git push
```
### 6. Refer to this repository from the other projects
To use the dependencies hosted on this repository in the other projects, include it as a repository in the required project's `pom.xml`.
```xml
<repositories>
  <repository>
    <id>ixdlabs-github</id>
    <name>GitHub IXD Labs Apache Maven Packages</name>
    <url>https://raw.githubusercontent.com/ixdlabs/ixdlabs-maven-packages/master/</url>
    <releases>
      <enabled>true</enabled>
      <updatePolicy>daily</updatePolicy>
    </releases>
    <snapshots>
      <enabled>true</enabled>
      <updatePolicy>always</updatePolicy>
    </snapshots>
  </repository>
</repositories>
```
