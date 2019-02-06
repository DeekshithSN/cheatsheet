
- mvn help:evaluate -Dexpression="project.artifactId".  --> to get artifact id

- mvn help:evaluate -Dexpression="project.groupId".    --> to get groupid

- mvn help:effective-pom -Doutput=pom_eff.xml        --> gives effective pom

- mvn install -Dmaven.repo.local=/alternate/repo/location     --> if you want to run project with different .m2 folder

- mvn  -B dependency:resolve-plugins  --> gives all the plugins

- mvn dependency:tree --> dependency tree
