# JavaPOS
The UnifiedPOS reference implementation for Java provided by UnifiedPOS committee members.

This project, in fact, is an aggregating project which does not contain source code itself.
It aggregates the project jar files from the following projects in this organization
* [JavaPOSContracts](https://github.com/JavaPOSWorkingGroup/JavaPOSContracts)
* [JavaPOSControls](https://github.com/JavaPOSWorkingGroup/JavaPOSControls)
* [JavaPOSConfigLoader](https://github.com/JavaPOSWorkingGroup/JavaPOSConfigLoader) (aka JCL)

The result of the aggregation is equal to the `jpos1xxx.jar` at the distribution archives like `JavaPOS-1.xx.x-Dist.zip` from the http://javapos.com side. In fact, this jar file contains the JavaPOS service interfaces and data types (contracts) and the JavaPOS device control classes, as well as the JavaPOS Config Loader classes all together. The distribution archive furthermore contains a `jpos-1xxx-controls.jar` which in general contains the same as the first jar except from the JavaPOS Config Loader classes.

## Issues From Original Project Structures

Originally, the sources for creating those libraries has been maintained in two different projects: The JavaPOS Config Loader sources were hosted in project on [Sourceforge](https://sourceforge.net/projects/jposloader/?source=navbar). The JavaPOS service interfaces, data types and device control classes were not publically hosted but maintained together in one project.

When migrating the source to GitHub it turned out that both original projects have a circular dependency. The JavaPOS device controls types depends on `jpos.JposServiceConnection` from the JCL sources. Whereas the JCL sources depends on JavaPOS data types like `jpos.JposConst` or `jpos.JposException`. 

This is a awkward circumstance for two reasons:

1. When populating libraries to maven.org and bintray.com the dependencies are registerd too and may be used for dependency resolving mechanisms by client build mechanims.

2. Both projects are not able to be build from the scratch without an bootstrap mechanism (where a part from the first or second project is build first to satisfy the dependency requirements from the other) which makes it hard to build theses projects on continues integration services like https://travis-ci.org.

## New Project Structures

As a solution to that the original code has been rearranged into 3 different projects:
* [JavaPOSContracts](https://github.com/JavaPOSWorkingGroup/JavaPOSContracts)
  * hosts the JavaPOS device service interface, data type and constant sources; in particular `jpos.*Const`, `jpos.events.*`, `jpos.services.*`
  * additionally it contains the interface type `jpos.loader.JposServiceInstance` from the original JavaPOS Config Loader project as this is later on needed by the JavaPOS device controls
* [JavaPOSConfigLoader](https://github.com/JavaPOSWorkingGroup/JavaPOSConfigLoader)
  * hosts the JavaPOS Config Loader sources as loaded from the original project except for the interface type `jpos.loader.JposServiceInstance`
  * depends on the new JavaPOS Contracts project
* [JavaPOSControls](https://github.com/JavaPOSWorkingGroup/JavaPOSControls)
  * hosts the JavaPOS device control sources
  * depends on the new JavaPOS Contracts project and the new JavaPOS Config Loader project

In that way no circular dependency is anymore in the independant source projects.

## Flexibility in Dependency Management

Furthermore we will get more flexibility on dependency management:
* the jar library built from [JavaPOSContracts](https://github.com/JavaPOSWorkingGroup/JavaPOSContracts) project may be used by JavaPOS device service implementors during implementation tasks without depending on the JavaPOS device control library and the JCL library
* software vendors providing their own JavaPOS device control implementations may deploy the [JavaPOS contracts library](https://github.com/JavaPOSWorkingGroup/JavaPOSContracts) and [JCL library](https://github.com/JavaPOSWorkingGroup/JavaPOSConfigLoader) only, substituting the reference implementation of the JavaPOS device control library by their own implementation
* application vendors and integrators may use libraries built from those single projects in a set or using the aggregated library built from this project for easier deployment

## Separated JCL Editor Project

Orginally, the JCL source project also hosts an graphical editor application for JavaPOS Config Loader configuration sources.
The sources for this application has been separated into the project [JCLEditor](https://github.com/JavaPOSWorkingGroup/JCLEditor) as it is a standalone application and is not required as dependency by ordinary JavaPOS applications.
This project has only a dependency to the new [JCL project](https://github.com/JavaPOSWorkingGroup/JavaPOSConfigLoader).




