---
layout: essay
type: essay
title: "Getting Help or Getting Ignored"
# All dates must be YYYY-MM-DD format!
date: 2023-09-06
published: true
labels:
  - Questions
  - Answers
  - StackOverflow
---

<img width="300px" class="rounded float-start pe-4" src="../img/stackoverflow-logo-300.png">

## Asking questions the right way

When asking questions online in support forums, the way you frame your questions can significantly impact the quality and speed of the help that you receive. Eric Raymond's, "How To Ask Questions The Smart Way," provides integral tips that will help structure questions for the highest effectiveness. According to Raymond, structuring your questions with an "Object - Deviation" format is a powerful strategy that enhances the likelihood of getting attention from individuals who have more knowledge than you.

The "Object - Deviation" format involves creating a title that concisely describes the specific context and the issue you are encountering. Here's how it works:

## The Object

This represents the particular circumstances or elements related to your problem. It can be anything from software versions to hardware components or coding environments. Essentially, it sets the stage for understanding the context in which the issue has come about.

## The Deviation
The "Deviation" component of the title outlines the specific problem or abnormality you are facing. It provides a clear and concise description of the issue without delving into details. This precision is integral to ensure that potential helpers can quickly identify the core problem.

For example, look to this made up question: "VALORANT 1.23 - Massive frame drops." VALORANT 1.23 mentions the program and software version, while "massive frame drops" highlight the specific issue. This structured approach ensures that helpers understand both the context and the problem, reducing ambiguity and adding less steps to the troubleshooting process. These titles provide lots of benefits technically as well. It can help helpers identify areas of their expertise, where they may have had, and fixed, the same problem before. The issue could arise from many areas including the software, hardware, or an external source. Also, this question formatting helps eliminate “hunch biases” which helps prevent helpers from making assumptions about the details of the problem.

## What is a real, good question?

This example comes from a user asking the question: ["'JavaPackage' object is not callable" error executing explain() in Pyspark 3.0.1 via Zeppelin.](https://stackoverflow.com/questions/65713299/javapackage-object-is-not-callable-error-executing-explain-in-pyspark-3-0)

```
Q: I am running Pyspark 3.0.1 for Hadoop 2.7 in a Zeppelin notebook. In general all is well, however when I execute df.explain() on a DataFrame I get this error:

Fail to execute line 3: df.explain()
Traceback (most recent call last):
  File "/tmp/1610595392738-0/zeppelin_python.py", line 158, in <module>
    exec(code, _zcUserQueryNameSpace)
  File "<stdin>", line 3, in <module>
  File "/usr/local/spark/python/pyspark/sql/dataframe.py", line 356, in explain
    print(self._sc._jvm.PythonSQLUtils.explainString(self._jdf.queryExecution(), explain_mode))
TypeError: 'JavaPackage' object is not callable

Has anyone come across and resolved this error before in the context of explain ?

My spark/jars folder contents:

(lists their spark/jars folder)
```

The developer provides a clear title that specifies the software version (Pyspark 3.01 via Zeppelin) and the exact issue ('JavaPackage' object is not callable) they are encountering. They also include relevant code snippets and error messages, enabling helpers to offer precise solutions.

```
A: I ran into this same issue on AWS with EMR 6.2.0 (also Spark 3.0.1 coincidentally?) and jupyter notebooks. The issue appears to be related to how pyspark is initialized. Specifically, the py4j Java imports.

The following import is supposed to be executed while the notebook kernel is being initialized but seems to be skipped. You just need to run this once per session.

from py4j.java_gateway import java_import
java_import(spark._sc._jvm, "org.apache.spark.sql.api.python.*")
Now df.explain() works as expected.

For future reference - when you see 'JavaPackage' object is not callable, it often means that the target Java class was not found. Either the class doesn't exist or the expected import hasn't been called.

```
 
The asker recieved a very specific answer from someone who has envountered the exact problem before. This could have been necause the asker was so specific in their question that the helper saw it and recognized the error as one they have seen before.

## How can I get ignored and get nowhere with my problem?

This example comes from a user asking the question: [linear-gradient syntax unclear.](https://stackoverflow.com/questions/70777494/linear-gradient-syntax-unclear)

```
Q: I am trying to understand this pen, but I have difficulties understanding line 44-45 in the SCSS file:

background: linear-gradient(var(--menu-link-active-color) 0 100%) left / 0 repeat;

I looked up many websites, but I couldn't find anything about linear-gradient() with 3 parameters. And also the slash is very unclear. I would be happy to get a hint or an explanation what this is!
```
In this instance, the title lacks specificity. It is not clear what this problem is pertaining to so helpers may not click on it as they don’t know what it means. After clicking, the developer says that it is about a pen tool in CSS I believe but it is not entirely clear. The first example adheres to the "Object - Deviation" format, while the second example falls short. As expected, the first question received more focused and effective responses, whereas the second question asks for additional information and less-targeted assistance. 


## Conclusion

In conclusion, the art of asking smart questions is a powerful skill that can greatly enhance your interactions in online support forums and communities. By using the "Object - Deviation" format, you can help yourself to communicate your issues more clearly, increasing the likelihood of receiving a timely and relevant solution. Ultimately, this structured approach not only benefits you but also contributes to a more efficient and productive collaborative environment within the software development community as people do not need to ask more questions to make the original clear.
