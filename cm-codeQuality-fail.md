# Execution fails at codeQuality
[Official documentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#code-quality-testing) about the Code Quality tests.

1. Only critical tests cannot be bypassed by a [Program Manager, Deployment Manager, or Business Owner approval](https://www.adobe.com/go/aem_cloud_mrg_usersroles_en).
   The only critical test in the "Code Quality" step, is the ["Security Rating"](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#code-quality-testing)

2. See [here for how to deal with false positives](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#dealing-with-false-positives)

3. Otherwise, as a last resort, you can ignore the code quality violations with attributes in the code. For example: `@SuppressWarnings("squid:S0016")`

Note, other types of excludes defined in the maven pom files such as `<sonar.exclusions>` (and others documented in \[1] and \[2]) get automatically removed, so they will not work.

\[1] https://stackoverflow.com/questions/39109228/how-can-we-ignore-some-sonarqube-rules-in-java

\[2] https://www.baeldung.com/sonar-exclude-violations

