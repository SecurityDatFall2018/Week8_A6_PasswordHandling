## Exercises

Create a project i your favourite language, and set it for use with BCrypt.

In Java with maven you will need the following dependency in your `pom.xml` file:
```xml
<dependency>
    <groupId>org.mindrot</groupId>
    <artifactId>jbcrypt</artifactId>
    <version>0.4</version>
</dependency>
```
and
```java
import org.mindrot.jbcrypt.BCrypt;
```

A C\# project can be setup with:
```
> dotnet new console -o Hashing.net
> cd Hashing.net
> dotnet add package BCrypt-Official --version 0.1.109
```
and

```csharp
using System;
using static BCrypt.Net.BCrypt;
```

### Getting started

Create a class `MCrypt` that uses the `SHA-256` hashing algorithm instead of `BCrypt`'s blowfish algorithm.

The signature (for Java) should be:
```java
public class MCrypt {
  public static String hashpw(String password, String salt) {...}
  public static boolean checkpw(String candidate, String hash) {...}
  }
```
or in C\#:
```csharp
public class MCrypt {
  public static string HashPassword(string password, string salt) {...}
  public static bool Verify(string candidate, string hash) {...}
  }
```

Output should be Base64 encoded, remember to embed the salt in the result of `hashpw` and to extract it in `checkpw`

Test the class with different passwords.

If you have time, you can implement a `gensalt()` (C\#: `GenerateSalt()`) method as well, that generates random salts. A fixed salt strategy will do ok for the exercise though.

### Using `BCrypt`

Create a method (good idea to make it static, so it can be called from `main`) that hashes the password `1q2w3e4r` with increasing rounds specified in the salt, start with 10.
For each round value measure the time it takes.

Hint: you can use the `System.nanoTime()`

### Brute force using `MCrypt`

Place the [`candidates.txt`](candidates.txt) file in the `src/main/resources` folder in your project.

Create a program that parses the [`passwd-raw`](passwd-raw) file and writes a new file
`passwd-mcrypt` to `src/main/resources`, where all passwords has been hashed by BCrypt.

Make a brute force attack on the new file using the `candidates.txt` and trying all passwords, which are the username followed by exactly three digits.

Measure the time.

### Brute force using `BCrypt`

Create another program that parses the [`passwd-raw`](passwd-raw) file and writes a new file
`passwd-bcrypt-10` to `src/main/resources`, where all passwords has been hashed by BCrypt with `10` rounds.

Make a brute force attack on the new file using the `candidates.txt` and trying all passwords, which are the username followed by exactly three digits.

Measure the time.

What would the time be if `13` rounds had been used instead?

### Reading text files in the `resources` folder

Here is a small program you can use to access text files in the `src/main/resources` folder:

```java
import java.io.BufferedReader;
import java.io.File;
import java.io.FileNotFoundException;
import java.io.FileReader;
import java.util.ArrayList;
import java.util.List;

public class TextFile {
  private List<String> lines = new ArrayList<>();

  public TextFile(String name) throws FileNotFoundException {
    ClassLoader cl = getClass().getClassLoader();
    BufferedReader in = new BufferedReader(
        new FileReader(new File(cl.getResource(name).getFile()))
        );
    in.lines().forEach(line -> lines.add(line));
    }

  public List<String> getLines() { return lines; }

  }
```

You can also find it at:
[Week-8-Passwords](https://github.com/SecurityDatFall2018/Week-8-Passwords/tree/master/Hashing.vm)
