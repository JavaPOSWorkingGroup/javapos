[![Gitpod ready-to-code](https://img.shields.io/badge/Gitpod-ready--to--code-blue?logo=gitpod)](https://gitpod.io/#https://github.com/JavaPOSWorkingGroup/javapos) 
[![CI](https://github.com/JavaPOSWorkingGroup/javapos/actions/workflows/build.yml/badge.svg)](https://github.com/JavaPOSWorkingGroup/javapos/actions/workflows/build.yml)
[![Release Build](https://github.com/JavaPOSWorkingGroup/javapos/actions/workflows/release.yml/badge.svg)](https://github.com/JavaPOSWorkingGroup/javapos/actions/workflows/release.yml)
[![Maven Central](https://maven-badges.herokuapp.com/maven-central/org.javapos/javapos/badge.svg)](https://maven-badges.herokuapp.com/maven-central/org.javapos/javapos/)

# JavaPOS 

The UnifiedPOS reference implementation for Java provided by UnifiedPOS committee members.

Use this library, if your are implementing JavaPOS device services or an JavaPOS application using the [reference implementation of device controls](https://github.com/JavaPOSWorkingGroup/javapos-controls) provided by this group (instead of using your own). In that case this library is valid to be deployed to production environments too.

If you have implemented your own version of device controls, do not use this libraray! Use the both libraries [javapos-contracts](https://github.com/JavaPOSWorkingGroup/javapos-contracts) and [javapos-config-loader](https://github.com/JavaPOSWorkingGroup/javapos-config-loader) instead of this one to avoid class ambiguities on your class-path.

Since version 1.15.4 of this package, the [javapos-config-loader](https://github.com/JavaPOSWorkingGroup/javapos-config-loader) version 4.0 gets incorporated which does not have a Xerces dependency anymore. Instead the XML parser from the Java framework library is used. This solves mainly vulnerability issues, no new functionality was added.
If you need to use the older version 3 of the JavaPOS Config Loader provided by [javapos-config-loader](https://github.com/JavaPOSWorkingGroup/javapos-config-loader) then do not use this library! Instead, use the three libraries [javapos-contracts](https://github.com/JavaPOSWorkingGroup/javapos-contracts), [javapos-config-loader](https://github.com/JavaPOSWorkingGroup/javapos-config-loader), and [javapos-controls](https://github.com/JavaPOSWorkingGroup/javapos-controls) for their own to have control of their specific versions.

NOTE: The documentation shown here in the past about project evolving has been moved to a [Wiki page](https://github.com/JavaPOSWorkingGroup/javapos/wiki/Migrating-to-And-Joining-All-Sources-At-GitHub). 
