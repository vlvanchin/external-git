# How to run executable Java Jar files

Here we have a sample1 project that shows how to build and execute java programs as a Jar file.

```
├─ com
   └── vlv
       ├── demosample
           └── GetProps.java

```

Above tree structure show the java source and class objects in their package structure.

Here is the sample code for GetProps.java

```
package com.vlv.demosample;



import java.lang.*;
import java.security.*;

public class GetProps {

	public static void main (String [] args) {
		String s;
		try {
      System.out.println ("-------------------");	
      System.out.println("os.name value");
			s = System.getProperty("os.name", "not given");
			System.out.println("os is " + s);

			System.out.println("about java.version");
			s = System.getProperty("java.version", "not given");
			System.out.println("java version " + s);

			System.out.println("about user home");
			s = System.getProperty("user.home", "not given");
			System.out.println("user home " + s);

			System.out.println("about java home");
			s = System.getProperty("java.home","not given");
			System.out.println("java home " + s);
		} catch (Exception e) {
			System.err.println("caught exception " + e.toString());
		}
	}
}

```

```
$ javac com/vlv/demosample/GetProps.java

```

Run the above command to compile the java code and the structure is like follows:

```
├─ com
   └── vlv
       ├── demosample
           ├── GetProps.class
           └── GetProps.java
  
```

Now create a manifest file that would specify the Main-Class, which will make the jar an executable one.

Please refer the contents of the mainfest.txt file : [manifest.txt](https://github.com/vlvanchin/testbed/blob/master/java/sample1/manifest.txt)

Now create an executable jar file with the below command:

```
$ jar -cvfm showproperties.jar manifest.txt *

```

Here is the command to run the *showproperties.jar* 

```
$ java -jar showproperties.jar

```

[Back to Homepage](../)

