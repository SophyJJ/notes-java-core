# Packages

- groupings for related types (Classes)
- they create a namespace (to avoid namingt collisions), set boundaries, and act as a distribution unit
- you want package names to be unique, so for github: `com.github.luiscarlin`
- you don't have to import classes if they are located within the same package they are being used
- you don't have to import clases from java.lang
- importing classes and packages is NOT adding referenced code, it's just mapping them.
  - so, if you want to import everything or just 1 class, it's the same wrt size, etc
- two ways to do imports:
  1. single type imports
    - mapping to a single class. ex: `import com.github.luiscarlin.project.rest.ClassName;`
    - this is preferred because you know exactly what simple name class you are using
    - most IDEs will do this for you
  2. import on demand
    - mapping for all types in the package. ex. `import com.github.luiscarlin.project.rest.*;`
    - only problem with this is that your code may break if there is a collision
      - like if the 3rd party package added a new class that colides another one you're using
    - your code could potentially break
- packages can also act as boundaries (package private)
  - no access modifier -> class is package private, members are package private
  - public -> class available everywhere, members available everywhere
  - private -> class not available, member only availble within class
  - protected -> class not availble, memver only availbe if you inherit class
- anything that's meant to be available ONLY in the package should be package private (ie no access modifier)
- you can distribute multiple packages in a jar file
  - collection of packages (`*.class` files) + a manifest file (entry point aka main)
  - the jar file can be created with IDE or from the command line with the Java jar utility
- if the jar file has an entry point (Main class), then you can `java -jar jar-file.jar` to run it
- jar file is just a zip file. If you change the extension to zip, you can open it.
- manifest goes in the META-INF folder
