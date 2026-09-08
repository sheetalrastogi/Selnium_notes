## How to remove jars with multiple versions on the class path?

Having multiple versions of the same JAR on the classpath can cause issues such as:
- NoSuchMethodError
- NoClassDefFoundError
- ClassCastException
- LinkageError
- Unexpected runtime behavior

Example:   
commons-lang3-3.9.jar
commons-lang3-3.14.0.jar

Only one version should exist on the runtime classpath.

## 1. Maven: Identify Duplicate Dependencies

Display the dependency tree:
	mvn dependency:tree

For a specific dependency:
	mvn dependency:tree -Dincludes=org.apache.commons:commons-lang3

Example Output:

```text
project
├── moduleA
│   └── commons-lang3:3.9
└── moduleB
    └── commons-lang3:3.14.0
```

## 2. Maven: Exclude Unwanted Version

```xml
<dependency>
    <groupId>com.example</groupId>
    <artifactId>moduleA</artifactId>

    <exclusions>
        <exclusion>
            <groupId>org.apache.commons</groupId>
            <artifactId>commons-lang3</artifactId>
        </exclusion>
    </exclusions>
</dependency>
```

Then explicitly define the desired version:

```xml
<dependency>
    <groupId>org.apache.commons</groupId>
    <artifactId>commons-lang3</artifactId>
    <version>3.14.0</version>
</dependency>
```


## 3. Detect Dependency Conflicts

	mvn dependency:analyze  or
	mvn dependency:tree -Dverbose
	
- Example output:
	commons-lang3:3.9 (omitted for conflict)
	commons-lang3:3.14.0


## 4. Fail Build on Duplicate Classes

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-enforcer-plugin</artifactId>
    <version>3.6.1</version>

    <executions>
        <execution>
            <id>enforce</id>

            <goals>
                <goal>enforce</goal>
            </goals>

            <configuration>
                <rules>
                    <dependencyConvergence/>
                </rules>
            </configuration>
        </execution>
    </executions>
</plugin>
```

- Build failure example:

Dependency convergence error:
commons-lang3:3.9
commons-lang3:3.14.0

## 5. Runtime Check (Java)

Print where a class is loaded from:

```java
System.out.println(
    org.apache.commons.lang3.StringUtils.class
        .getProtectionDomain()
        .getCodeSource()
        .getLocation()
);
```

Output:
file:/libs/commons-lang3-3.14.0.jar

