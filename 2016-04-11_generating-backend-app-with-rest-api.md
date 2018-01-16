# Getting started with Java EE - Generating Backend App with REST API

In this example we will be creating backend app REST API app for storing data about books in Java EE platform using JBoss Forge code generator without any manual coding.

[github.com/krzysbaranski/javaee-example](https://github.com/krzysbaranski/javaee-example)

# 1. Start JBoss Forge

In command line run forge from JBoss Forge - it's easy to use code generator for JBoss and Wildfly platform and other Java EE Application Servers.

```bash
$ forge
```

    Using Forge at /opt/jbossforge/forge-distribution
     _____
    |  ___|__  _ __ __ _  ___
    | |_ / _ \| `__/ _` |/ _ \  \\
    |  _| (_) | | | (_| |  __/  //
    |_|  \___/|_|  \__, |\___|
                   |__/
    JBoss Forge, version [ 3.0.1.Final ] - JBoss, by Red Hat, Inc. [ http://forge.jboss.org ]


# 2. Creating app in JBoss Forge

Creating new app in JBoss Forge is simple as running "project-new" inside JBoss Forge application and answering few simple questions.

```
[project]$ project-new
```

    ***INFO*** Required inputs not satisfied, entering interactive mode
    * Project name:  awesomeapp
    ? Top level package [org.awesomeapp]:  com.mycompany.awesomeapp
    ? Version [1.0.0-SNAPSHOT]:
    ? Final name:  AwesomeApp
    ? Project location [/tmp/project]:

    [0] (x) war
    [1] ( ) jar
    [2] ( ) parent
    [3] ( ) forge-addon
    [4] ( ) resource-jar
    [5] ( ) ear
    [6] ( ) from-archetype
    [7] ( ) generic

    Press to confirm, or +C to cancel.
    * Project type: [0-7]

    [0] (x) Maven

    Press to confirm, or +C to cancel.
    * Build system: [0]

    [0] (x) JAVA_EE_7
    [1] ( ) JAVA_EE_6
    [2] ( ) NONE

    Press to confirm, or +C to cancel.
    ? Stack (The technology\ stack to be used in this project): [0-2] 0
    ***SUCCESS*** Project named 'awesomeapp' has been created.
    ***SUCCESS*** Stack 'Java EE 7' installed in project

JBoss Forge will create pom.xml file and folder structure for our app that looks like this:


    .
    ├── pom.xml
    └── src
        ├── main
        │   ├── java
        │   │   └── com
        │   │       └── mycompany
        │   │           └── awesomeapp
        │   ├── resources
        │   └── webapp
        └── test
            ├── java
            └── resources

    11 directories, 1 file


# 3. Adding database support (persistence - JPA)
```
[awesomeapp jbossforge]$ jpa-setup
```

    ***SUCCESS*** Persistence (JPA) is installed.

# 4. Generating classes representing tables (JPA Entities)

To store information about authors we will be creating table author in database.

First we will generate java class Author representing table author in java code.

```
  [awesomeapp]$ jpa-new-entity
```

    ***INFO*** Required inputs not satisfied, entering interactive mode
    ? Package Name (The package name where this type will be created [com.mycompany.awesomeapp.model]:
    * Type Name (The type name):  Author

    [0] ( ) TABLE
    [1] ( ) SEQUENCE
    [2] (x) IDENTITY
    [3] ( ) AUTO

    Press to confirm, or +C to cancel.
    ? ID Column Generation Strategy: [0-3] 2
    ? Table Name:  author
    ***SUCCESS*** JPA Entity com.mycompany.awesomeapp.model.Author was created

# 5. Adding fields to author table

Next step will be to add fields to generated in previous step Author class which will store name and surname of author.

```
[Author.java]$ jpa-new-field
```

    ***INFO*** Required inputs not satisfied, entering interactive mode

    [0] (x) com.mycompany.awesomeapp.model.Author

    Press to confirm, or +C to cancel.
    * Target Entity (The targetEntity which the field will be created): [0]
    * Field Name (The field name to be created in the target targetEntity): name
    * Field Type (The type intended to be used for this field) [String]:
    ? Column Name (The column name. Defaults to the field name):
    ? Length (The column length. (Applies only if a string-valued column is used.)) [255]:
    ? Not Nullable [y/N]:
    ? Not Insertable [y/N]:
    ? Not Updatable [y/N]:
    ? Is LOB? (If the relationship is a LOB, in this case, it will ignore the value in the Type field) [y/N]:
    ? Is Transient? (Creates a field with @Transient) [y/N]:
    ***SUCCESS*** Field name created

```
[Author.java]$ jpa-new-field
```

    ***INFO*** Required inputs not satisfied, entering interactive mode

    [0] (x) com.mycompany.awesomeapp.model.Author

    Press to confirm, or +C to cancel.
    * Target Entity (The targetEntity which the field will be created): [0]
    * Field Name (The field name to be created in the target targetEntity): surname
    * Field Type (The type intended to be used for this field) [String]:
    ? Column Name (The column name. Defaults to the field name):
    ? Length (The column length. (Applies only if a string-valued column is used.)) [255]:
    ? Not Nullable [y/N]:
    ? Not Insertable [y/N]:
    ? Not Updatable [y/N]:
    ? Is LOB? (If the relationship is a LOB, in this case, it will ignore the value in the Type field) [y/N]:
    ? Is Transient? (Creates a field with @Transient) [y/N]:
    ***SUCCESS*** Field surname created


# 6. Add book table

To store information about books we will be creating table book in database.

In JBossForge:
```
[Author.java]$ jpa-new-entity
```

    ***INFO*** Required inputs not satisfied, entering interactive mode
    ? Package Name (The package name where this type will be created [com.mycompany.awesomeapp.model]:
    * Type Name (The type name):  Book

    [0] ( ) TABLE
    [1] ( ) SEQUENCE
    [2] (x) IDENTITY
    [3] ( ) AUTO

    Press to confirm, or +C to cancel.
    ? ID Column Generation Strategy: [0-3] 2
    ? Table Name:  book
    ***SUCCESS*** JPA Entity com.mycompany.awesomeapp.model.Book was created

7. Add fields to book table

To store information about books we will add title and year to table book

In JBossForge:
```
[Book.java]$ jpa-new-field
```

    ***INFO*** Required inputs not satisfied, entering interactive mode

    [0] ( ) com.mycompany.awesomeapp.model.Author
    [1] (x) com.mycompany.awesomeapp.model.Book

    Press to confirm, or +C to cancel.
    * Target Entity (The targetEntity which the field will be created): [0-1]
    * Field Name (The field name to be created in the target targetEntity):   title
    * Field Type (The type intended to be used for this field) [String]:
    ? Column Name (The column name. Defaults to the field name):
    ? Length (The column length. (Applies only if a string-valued column is used.)) [255]:
    ? Not Nullable [y/N]:
    ? Not Insertable [y/N]:
    ? Not Updatable [y/N]:
    ? Is LOB? (If the relationship is a LOB, in this case, it will ignore the value in the Type field) [y/N]:
    ? Is Transient? (Creates a field with @Transient) [y/N]:
    ***SUCCESS*** Field title created

```
[Book.java]$ jpa-new-field
```

    ***INFO*** Required inputs not satisfied, entering interactive mode

    [0] ( ) com.mycompany.awesomeapp.model.Author
    [1] (x) com.mycompany.awesomeapp.model.Book

    Press to confirm, or +C to cancel.
    * Target Entity (The targetEntity which the field will be created): [0-1]
    * Field Name (The field name to be created in the target targetEntity): year
    * Field Type (The type intended to be used for this field) [String]:  Integer
    ? Column Name (The column name. Defaults to the field name):
    ? Length (The column length. (Applies only if a string-valued column is used.)) [255]:
    ? Not Nullable [y/N]:
    ? Not Insertable [y/N]:
    ? Not Updatable [y/N]:

    [0] (x) Basic
    [1] ( ) Embedded
    [2] ( ) One-to-One
    [3] ( ) One-to-Many
    [4] ( ) Many-to-One
    [5] ( ) Many-to-Many

    Press to confirm, or +C to cancel.
    ? Relationship Type (The relationship type): [0-5]
    ? Is LOB? (If the relationship is a LOB, in this case, it will ignore the value in the Type field) [y/N]:
    ? Is Transient? (Creates a field with @Transient) [y/N]:
    ***SUCCESS*** Field year created


8. Add author to book

To add information about author to book we need to add relationship. In this case we will be want to allow multiple authors to one book, to cover the case when there is more than one author of particular book. This kind of relationship is commonly named "many-to-many" relation.

Run in JBossForge:

```
[awesomeapp]$ jpa-new-field
```

    ***INFO*** Required inputs not satisfied, entering interactive mode

    [0] ( ) com.mycompany.awesomeapp.model.Author
    [1] (x) com.mycompany.awesomeapp.model.Book

    Press to confirm, or +C to cancel.
    * Target Entity (The targetEntity which the field will be created): [0-1] 1
    * Field Name (The field name to be created in the target targetEntity):  author
    * Field Type (The type intended to be used for this field) [String]:  com.mycompany.awesomeapp.model.Author
    ? Column Name (The column name. Defaults to the field name):  author_id
    ? Length (The column length. (Applies only if a string-valued column is used.)) [255]:
    ? Not Nullable [y/N]:
    ? Not Insertable [y/N]:
    ? Not Updatable [y/N]:

    [0] ( ) Basic
    [1] ( ) One-to-Many
    [2] ( ) One-to-One
    [3] (x) Many-to-Many
    [4] ( ) Many-to-One

    Press to confirm, or +C to cancel.
    ? Relationship Type (The relationship type): [0-4] 3
    ? Is Transient? (Creates a field with @Transient) [y/N]:
    ***SUCCESS*** Relationship Many-to-Many created


# 9. Generate REST API for manipulating authors and books.

Run in JBossForge:

```
[awesomeapp]$ rest-generate-endpoints-from-entities
```

    ***INFO*** Required inputs not satisfied, entering interactive mode

    Press to confirm, or +C to cancel.
    * Targets: [0-1] 0
    * Targets: [0-1] 1

    [0] (x) com.mycompany.awesomeapp.model.Author
    [1] (x) com.mycompany.awesomeapp.model.Book

    Press to confirm, or +C to cancel.
    * Targets: [0-1]

    [0] (x) JPA_ENTITY
    [1] ( ) ROOT_AND_NESTED_DTO

    Press to confirm, or +C to cancel.
    * Generator: [0-1] 0
    * Content Type [application/json]:
    * Target Package Name [com.mycompany.awesomeapp.rest]:

    [0] (x) awesomeapp-persistence-unit

    Press to confirm, or +C to cancel.
    * Persistence Unit: [0]
    ***SUCCESS*** Endpoint created

# 10. Running app

That's all coding, now let's run our app.

# Build app
```bash
mvn install
```

Application artifact will be created in file `target/AwesomeApp.war`
## Install Wildlfy:

### Download WildFly:
```bash
wget 'http://download.jboss.org/wildfly/10.0.0.Final/wildfly-10.0.0.Final.tar.gz'
```

### Unpack Wildfly package:
```bash
tar -xvzf wildfly-10.0.0.Final.tar.gz -C /tmp/
```

### Start Wildfly:
```bash
/tmp/wildfly-10.0.0.Final/bin/standalone.sh
```

### Run app (deploy artifact) to Wildfly

Copy file target/AwesomeApp.war to deployment dir of application server, in this example to Wildfly:

```
cp target/AwesomeApp.war /tmp/wildfly-10.0.0.Final/standalone/deployment/
```

Now application should start

Check server logs in file `/tmp/wildfly-10.0.0.Final/standalone/log/server.log`

### Example use of REST API:

#### Author:

* To add author send REST POST request to URL http://localhost:8080/AwesomeApp/rest/authors

* Example JSON input data:

```json
{
  "name": "Mark",
  "surname": "Twain"
}
```

```json
{
  "name": "Arthur C.",
  "surname": "Clark"
}
```

```json
{
  "name": "Stephen",
  "surname": "Baxter"
}
```


* Examples in CURL:

```bash
curl -H "Content-Type: application/json" -X POST \
-d '{"name":"Mark","surname":"Twain"}' \
http://localhost:8080/AwesomeApp/rest/authors
```

```bash
curl -H "Content-Type: application/json" -X POST \
-d '{"name":"Arthur C.","surname":"Clark"}' \
http://localhost:8080/AwesomeApp/rest/authors
```

```bash
curl -H "Content-Type: application/json" -X POST \
-d '{"name":"Stephen","surname":"Baxter"}' \
http://localhost:8080/AwesomeApp/rest/authors
```

* GET authors data: http://localhost:8080/AwesomeApp/rest/authors
* To add book send REST POST request to URL http://localhost:8080/AwesomeApp/rest/books
* Example input data

```json
{
  "title": "The Adventures of Tom Sawyer",
  "year": 1876,
  "author": [
    {
      "id": 1
    }
  ]
}
```

Second book:

```json
{
  "title": "Adventures of Huckleberry Finn",
  "year": 1884,
  "author": [
    {
      "id": 1
    }
  ]
}
```

Add book with two authors:

```json
{
  "title": "Firstborn",
  "year": 2007,
  "author": [
    {
      "id": 2
    },
    {
      "id": 3
    }
  ]
}

```

* Examples in CURL:

```bash
curl -vv -H "Content-Type: application/json" -X POST \
-d '{"title":"The Adventures of Tom Sawyer","year":1876,"author":[{"id":1}]}' \
http://localhost:8080/AwesomeApp/rest/books
```

```bash
curl -vv -H "Content-Type: application/json" -X POST \
-d '{"title":"Adventures of Huckleberry Finn","year":1884,"author":[{"id":1}]}' \
http://localhost:8080/AwesomeApp/rest/books
```

```bash
curl -vv -H "Content-Type: application/json" -X POST \
-d '{"title":"Firstborn","year":2007,"author":[{"id":2},{"id":3}]}' \
http://localhost:8080/AwesomeApp/rest/books
```

* GET all books
http://localhost:8080/AwesomeApp/rest/books

* GET book with id=1
http://localhost:8080/AwesomeApp/rest/boooks/1

* GET all authors
http://localhost:8080/AwesomeApp/rest/authors

* GET author with id=1
http://localhost:8080/AwesomeApp/rest/authors/1

* Other REST methods: UPDATE, DELETE allows you to modify or delete data

## Required tools ##
* Java SE Development Kit 8 (JDK) - compiling and running app
  [Java JDK download](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* WildFly - Java EE Application Server
  [wildfly.org](http://wildfly.org/downloads/) or [Wildfly 10.0.0.Final.tar.gz](http://download.jboss.org/wildfly/10.0.0.Final/wildfly-10.0.0.Final.tar.gz)
* Maven 3+
  [https://maven.apache.org/download.cgi](https://maven.apache.org/download.cgi)
* JBoss Forge 3+ (zip install)
  [http://forge.jboss.org/download](http://forge.jboss.org/download) or [forge 3.0.1 zip](http://downloads.jboss.org/forge/releases/3.0.1.Final/forge-distribution-3.0.1.Final-offline.zip)
* CURL - Command line tool for http
  [curl.haxx.se](https://curl.haxx.se/)
