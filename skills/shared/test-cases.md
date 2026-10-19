# ACE Test Cases

## Purpose
This document defines ACE-focused guidance for creating and refining ACE Test Cases which are saved in ACE Test Projects and can be executed using the ACE Unit Testing framework

## When to use
Use this document when generating or reviewing ACE Test Cases. ACE Test Cases can be used for different purposes. This skill uses the following terminology:
1. A Unit Test is an ACE Test Case which aims to test ONE message flow node (Compute, JavaCompute, Mapping, Filter, Route etc.).  Unit Tests will not require external systems to be available in order to execute. They will include stubs, test doubles or mocks in place of external systems.
2. A Component Test is an ACE Test Case which aims to test more than one message flow node. Component tests will typically involve testing a whole subflow or a sequence of several message flow nodes within a message flow. Component Tests will not require external systems to be available in order to execute. They will include stubs, test doubles or mocks in place of external systems.
3. A Integration Test aims to test more than one message flow node and can even involve multiple message flows acting together. Integration Tests may require external systems to be available in order to execute. Integration Tests may not be appropriate for running as an ACE Test Case in an ACE Test Project, executed using the ACE Unit Testing framework.

## Inputs you must read first

When generating a new ACE Unit Test or Component Test, you must first: read 
1. Locate the relevant ACE Project (most likely an Application project, a REST API project or an Integration Service project) which contains the flow source which needs to be tested and is defined in the `.msgflow` / `.subflow` file
2. Read the `.msgflow` / `.subflow` source files. Use this to find out message flow node names, terminal names and subflow nesting. Never derive an expected value from the code under test.
3. Read the `.esql` / `.java` / `.map` files which are invoked as part of the message flow's execution.

## Where the tests live

- ACE Test Cases are saved in ACE Test Projects.
- ACE Test Project name should be `<Application>_Test`, where `<Application>` is the name of the Application project which contains the message flow which needs to be tested. 
- If the project does not already exist, create it using the guidance in [`skills/shared/test-projects.md`](test-projects.md).
- The `.java` source file containing one or more ACE Test Cases should be located at `<Application>_Test/src/main/java/<package path>/<Application>_<MessageFlow>_<Node>_Tests.java`
- If the message flow which needs to be tested includes a subflow, then the `.java` source file containing one or more ACE Test Cases should be located at `<Application>_Test/src/main/java/<package path>/<Application>_<MessageFlow>_<SubflowNode>_<Node>_Tests.java`
- The `.java` source file represents a single public class and should contain all the ACE Test Cases for testing a single message flow node.
- Within the class, there should be one `@Test` method per behaviour of a message flow node that you wish to test. This method is the ACE Test Case. ACE Test Cases 
- Each ACE Test Case should have its own unique name. A standard convention is to use a four digit suffix to number each ACE Test Case which is testing a given message flow node. This provides for plenty of expansion space as it allows for up to 9999 separate Test Cases for a single message flow node.

## How to address a message flow node in an ACE Test Case

Build a `SpyObjectReference` using the names in the message flow source `.msgflow` file:
```java
SpyObjectReference ref = new SpyObjectReference()
    .application("<Application>")
    .messageFlow("<MessageFlow>")
    .subflowNode("<SubflowNode>")   // repeat for each nesting level, omit if none
    .node("<Node>");
NodeSpy spy = new NodeSpy(ref);
```
Names are the node LABELS in the flow, including spaces. Read them from the `.msgflow` / `.subflow` XML source file. Do not guess.
Terminal names (such as `in`, `out`, `out1`, `failure`, ...) also come from the flow XML.

## How to define the input data for an ACE Test Case

Prefer building the input message in code, field by field, so that the ACE Test Case shows what it depends on:
```java
TestMessageAssembly input = new TestMessageAssembly();
input.messagePath("JSON.Data.id").setValue(123);
input.messagePath("XMLNSC.order.customer.name").setValue("Joe Bloggs");
input.localEnvironmentPath("HTTP.Input.QueryString.MyParam1").setValue("MyValue1");
```

Use a recorded message assembly file (with `.mxml` extension) only when one already exists in `src/main/resources` or when one is explicitly provided by the user, or when one is generated using the `ibmint generate tests` command
```java
InputStream in = Thread.currentThread().getContextClassLoader().getResourceAsStream("<file>.mxml");
input.buildFromRecordedMessageAssembly(in);
```


## ACE Test Case Rules

1. Never delete, disable or weaken an existing test to make a build pass.
2. Never independently change an expected value unless the requirement or mapping changed. Say which line changed in your summary. Only change expected values if explicitly directed to do so by the user.
3. If the definition of a message flow and its test disagree, do not adjust the test. Report a flow defect.
4. You should not include credentials, host names or environment-specific values in ACE Test Cases.



