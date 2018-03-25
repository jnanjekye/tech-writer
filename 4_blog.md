---
Title: "Continuous integration checklist"
Subtitle: "Uploading files to AWS S3 with Rails, BDD with Cucumber and Continous Intergration with Semaphore"
Author: "Joannah Nanjekye"
Web: "nanjekyejoannah.github.io"
Date: "March 24, 2018"
output: html_document
---

![Alt](images/checklist-150938_1280.png "image from google search on checklist images")

Continuous Integration (CI) is a practice in software development where developers are required to integrate their source code into a single shared repository frequently this is typically several times a day. Every commit is then checked by an automated build which allows the team to get notified of problems as early as possible and easily.

Continuous Integration (CI) is much more than quick routine thrown together to just fullfil another ritual in the organisation. To get all the benefits of continous Integeration, some best practices need to be ensured.

It is hard to discuss Continuous Integration and Continous Delivery without mentioning some of the contributions of people like Martin Fowler , Jez Humble etc. Aravind Dhakshinamoorthy [created a list of items to act as a checklist](https://www.linkedin.com/pulse/checklist-continuous-integration-automation-aravind-dhakshinamoorthy/) for anyone implementing Continuous Integration for any project. In an article entitled "Checklist for Continuous Integration and Automation Deployment", Aravind Dhakshinamoorthy notes the following items.

    Build per check-in: For every code which is checked into the source code repository, the build process should kick in to generate the artifact.

    Poll configuration: CI server has to be configured to poll the source code repository on a frequent interval (lets say every 3 minutes) to look for a change.

    Push configuration: Alternatively, configuration can be done at source code repository to push a notification to the CI server when a new code is checked in.

    Gated check-in: Gated check-in should be leveraged when necessary which gives the flexibility to create a Shelve-set, build the changes for validation before code is checked in.

    Regular Build: CI server should be configured in such a way to take only the latest changes (just the updates), rather than the entire repository for building the artifact. 

    Full build: Additional option should be configured in CI environment to trigger a full build as well where the local repository in CI server can be cleaned up and the entire code base will be downloaded newly for building the artifact. This can be triggered on need basis and when the local repository is corrupted for some reasons.
    Versioning: It's a good practice to version the package files (.jar files for java, .dll files for .net) either using the source repository check-in revision # or using build # from CI job.

    Artifact Upload: Every successful artifact generated out from the build process has to be uploaded into a repository for future deployment process. Team can decide to go with third party repository management tools like Nexus or to leverage cloud storage to store artifacts to store the builds. It's always a good practice to store the artifacts outside of the CI servers instead of storing in the same CI server itself. 

    Server side tests execution configuration: Based on the language the application and unit tests are written, choose the appropriate plug-in to execute the server side unit tests. For example, while using TFS it comes with support of MSTest to execute the test cases in C#. For the same tests when running in Jenkins, we need to configure explicitly in Jenkins with the local path of MSTest.exe, for some languages we may have to install the necessary third party plug-ins too.

    Client side tests execution configuration: Similar to setting up the server side test execution tool in CI environment, configuration has to be done to run the client side test cases. For eg: if the team is using Jasmine framework to execute JavaScript test cases with the support of PhatomJS for headless browser support, we have to explicitly configure in CI for PhatomJS to execute the JS test cases built using Jasmine.

    Segregation of jobs: The jobs have to be segregated in the CI environment in such as way the long running tests can be scheduled to run on a nightly basis rather than running it immediately for every check-in. For example, a) if the user interface test suite built using Selenium runs longer time to execute, then it has to be configured to run nightly. b) if the performance tests needs to be executed which involves cost and time to complete, it has to be configured to run on need basis.

    Execution of test cases: After the code is checked in, the regular job should execute all the client + server side test cases and capture the test results in CI environment which should be available for every developer to review. 

    Code metrics / Reporting: Once the tool to capture code quality and reporting is identified, the same has to be configured in CI environment as a build step. Code metrics capturing tool has to be configured to capture the static code analysis results and the code coverage for every execution. For eg. If we are using SonarQube for reporting code quality of .net applications, then FxCop has to be configured in SonarQube to evaluate the static code analysis.

    Email Notification: Email notification has to be configured in CI server with SMTP server. If the build has failed for any reasons, email has to be sent to the developer who has broken the build with the details of the exception. It's developers responsibility to fix the code and check-in the change and bring the build back into normal state. 

    Automation Deployment: This should be configured as the last step in the build process. Automation deployment tool of choice to be configured in CI environment to trigger with the latest artifact. With the latest artifact, it has to be deployed into integration environment (or development environment) automatically for developer testing before the build is deployed to QA environments.

Once you can take care of the above, then you are sure the  Continuous Integration  pipeline implemented will yield fruit. Another thing you can ensure is that the whole CI process runs faster. This can depend on the tool you are using for your CI process. Semaphore is a hosted CI service that automatically parallelizes your test runs so that the time it takes for your developers to get results back from the process is shorter for better productivity. Check out [semaphore Boosters](https://semaphoreci.com/product/boosters) to get more out of your CI pipeline.


