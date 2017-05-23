# Serialization

- persists objects (with state) by storing from runtime into a byte stream
- restores objects (with state) from byte stream into runtime
- operates on instance members (but you can customize it to serialize statics)
- you can save state of your objects into file system/ database (RDBMS = blobl, OODBMS)
  - you can send objects are well
- objects that your object uses are also saved, createing an object-graph
- `serializable` is a marker interface. it has no methods
- `ObjectOutputStream` => serializes an object-graph into steam
- `ObjectInputStream` => deserializes stream to object-graph
- in order to implement `serializable`, all member types need to `implement serializable` as well
- ex:

```java
// in order for BankAccount to be serializable, all member types need to implement it too
public class BankAccount implements serializable {
    // String class is serializable itself, so you're good
    private final String id;
    // primitives are serializable already
    private int balance = 0;

    public BankAccount(id, balance);
    // ...
}
```

- to serialize:

```java
// create an obj
BankAccount acct = new BankAccount("1234", 500);
acct.deposit(250);
saveAccount(acct, "account.dat");

// helper function
void saveAccount(BankAccount ba, String filename) {
    // try with resources
    try (ObjectOutputStream objectStream =
        new ObjectOutputStream(Files.newOutputStream(Paths.get(filename)))) {
        objectStream.writeObject(ba);
    } catch(IOException e) {
        // so something
    }
}
```

- to deserialize:

```java
// load a bank account from a file
BankAccount acct = loadAccount("account.dat");

// helper to deserialize the account
BankAccount loadAccount(String filename) {
    BankAccount ba = null;

    // try with resources
    try (ObjectInputStream objectStream =
        new ObjectInputStream(Files.newInputStream(Paths.get(filename)))) {
        ba = (BankAccount) objectStream.readObject();
    } catch(IOException e) {
        // do something
    } catch (ClassNotFoundException e) {
        // if class not in classpath, then this will be caught
    }
    return ba;
}
```

## Serial Verion Unique Identifier

- java takes a hash (serial version) of the class when serializing
- when deserializing, it will compare the hash of the class we want to deserialize from the stream vs the runtime
- you get `InvalidClassException` if they don't match
- any changes in the class name, members, etc will cause a missmatch
- to fix it, as a dev, you have to manage this serial UID
- to specify a serial UID:
  - add `serialVersionUID` field
    - long/ static final/ private
    - the value can be obtained using `serialver` utility (in JDK bin)
      - lot of plugins provide this already
      - to obtain UID with serialVer: `serialver com.my.package.BankAccount`
      - you can also do: `serialver -show` to open a GUI
- use the same serial UID for future versions of your class
- deserialization is smart. It handles cases where you removed/ added fields

## Customizing Serialization

- you can add `writeObject` and `readObject` methods to the class you want to serialize and deserialize to manage how they behave
- ex:

```java
public class BankAccount implements Serializable {
    // members and methods
    private void writeObject(OBjectOutputStream out) throws IOException {
        // behave as default
        out.defaultWriteObject();
        // has other methods, like writeInt()
        // they are positional though, so first thing you write has to be first thing you read
    }
    private void readObject(ObjectInputStream in) throws IOException, ClassNotFoundException {
        // readInt() is positional, so instead, read all the fields
        ObjectInputStream.GetField fields = in.readFields();
        // note that you can provide default values to account for incompatible types
        id = (String) fields.get("id", null);
        balance = fields.get("balance", 0);
        lastTxtType = fields.get("lastTxtType", 'u');
        lastTxtAmount = fields.get("lastTxAmount", -1);
    }
}
```

## Transient Fields

- if you use transient on a field, it will not be serialized
- useful when saving space and dealing with fields that can be determined by other ones

```java
public class AccountGroup implementd Serializable {
    private Map<String, BankAccount> accountMap = new HashMap();
    // totalBalance will not be serialized because we can determine its value
    private transient int totalBalance;
    public int getTotalBalance() {
        return totalBalance;
    }
    public void addAccount(BankAccount account) {
        totalBalance += account.getBalance();
        accountMap.put(account.getId(), account);
    }

    // customize deserializing
    void readObject(ObjectInputStream in) throws IOException, ClassNotFooundException {
        // perform the regular deserialization
        in.defaultReadObject();
        // determine the value of totalBalance
        for(BankAccount account : accountMap.values()) {
            totalBalance += account.getBalance();
        }
    }
}
```
