# ACE Version References

## Purpose
This document centralizes version-specific IBM App Connect Enterprise (ACE) references used by the ACE Flowpilot skills.

## When to use
Use this document whenever a task depends on schema validation, project structure differences, or other version-specific ACE behavior.

### Detecting the ACE Toolkit version
If the user has requested a task that depends on locating a file or a command which is part of an ACE installation, first try to detect to see if this skill is being used within a shell or terminal session launched from within an instance of the ACE Toolkit:
1. Starting from the current shell process, walk up the chain of parent processes until you find the ACE Toolkit process. It is the process whose command line contains com.ibm.etools.msgbroker.tooling.ide. On Windows, its executable is also named toolkit_<version>.exe, for example toolkit_13_0_9_0.exe.
2. Take the Toolkit's executable path and read the ACE install location and version from it. On Windows, for example, C:\Program Files\IBM\ACE\13.0.9.0\tools\toolkit_13_0_9_0.exe gives the install root C:\Program Files\IBM\ACE\13.0.9.0 and the version 13.0.9.0.
3. Use the install root to build any paths you need, such as the schema folders under common/schemas. Don't use a hard-coded version.    
4. If no Toolkit process is found, for example because the shell was started outside the Toolkit, do not guess. Ask the user which ACE version they are using.
5. Tell the user which version you detected and how, so they can correct it.

## Supported version references
The current skill content was originally authored with ACE 13 schema paths in mind. Version-specific references should be maintained here rather than embedded throughout other files.

## Schema locations

### Message Flow schema
- MessageFlow.xsd and MessageFlowUI.xsd are schemas provided as part of the ACE product install that can help you use correct syntax when creating `.msgflow` files
- The XSD files can be found in the ACE installation at `<ACE Install Location>/common/schemas/MessageFlow'
- For example the location within the default install location on Windows is `C:\Program Files\IBM\ACE\13.0.M.F\common\schemas\MessageFlow` where M represents the ACE Modification release number and F represents the ACE Fixpack release number such as `13.0.9.0` In general pick the latest available release, and therefore the directory with the highest available number M.
- For example the location within the default install location on Linux is `/opt/IBM/ace-13.0.M.F/common/schemas/MessageFlow` where M represents the ACE Modification release number and F represents the ACE Fixpack release number such as `13.0.9.0` In general pick the latest available release, and therefore the directory with the highest available number M.
- For example the location within the default install location on MacOS is `/Applications/IBM App Connect Enterprise 13.0.M.F/common/schemas/MessageFlow` where M represents the ACE Modification release number and F represents the ACE Fixpack release number such as `13.0.9.0` In general pick the latest available release, and therefore the directory with the highest available number M.
- If you do not have access to the XSD files you should ask the user to provide them from the above location.

### Policy schema
- Policy.xsd schema is provided as part of the ACE product install and can help you use correct syntax when creating `.policyxml` files
- This XSD file can be found in the ACE installation at `<ACE Install Location>/common/schemas/Policy'
- For example the location within the default install location on Windows is `C:\Program Files\IBM\ACE\13.0.M.F\common\schemas\Policy` where M represents the ACE Modification release number and F represents the ACE Fixpack release number such as `13.0.9.0` In general pick the latest available release, and therefore the directory with the highest available number M.
- For example the location within the default install location on Linux is `/opt/IBM/ace-13.0.M.F/common/schemas/Policy` where M represents the ACE Modification release number and F represents the ACE Fixpack release number such as `13.0.9.0` In general pick the latest available release, and therefore the directory with the highest available number M.
- For example the location within the default install location on MacOS is `/Applications/IBM App Connect Enterprise 13.0.M.F/common/schemas/Policy` where M represents the ACE Modification release number and F represents the ACE Fixpack release number such as `13.0.9.0` In general pick the latest available release, and therefore the directory with the highest available number M.
- If you do not have access to the XSD file you should ask the user to provide it from the above location.

### Connector policy schema
- Connector policies (`policyType` set to a connector code such as `salesforce` or `servicenow`) are not defined in Policy.xsd. Their types are in PolicyConnectors.xsd, and the Toolkit's templates for them in PolicyUIConnectors.xsd.
- Both XSD files are in the ACE installation at `<ACE Install Location>/common/schemas/Connectors`, next to the `Policy` folder above, with the same install locations per platform.

## Rules
- Do not hard-code ACE schema locations in multiple documents when a reference to this file is sufficient.
- When validating node `xmi:type` values, use the Message Flow schema applicable to the user's ACE version.
- When validating policy XML content, use the schema applicable to the user's ACE version that defines the policy's `policyType`: Policy.xsd for the built-in policy types, PolicyConnectors.xsd for connector policies.

## Related files
- [`skills/shared/message-flow-rules.md`](message-flow-rules.md)
- [`skills/shared/node-types.md`](node-types.md)
- [`skills/shared/policy-projects.md`](policy-projects.md)

## Maintenance notes
- Add new ACE versions here as they are validated.
- If a later ACE version changes schema locations or node type names, document those differences here.
