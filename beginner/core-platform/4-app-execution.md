# App Execution

## Persisting Properties

- why?
  - store app config
  - track state of app
  - track user preferences

- Solution: use `java.util.Properties`
  - inherits from HashTable
  - key/values = strings
  - setProperty -> sets key = value or creates the entry if doesn't exist
  - getProperty -> get value (null if not found) - you can also pass default if DNE
  - you can read/ write to a stream
  - supports as text or xml
    - text: \*.properties
      - "key=value" or "key  = value " or "key: value" or "key value"
      - can escape whitespace, = , or : with \
      - comments with # or !

```java
// store properties in file
Properties props = new Properties();
props.setProperty("key", "value");

try(Writer writer = Files.newBufferedWriter(Paths.get("xyz.properties"))) {
    // optional top of the file comment
    // by default, time and date added to file
    props.store(writer, "My comment");
}
```

```java
// load properties from file
Properites props = new Properties();
try(Reader reader = Files.newBufferedReader(Paths.get("xyz.properties"))) {
    props.load(reader);
}
props.getProperty("key"); //returns value
```

```java
// loads MyDetaultValues.xml on first run, modifies props, and stores them for future runs
public void static main() {
    try {
        Properties defaultProps = new Properties();
        try(InputStream inputStream - Main.class.getResourceAsStream("MyDefaultValues.xml")) {
            defaultProps.loadFromXML(inputStream);
        }
        // load default properties as default
        Properties userProps = new Properties(defaultProps);
        loadUserProps(userProps);

        if(userProps.getProperty("isFirstRun").equalsIgnoreCase("Y")) {
            userProps.setProperty("isFirstRun", "N");
            saveUserProps(userProps);
        }
    }
    catch (IOException e){
        System.out.println(e.getClass().getSimpleName() + ">" + e.getMesage());
    }
}

private static Properties loadUserProps(Properties userProps) throws IOException {
    Path userFile = Paths.get("userValues.xml");
    if (Files.exists(userFile)) {_
        try(InputStream inputStream = Files.newInputStream(userFile)) {
            userProps.loadFromXML(inputStream);
        }
    }
    return userProps;
}

private static void saveUserProps(Properties userProps) throws IOException {
    try(OutputStream outputStream = Files.newOutputStream(Paths.get("userValues.xml"))) {
        userProps.storeToXML(outputStream, null);
    }
}
```

## Setting Classpath

- 2 ways: environment variable or pass it at runtime
  - environment variable not a very good option `CLASSPATH`
  - at runtime:
    - if everything is .class: `java -cp /psdir:/libdir com.pluralsight.training.Main`
    - if jar is added: `java -cp /psfit/training.jar:/libdir com.pluralsight.training.Main`
    - if jar's manifest is in charge and it's all included there: `java -jar app.jar`

## Execution Environment Information

- System Properties:
  - you can access user info/ java installation info/ OS config info
  - access with `System.getProperty("somekey");`
- Environment Variables:
  - info about the OS and env vars that user sets for the app to use
  - access with `System.getenv()`
