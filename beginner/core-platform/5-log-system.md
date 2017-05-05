## Log System

- Java built-in solution: `java.util.logging`
- one global app-wide log manager. You can access it statically `LogManager.getLogManager`
- Logging levels:
  - off: logger capture nothing (Integer.MAX_VALUE)
  - severe: serious failiure (1000)
  - warning: potential problem (900)
  - info: general info (800)
  - config: config info (700)
  - fine: general developer info (500)
  - finer: detailed developer info (400)
  - finest: specialized developer info (300)
  - all: logger will capture everything (Integer.MIN_VALUE)
- sometimes the inferred class name and method name are not correct
  - use `logger.logp(Level.SEVERE, "com.bla.ClassName", "methodName", "Message");`
- the following logger messages will only print if level is FINER
  - `logger.entering("com.blah.ClassName", "methodName")`
  - `logger.exiting("com.blah.ClassName", "methodName")`

```java
public class Main {
    static Logger logger = LogManager.getLogManager().getLogger(Logger.GLOBAL_LOGGER_NAME);
    public static void main()_{
        // logger will display only INFO, WARNING, and SEVERE levels
        logger.setLevel(Level.INFO);

        // these are both the same
        logger.log(Level.SEVERE, "severe problem");
        looger.severe("another severe problem")
    }
}
```

- you can parametetize logging message and method parameters

```java
void doWork(String left, String right) {
    logger.entering("com.blah.ClassName", "doWork", new Object[] { left, right });
    logger.info("{0} is hello and {1} is bye", new Object[] { left, right });
    logger.info("{0} is the only value", left);
    String result = left + right;
    logger.entering("com.blah.ClassName", "doWork", result);
}
```

- you can create your own logger and specify its handler (write to file, console, etc) + formatter
- FileHandler can rotate and reuse a set of log files

```java
public class Main {
    static Logger logger = Logger.getLogger("com.mypackage");
    public static void main (String[] args) {
        // rotate set of 4 log files
        // move to next log after 1000 bytes
        // create files in user HOME /home/username/myapp_x.log
        FileHandler h = new FileHandler("%h/myapp_%g.log", 1000, 4);
        h.setLevel(Level.ALL);
        h.setFormatter(new SimpleFormatter());
        logger.addHandler(h);
        logger.setLevel(Level.ALL);
        logger.log(Level.INFO, "logging");
    }
}
```

- you can also create your own formatter or configure SimpleFormatter
- to configure SimpleFormatter, pass system property: `java.util.logging.SimpleFormatter.format`\
  - `java -Djava.util.logging.SimpleFormatter.format=%5$s,%2$s,%4$s%n com.blah.Main`

- Logger config file

```bash
# log.properties
java.util.logging.ConsoleHandler.level = ALL
java.util.loggin.COnsoleHandler.formatter = java.util.logging.SimpleFormatter
com.mypackage.handlers = java.util.logging.ConsoleHandler
com.mypackage.level = ALL
java.util.logging.SimpleFormatter.format = %5$s,%2$s,%4$s%n
```

- start program with `java -Djava.util.logging.config.file=log.properties com.blah.Main`

- use the logger

```java
public class Main {
    static Logger logger = Logger.getLogger("com.mypackage");
    public staic void main (String[] args) {
        logger.info("my info)");
    }
}
```
