# AI Javadoc writer

Did you ever have the problem with this large legacy code base and wished for a good javadoc? Do you wish your fellow coders would have written a reasonable javadoc of their Java java code?

Just use the docwriter to update your application JavaDoc with AI generated documentation. You can decide if the documenation should only span the class/interface declarations, or should cover evey public/private method.

## Eat my own dogfood:
Undocumented code
```java
@SpringBootApplication
@Slf4j
public class DocWriterApplication implements CommandLineRunner {

    ...

    @Override
    public void run(String ... args) throws Exception {
        logArgs();
		addDocs();

    }

}

```
Gets documented as
```java
/**
 *  The DocWriterApplication class is responsible for adding missing Javadoc to classes and interfaces in Java source code.
 *  It utilizes the OpenAI GPT-3.5 Turbo model to generate the Javadoc based on the provided source code.
 *  The Javadoc is added as class/interface-level comments and includes an author tag with the specified author name.
 *
 * @author DocWriterApplication
 */
@SpringBootApplication
@Slf4j
public class DocWriterApplication implements CommandLineRunner {

    ...

    @Override
    public void run(String ... args) throws Exception {
        logArgs();
		addDocs();

    }

}
```

## How to run this
Since you are documenting a java application, a good understanding of running a java application is assumed. 

Prerequisites:
* pre unstalled java version 17 or newer
* pre installed maven
* openai Api Key as the API not for free. https://platform.openai.com/docs/quickstart/step-2-setup-your-api-key

```bash
export OPENAI_API_KEY==your-openapi-key
./docWriter.sh --srcDir=./src/main/java 
```

You can provide any combination of these parameters
```bash
./docWriter.sh --srcDir=./src/main/java --maxFileToChange=10 --classDoc=true --publicMethodDoc=false --privateMethodDoc=false --author=yourname

```

This will traverse all the java files in the passed directory, and generate JavaDoc. Dont forget to proof read these docs before propagating/comitting.

## Privacy consideration
Your code will be partially sent to OpenAI as part of the completion requests. Please note however, that OpenAI policy 
* excludes such data from training
* keeps the data ownership with you for both input (code) and output (docs)

https://openai.com/enterprise-privacy



