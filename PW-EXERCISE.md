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
> dotnet new console -o myBCryptProject
> cd myBCryptProject
> dotnet add package BCrypt-Official --version 0.1.109
```
and

```csharp
using System;
using static BCrypt.Net.BCrypt;
```

### Getting started

Create a class `MCrypt` that uses the `MDA-256` hashing algorithm instead of `BCrypt`'s blowfish algorithm.

The signature (for Java) should be:
```java
public class MCrypt {
    public static String hashpw(String password, String salt) {...}
    public static boolean checkpw(String candidate, String hash) {...}
    }
```
Output should be Base64 encoded, remember to embed the salt in the result of `hashpw` and to extract it in `checkpw`

Test the class with different passwords.

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
