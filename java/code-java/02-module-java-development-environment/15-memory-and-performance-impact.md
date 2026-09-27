## 15. Memory & Performance Impact

---

#### 15.1. JDK vs JRE in Production
##### Development Environment:
- Requires JDK (need javac, jar, javadoc, etc.).

##### Production Environment:
- Only requires JRE (smaller footprint, no development tools).
- Modern container images (Docker) often use JRE-only images to reduce size.

##### Performance Impact:
- **JDK size:** ~300-400 MB
- **JRE size:** ~150-200 MB
- Using JRE in production reduces deployment size and attack surface.

---

#### 15.2. JVM Startup Time
##### Cold Start:
- First run loads classes, initializes JVM (~100-500 ms for small apps).

##### Warm Start:
- Subsequent runs benefit from JIT-compiled code and OS-level caching.

##### Java 21+ Improvements:
- **Project Leyden:** Aims to reduce startup time and memory footprint.
- **CDS (Class Data Sharing):** Preloads common classes to reduce startup time.

---

#### 15.3. Bytecode Verification Overhead
##### At Class Loading:
- JVM verifies bytecode for security (prevents malicious code).
- Adds slight overhead (~10-20 ms per class).
- Essential for security; cannot be disabled.

---

#### 15.4. Environment Variable Impact
##### CLASSPATH Issues:
- Overly long CLASSPATH increases class-loading time.
- Missing CLASSPATH entries cause ClassNotFoundException.

**Best Practice:** Use build tools (Maven, Gradle) to manage dependencies instead of manual CLASSPATH management.