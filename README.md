## Source
https://www.blog.akhil.cc/static-jni

## Steps I took on OS X Catalina 10.15.6
```
mkdir NativeHelloWorld && cd NativeHelloWorld
vim HelloWorld.java
javac -h . HelloWorld.java
vim Native.c
curl https://repo1.maven.org/maven2/org/graalvm/nativeimage/svm/21.1.0/svm-21.1.0.jar -so svm-21.1.0.jar
jar xvf svm-21.1.0.jar
vim NativeFeature.java
vim manifest.txt
javac -cp . HelloWorld.java NativeFeature.java
sdk install java 21.0.0.2.r8-grl
javac -cp . HelloWorld.java NativeFeature.java
jar cfm HelloWorld.jar manifest.txt HelloWorld.class NativeFeature.class
cc -c -I "$JAVA_HOME/include" -I "$JAVA_HOME/include/darwin" -o native.o Native.c
ar rcs libNative.a native.o
gu install native-image
/Users/spatail/.sdkman/candidates/java/current/bin/native-image -jar HelloWorld.jar -H:CLibraryPath=.
./HelloWorld
```
