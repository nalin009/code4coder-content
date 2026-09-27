## 5 Installing JDK

---

#### 5.1 Choosing the Right JDK
- **Oracle JDK:** Official Oracle version (requires license for production use in some cases).
- **OpenJDK:** Free, open-source implementation (widely used).
- **Other Distributions:** Amazon Corretto, Azul Zulu, Eclipse Temurin (all OpenJDK-based).
- **Recommendation for Beginners:** Download OpenJDK from https://jdk.java.net/ or Oracle JDK from https://www.oracle.com/java/technologies/downloads/.

---

#### 5.2 Installation Steps (Platform-Independent Overview)
##### Windows:
1. Download the JDK installer (`.exe` file).
2. Run the installer and follow on-screen instructions.
3. JDK typically installs to `C:\Program Files\Java\jdk-<version>`.

##### macOS:
1. Download the JDK `.dmg` file.
2. Open and install.
3. JDK typically installs to `/Library/Java/JavaVirtualMachines/jdk-<version>.jdk`.

##### Linux:
1. Download the JDK `.tar.gz` file.
2. Extract: `tar -xvzf jdk-<version>.tar.gz`
3. Move to `/opt` or `/usr/local` (optional).

---

#### 5.3 Verifying Installation
###### Open terminal/command prompt and run:

```java
java -version
javac -version
```

**Expected Output**:

```java
java version "21.0.1" 2023-10-17 LTS
Java(TM) SE Runtime Environment (build 21.0.1+12-LTS-29)
Java HotSpot(TM) 64-Bit Server VM (build 21.0.1+12-LTS-29, mixed mode, sharing)

javac 21.0.1
```

**If you get "`command not found`" or "`not recognized,`" environment `variables` are not set.**