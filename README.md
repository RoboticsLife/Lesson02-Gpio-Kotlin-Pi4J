### Kotlin Gpio project. Working with IO lines on Raspberry Pi using Pi4J Kotlin/Java langs and remote compiling / debugging to any ARM GPIO compatible hardware. Advanced AI features (TensorFlow)


[All tutorails and videos on my YouTube channel](https://www.youtube.com/@OleksandrNeiko)



## Lesson 02: Useful tips, Git, AI Assistant


#### Step 1: maven pom.xml settings

###### Properties section

 <properties>
        <main.class>org.example.runtime.MainKt</main.class>   <!-- Lesson01 :: add to pom.xml -->
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <kotlin.code.style>official</kotlin.code.style>
        <kotlin.compiler.jvmTarget>1.8</kotlin.compiler.jvmTarget>

        <!-- DEPENDENCIES VERSIONS --> <!-- Add this to pom.xml -->
        <slf4j.version>2.0.12</slf4j.version>
        <pi4j.version>2.6.1</pi4j.version>

        <!-- BUILD PLUGIN VERSIONS --> <!-- Add this to pom.xml -->
        <maven-compiler-plugin.version>3.8.1</maven-compiler-plugin.version>
        <maven-jar-plugin.version>3.1.0</maven-jar-plugin.version>
        <maven-shade-plugin.version>3.2.4</maven-shade-plugin.version>
    </properties>



###### Plugins section

  <!-- Add those Plugins to pom.xml -->

            <!--
            https://maven.apache.org/plugins/maven-compiler-plugin/
            The Compiler Plugin is used to compile the sources of your project.
            -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>${maven-compiler-plugin.version}</version>
                <configuration>
                    <release>${java.version}</release>
                    <showDeprecation>true</showDeprecation>
                    <showWarnings>true</showWarnings>
                    <verbose>false</verbose>
                </configuration>
            </plugin>

            <!--
            https://maven.apache.org/plugins/maven-jar-plugin/
            This plugin provides the capability to build (executable) jars and is used here to set the mainClass
            which will start the application.
            -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-jar-plugin</artifactId>
                <version>${maven-jar-plugin.version}</version>
                <configuration>
                    <archive>
                        <manifest>
                            <mainClass>${main.class}</mainClass>
                        </manifest>
                    </archive>
                </configuration>
            </plugin>

            <!--
            https://maven.apache.org/plugins/maven-shade-plugin/
            This plugin provides the capability to package the artifact in an uber-jar, including its dependencies and
            to shade - i.e. rename - the packages of some of the dependencies. The transformer will combine the files
            in the META-INF.services directories of multiple Pi4J plugins with the same package name into one file.
            -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-shade-plugin</artifactId>
                <version>${maven-shade-plugin.version}</version>
                <configuration>
                    <transformers>
                        <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer"/>
                    </transformers>
                </configuration>
                <executions>
                    <execution>
                        <phase>package</phase>
                        <goals>
                            <goal>shade</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>


###### Dependencies section

    <!-- Add those Dependencies to pom.xml -->

        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-api</artifactId>
            <version>${slf4j.version}</version>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-simple</artifactId>
            <version>${slf4j.version}</version>
        </dependency>

        <!-- include Pi4J Core -->
        <dependency>
            <groupId>com.pi4j</groupId>
            <artifactId>pi4j-core</artifactId>
            <version>${pi4j.version}</version>
        </dependency>

        <!-- include Pi4J Plugins (Platforms and I/O Providers) -->
        <dependency>
            <groupId>com.pi4j</groupId>
            <artifactId>pi4j-plugin-raspberrypi</artifactId>
            <version>${pi4j.version}</version>
        </dependency>
        <dependency>
            <groupId>com.pi4j</groupId>
            <artifactId>pi4j-plugin-gpiod</artifactId>
            <version>${pi4j.version}</version>
        </dependency>

        <dependency>
            <groupId>org.jetbrains.kotlinx</groupId>
            <artifactId>kotlinx-coroutines-core</artifactId>
            <version>1.10.1</version>
        </dependency>


#### Step 2: remote compiling / debugging setup


Add new launch configuration to IntelliJ IDEA

![screenshot](readme/readme01.png)


fill IP / port adress to Raspberry PI. Username & password as sudo connection. Add Main Kotlin class and project module.

![screenshot](readme/readme02.png)
