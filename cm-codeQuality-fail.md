# Execution fails at codeQuality
[Official documentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#code-quality-testing) about the Code Quality tests.

1. Only critical tests cannot be bypassed by a [Program Manager, Deployment Manager, or Business Owner approval](https://www.adobe.com/go/aem_cloud_mrg_usersroles_en).
   The only critical test in the "Code Quality" step, is the ["Security Rating"](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#code-quality-testing)

2. See [here for how to deal with false positives](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#dealing-with-false-positives)

2. Otherwise, as a last resort you can ignore the code quality violations:
   1.  The [```<sonar.exclusions>``` element](https://stackoverflow.com/questions/21425012/configure-sonar-to-exclude-files-from-maven-pom-xml) can be added to the pom.xml to bypass code quality failures that are false positives or deemed insignificant.
       Example to exclude certain code from checking: 
       ```
       <properties>
         <sonar.exclusions>**/org/my/custom/code/package/**/*</sonar.exclusions>
       </properties>
       ``` 
   2. If you want to ignore specific rules it should be possible with `sonar-project.properties` see [here](https://www.baeldung.com/sonar-exclude-violations)

   3. It can also be done with attributes in the code. For example: `@SuppressWarnings("squid:S0016")`


\[1] https://stackoverflow.com/questions/39109228/how-can-we-ignore-some-sonarqube-rules-in-java

\[2] https://www.baeldung.com/sonar-exclude-violations

