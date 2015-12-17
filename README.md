# Play2 Maven Plugin on Heroku

This is an example of how to use the Play2 Maven Plugin with a Heorku app

[![Deploy to Heroku](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy)

## Usage

The main modification was to and a binding of the `play2:dist-exploded` goal
to the `install` phase (so that Heroku will run it). This has been added to the `pom.xml`:

```xml
<plugin>
  <groupId>com.google.code.play2-maven-plugin</groupId>
  <artifactId>play2-maven-plugin</artifactId>
  <version>${play2.plugin.version}</version>
  <extensions>true</extensions>
  <configuration>
    <mainLang>java</mainLang>
    <routesGenerator>injected</routesGenerator>
  </configuration>
  <executions>
    <execution>
      <phase>install</phase>
      <goals>
        <goal>dist-exploded</goal>
      </goals>
    </execution>
  </executions>
</plugin>
```

A `Procfile` as also been added:

```
web: sh target/dist/play-java-*/start -Dhttp.port=$PORT
```