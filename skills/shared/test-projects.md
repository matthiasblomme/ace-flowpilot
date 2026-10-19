# ACE Test Projects

## Purpose
This document defines the required structure for IBM App Connect Enterprise (ACE) Test projects.

## When to use
Use this document when creating ACE unit tests which should always be created inside an ACE Test project.

## When to create a Test project
- Create a Test project when creatin ACE unit tests and the user has not identified an existing suitable Test project.
- ACE unit tests must be created in a Test project, and not in an Application project or REST API project or Library project.
- If the user has not specified a name for the Test project, follow the convention of using a name that has a `_Test` suffix added to the name of the Application project (which hosts the message flows which the user is aiming to be subject of the unit testing).

## Required project files
An ACE Test project must contain:
- a `.project` file in the project root
- a `bin` directory
- a `src` directory
- a `src/main/java` directory
- a `src/main/resources` directory
- a `.settings` directory
- a `.settings/org.eclipse.core.resources.prefs` file
- a `testproject.descriptor` file in the project root
- a `.classpath` file in the project root


## `.project` requirements

**Use the following example `.project` file.** Replace `<ProjectName>` with the actual project folder name. Do not add, remove, or modify any `<nature>` entries — the file must contain exactly the natures shown and no others.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<projectDescription>
	<name><ProjectName></name>
	<comment></comment>
	<projects>
	</projects>
	<buildSpec>
		<buildCommand>
			<name>org.eclipse.jdt.core.javabuilder</name>
			<arguments>
			</arguments>
		</buildCommand>
		<buildCommand>
			<name>com.ibm.etools.mft.applib.mbprojectbuilder</name>
			<arguments>
			</arguments>
		</buildCommand>
		<buildCommand>
			<name>com.ibm.etools.msg.validation.dfdl.mlibdfdlbuilder</name>
			<arguments>
			</arguments>
		</buildCommand>
		<buildCommand>
			<name>com.ibm.etools.mft.flow.adapters.adapterbuilder</name>
			<arguments>
			</arguments>
		</buildCommand>
		<buildCommand>
			<name>com.ibm.etools.mft.flow.sca.scabuilder</name>
			<arguments>
			</arguments>
		</buildCommand>
		<buildCommand>
			<name>com.ibm.etools.msg.validation.dfdl.mbprojectresourcesbuilder</name>
			<arguments>
			</arguments>
		</buildCommand>
		<buildCommand>
			<name>com.ibm.etools.mft.esql.lang.esqllangbuilder</name>
			<arguments>
			</arguments>
		</buildCommand>
		<buildCommand>
			<name>com.ibm.etools.mft.map.builder.mslmappingbuilder</name>
			<arguments>
			</arguments>
		</buildCommand>
		<buildCommand>
			<name>com.ibm.etools.mft.flow.msgflowxsltbuilder</name>
			<arguments>
			</arguments>
		</buildCommand>
		<buildCommand>
			<name>com.ibm.etools.mft.flow.msgflowbuilder</name>
			<arguments>
			</arguments>
		</buildCommand>
		<buildCommand>
			<name>com.ibm.etools.mft.decision.service.ui.decisionservicerulebuilder</name>
			<arguments>
			</arguments>
		</buildCommand>
		<buildCommand>
			<name>com.ibm.etools.mft.pattern.capture.PatternBuilder</name>
			<arguments>
			</arguments>
		</buildCommand>
		<buildCommand>
			<name>com.ibm.etools.mft.json.builder.JSONBuilder</name>
			<arguments>
			</arguments>
		</buildCommand>
		<buildCommand>
			<name>com.ibm.etools.mft.restapi.ui.restApiDefinitionsBuilder</name>
			<arguments>
			</arguments>
		</buildCommand>
		<buildCommand>
			<name>com.ibm.etools.mft.policy.ui.policybuilder</name>
			<arguments>
			</arguments>
		</buildCommand>
		<buildCommand>
			<name>com.ibm.etools.msg.validation.dfdl.dfdlqnamevalidator</name>
			<arguments>
			</arguments>
		</buildCommand>
		<buildCommand>
			<name>com.ibm.etools.mft.bar.ext.barbuilder</name>
			<arguments>
			</arguments>
		</buildCommand>
		<buildCommand>
			<name>com.ibm.etools.mft.unittest.ui.TestCaseBuilder</name>
			<arguments>
			</arguments>
		</buildCommand>
		<buildCommand>
			<name>com.ibm.etools.mft.msg.assembly.messageAssemblyBuilder</name>
			<arguments>
			</arguments>
		</buildCommand>
		<buildCommand>
			<name>com.ibm.etools.mft.applib.applibbuilder</name>
			<arguments>
			</arguments>
		</buildCommand>
		<buildCommand>
			<name>com.ibm.etools.mft.jcn.jcnbuilder</name>
			<arguments>
			</arguments>
		</buildCommand>
	</buildSpec>
	<natures>
		<nature>com.ibm.etools.msgbroker.tooling.testProjectNature</nature>
		<nature>org.eclipse.jdt.core.javanature</nature>
		<nature>com.ibm.etools.mft.jcn.jcnnature</nature>
		<nature>com.ibm.etools.mft.bar.ext.barnature</nature>
	</natures>
</projectDescription>
```

## `.settings` requirements
The `.settings/org.eclipse.core.resources.prefs` file must contain:

```properties
eclipse.preferences.version=1
encoding/<project>=UTF-8
```

## `testproject.descriptor` requirements
The `testproject.descriptor` file must exist in the project root and use the structure shown below

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<ns2:testprojectDescriptor xmlns="http://com.ibm.etools.mft.descriptor.base" xmlns:ns2="http://com.ibm.etools.mft.descriptor.testproject">
<references/>
</ns2:testprojectDescriptor>
```

If it is known which Application the Test project is designed to be testing, then you must add content within the `<references>` element like this: `<applicationReference><applicationName>ExampleApplicationBeingTested</applicationName></applicationReference></references></ns2:testprojectDescriptor>` where `ExampleApplicationBeingTested` is the name of the Application project which contains the message flows which are to be tested.

## `.classpath` requirements
The `.classpath` file must contain:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<classpath>
	<classpathentry kind="src" path="src/main/java"/>
	<classpathentry kind="con" path="org.eclipse.jdt.launching.JRE_CONTAINER"/>
	<classpathentry kind="con" path="org.eclipse.jdt.junit.JUNIT_CONTAINER/5"/>
	<classpathentry kind="con" path="org.eclipse.jdt.USER_LIBRARY/Integration Test Library"/>
	<classpathentry kind="output" path="bin"/>
</classpath>
```