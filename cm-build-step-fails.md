## build step fails in Cloud Manager but not on local maven build

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
