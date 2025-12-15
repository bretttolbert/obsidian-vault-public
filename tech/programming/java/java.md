# java

###### Specificy path to jar files on command line

```bash
java --module-path <path_to_your_jar> --module <module_name>/<main_class>
```

E.g.
```bash
java --module-path target/hello-world.jar -m com.example.app/com.example.app.Main
```

###### show java system properties
```bash
java -XshowSettings:properties
```

###### Set tmpdir system property
```bash
java -Djava.io.tmpdir=/path/to/tmpdir
```
