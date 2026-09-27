## 6 Setting Environment Variables
Environment variables tell the operating system where to find Java executables.

---

#### 6.1. Key Environment Variables

###### **JAVA_HOME**
**Purpose:** Points to the JDK installation directory.
**Why Needed:** Many tools (Maven, Gradle, IDEs) use `JAVA_HOME` to locate Java.
**Example:**
- **Windows:** `C:\Program Files\Java\jdk-21`
- macOS/Linux: `/Library/Java/JavaVirtualMachines/jdk-21.jdk/Contents/Home`

###### **PATH**
**Purpose:** Tells the OS where to find executable commands (like java and javac).
**Why Needed:** Without `PATH`, you must specify the full path to run Java commands.
**Example:**
- Add `%JAVA_HOME%\bin` (Windows) or `$JAVA_HOME/bin` (macOS/Linux) to PATH.

###### **CLASSPATH**
**Purpose:** Tells the JVM where to find user-defined `classes` and `libraries`.
**Why Needed:** For complex projects with external libraries.
**Default Behavior:** If not set, JVM searches the current directory (.) by default.

---

#### 6.2. Setting Environment Variables (Step-by-Step)

###### **Windows:**
1. Right-click "`This PC`" → `Properties` → `Advanced System Settings` → `Environment Variables`.
2. Under "`System Variables`," click "`New`":
    - Variable Name: `JAVA_HOME`
    - Variable Value: `C:\Program Files\Java\jdk-21`
3. Find Path variable → Edit → New → Add %JAVA_HOME%\bin
4. Click OK. Restart terminal.

###### **macOS/Linux:**
Edit `~/.bash_profile`, `~/.zshrc`, or `~/.bashrc`:

```java
export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk-21.jdk/Contents/Home
export PATH=$JAVA_HOME/bin:$PATH
```

**Save and run:** `source ~/.bash_profile` (or restart terminal).

---

#### 6.3. Verification

```java
echo $JAVA_HOME   # macOS/Linux
echo %JAVA_HOME%  # Windows

java -version
javac -version
```

**Common Mistake:** Setting `JAVA_HOME` to bin directory instead of JDK root. `JAVA_HOME` should point to the JDK directory, NOT jdk/bin.