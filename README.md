rserve-maven-plugin
===================

Maven plugin for Rserve lifecycle

Supports rserve:start rserve:stop and rserve:run mojos. Start will 
start Rserve and exit with minimal output to maven console, stop
will stop and exit, run will block and dump debug information to
standard out.

Basic usage:
```
<project>
  <build>
    <plugins>
      <plugin>
        <groupId>edu.dfci.cccb</groupId>
        <artifactId>rserve-maven-plugin</artifactId>
        <version>0.0.4</version>
        <configuration>
          <setup>

            <!-- Key/value pair correspond to entries in Rserv.conf -->
            <port>6311</port>
          </setup>

          <!-- Actual R code to run in the plugin process before the server,
               is started, this is good for package installation -->
          <onInitialize>print(paste("Hello","${basedir}"))</onInitialize>

          <!-- Actual R code to run in the request process -->
          <onRequest>print(paste("Hi","$basedir"))</onRequest>
        </configuration>
      </plugin>
    </plugins>
  </build>
  <pluginRepositories>
    <pluginRepository>
      <id>cccb</id>
      <name>CCCB Maven Repository</name>
      <url>https://raw.github.com/dfci-cccb/maven-repo/master/releases/</url>
    </pluginRepository>
  </pluginRepositories>
</project>