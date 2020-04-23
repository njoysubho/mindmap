## My experience Micronaut

Following the development of micronaut from very early days. 
Micronaut is pragmatic in the sense they didn't try to completely replace Spring and re invent wheel rather
they address teh core issue in Spring which is startup time. Micronaut is fast due to its compile time identifivation
of injection points. 
Developer experience is seamless if some one coming from Spring background .
One small hitch though, in Spring a class with Coponent/Service/Repository annotation will default create a 
bean whether it is used some where or not but in Micronaut this is not the case , because it generate classes which has 
injection point defined the beans will not be created hence if you expecting to run some code on startup within @PostConstruct annotated method that will not run.

Super support for Graal Native Image. 

Support for Spring cloud config.

Same experience as spring data repository.

Almost all functionality available like Spring.


