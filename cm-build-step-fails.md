## Build step fails in Cloud Manager but not on local maven build

### Extract the mvn commands from the maven_build.log
1. Download the maven_build.log file from the Cloud Manager UI
2. Extract the exact maven commands from the maven_build.log to run them on the local build.  Either run the grep command below or search for all lines containing "Executing command mvn ".

        grep "Executing command mvn " maven_build.log | grep -Eo "mvn .*$"

        mvn --batch-mode org.codehaus.mojo:versions-maven-plugin:2.6:set -DnewVersion=2020.1007.215239.0000192274 -DprocessAllModules=true -DartifactId=* -DgroupId=* -DoldVersion=* -DgenerateBackupPoms=false
        mvn --batch-mode org.apache.maven.plugins:maven-dependency-plugin:3.1.2:resolve-plugins
        mvn --batch-mode de.qaware.maven:go-offline-maven-plugin:resolve-dependencies
        mvn --batch-mode org.apache.maven.plugins:maven-clean-plugin:3.1.0:clean -Dmaven.clean.failOnError=false
        mvn --batch-mode org.jacoco:jacoco-maven-plugin:prepare-agent package -DcloudManagerOriginalVersion=0.0.1-SNAPSHOT

3. Run those mvn commands on the local build and you should see the same failures as in the cloud manager build

### If build fails in Production and Stage pipelines but not in Dev

* Production and Stage pipelines use the versions-maven-plugin to generate a version
  * versions-maven-plugin documentation - [https://www.mojohaus.org/versions-maven-plugin/]
  * Related [Cloud Manager documentation](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/managing-code/activating-maven-project.html)

### If a build fails due to a missing commit in a sub-module
If you see an error like this one in the maven_build.log file:
```
fatal: git fetch-pack: expected ACK/NAK, got '?TF401035: The object '1446245ab51f138dc3ea82635856c9f417c12345' does not exist.'
fatal: The remote end hung up unexpectedly
Fetched in submodule path 'CM_Test_Submodule', but it did not contain 1446245ab51f138dc3ea82635856c9f417c12345. Direct fetching of that commit failed.
```
Then your sub-module points to a commit that no longer exists.  Update the submodule to a later commit.  See [this documentation](https://git-scm.com/docs/git-submodule#Documentation/git-submodule.txt-update--init--remote-N--no-fetch--no-recommend-shallow-f--force--checkout--rebase--merge--referenceltrepositorygt--depthltdepthgt--recursive--jobsltngt--no-single-branch--ltpathgt82308203).  For example, see [this article](https://stackoverflow.com/questions/5828324/update-git-submodule-to-latest-commit-on-origin).
