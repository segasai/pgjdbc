<img src="http://developer.postgresql.org/~josh/graphics/logos/elephant-64.png" />
# PostgreSQL JDBC driver

This is a simple readme describing how to compile and use the Postgresql JDBC driver.

## Info

This isn't a guide on how to use JDBC - for that refer to [Oracle's website](http://www.oracle.com/technetwork/java/javase/jdbc/) and the [JDBC tutorial](http://docs.oracle.com/javase/tutorial/jdbc/).

For problems with this driver, refer to driver's [home page](http://jdbc.postgresql.org/) and associated [mailing list](http://archives.postgresql.org/pgsql-jdbc/).

## Compiling

To compile you will need to have a Java 5 or newer JDK and will need to have
Ant installed. To obtain Ant go to http://ant.apache.org/index.html and
download the binary. Being pure Java it will run on virtually all Java
platforms. If you have any problems please email the pgsql-jdbc list.

Once you have Ant, simply run ant in the top level directory.  This will
compile the correct driver for your JVM, and build a .jar file (Java ARchive)
called postgresql.jar.

*REMEMBER*: Once you have compiled the driver, it will work on ALL platforms
that support that version of the API. You don't need to build it for each
platform.

If you are having problems, prebuilt versions of the driver 
are available at the [Postgresql JDBC site](http://jdbc.postgresql.org/).

## Installing the driver

To install the driver, the postgresql.jar file has to be in the classpath.

i.e. under LINUX/SOLARIS (the example here is my linux box):

	export CLASSPATH=.:/usr/local/pgsql/share/java/postgresql.jar

## Using the driver

To use the driver, you must introduce it to JDBC. Again, there's two ways
of doing this:

- Hardcoded

   This method hardcodes your driver into your application/applet. You
   introduce the driver using the following snippet of code:

```java
try {
  Class.forName("org.postgresql.Driver");
} catch(Exception e) {
  // your error handling code goes here
}
```

   Remember, this method restricts your code to just the postgresql database.
   However, this is how most people load the driver.

- Parameters

   This method specifies the driver from the command line. When running the
   application, you specify the driver using the option:

    `-Djdbc.drivers=org.postgresql.Driver`

   eg: This is an example of running one of my other projects with the driver:

    `java -Djdbc.drivers=org.postgresql.Driver uk.org.retep.finder.Main`

   note: This method only works with Applications (not for Applets).
	 However, the application is not tied to one driver, so if you needed
	 to switch databases (why I don't know ;-) ), you don't need to
	 recompile the application (as long as you havent hardcoded the url's).

## JDBC URL syntax

The driver recognises JDBC URLs of the form:

    jdbc:postgresql:database

    jdbc:postgresql://host/database

    jdbc:postgresql://host:port/database

Also, you can supply both username and passwords as arguments, by appending
them to the URL. e.g.:

    jdbc:postgresql:database?user=me
    jdbc:postgresql:database?user=me&password=mypass

Notes:

- If you are connecting to localhost or 127.0.0.1 you can leave it out of the
   URL. i.e.: `jdbc:postgresql://localhost/mydb` can be replaced with
   `jdbc:postgresql:mydb`

- The port defaults to 5432 if it's left out.

---

That's the basics related to this driver. You'll need to read the JDBC Docs
on how to use it.

---

## Bug reports, patches and development

PgJDBC development is carried out on the [PgJDBC mailing list](http://jdbc.postgresql.org/lists.html) and on [GitHub](https://github.com/pgjdbc/pgjdbc).

### Bug reports

For bug reports please post on pgsql-jdbc or add a GitHub issue. If you include
additional unit tests demonstrating the issue, or self-contained runnable test
case including SQL scripts etc that shows the problem, your report is likely to
get more attention. Make sure you include appropriate details on your
environment, like your JDK version, container/appserver if any, platform,
PostgreSQL version, etc. Err on the site of excess detail if in doubt.

### Bug fixes and new features

If you've developed a patch you want to propose for inclusion in PgJDBC, feel
free to send a GitHub pull request or post the patch on the PgJDBC mailing
list.  Make sure your patch includes additional unit tests demonstrating and
testing any new features. In the case of bug fixes, where possible include a
new unit test that failed before the fix and passes after it.

For information on working with GitHub, see: http://help.github.com/articles/fork-a-repo and http://learn.github.com/p/intro.html.

### Testing

Remember to test proposed PgJDBC patches when running against older PostgreSQL
versions where possible, not just against the PostgreSQL you use yourself.

You also need to test your changes with older JDKs. PgJDBC must support JDK5
("Java 1.5") and newer, which means you can't use annotations, auto-boxing, for
(:), and numerous other features added since JDK 5. Code that's JDBC4 specific
may use JDK6 features, and code that's JDBC4.1 specific may use JDK7 features.
Common code and JDBC3 code needs to stick to Java 1.5.

Two different versions of PgJDBC can be built, the JDBC 3 and JDBC 4 drivers.
The former may be built with JDK 5, while building JDBC4 requires JDK 6 or 7.
The driver to build is auto-selected based on the JDK version used to run the
build. The best way to test a proposed change with both the JDBC3 and JDBC4
drivers is to build and test with both JDK5 and JDK6 or 7.

You can get old JDK versions from the [Oracle Java Archive](http://www.oracle.com/technetwork/java/archive-139210.html).

Typically you can test against an old JDK with:

    export JAVA_HOME=/path/to/jdk_1_5
    export PATH=$JAVA_HOME/bin:$JAVA_HOME/jre/bin:
    ant clean test

For information about the unit tests and how to run them, see
  [org/postgresql/test/README](org/postgresql/test/README)

### Ideas

If you have ideas or proposed changes, please post on the mailing list.
Think about how the change would affect other users, what side effects it
might have, how practical it is to implement, what implications it would
have for standards compliance and security, etc.

Few of the PgJDBC developers have much spare time, so it's unlikely that your
idea will be picked up and implemented for you. The best way to make sure a
desired feature or improvement happens is to implement it yourself. The PgJDBC
sources are reasonably clear and they're pure Java, so it's sometimes easier
than you might expect.

### Sponsors

[credativ ltd (Canada)](http://www.credativ.ca) and [xTuple](http://www.xtuple.com)
 
