<H1>Basic of CI/CD</H1>
CI/CD stands for Continuous Integration and Continuous Delivery (or Continuous Devployment). It is a set of automated software engineering practices that let development team build, test, and release code change faster and more reliably. 

<H3>CI (Continuous Integration)</H3>
During the review of a pull request, a automated CI pipeline is triggered. When the CI pipeline is triggered, it runs through several stages, including unit testing, dependency scan, build artifact, and code scanning on both the `newly added code` and code from the  `main` branch. If any of the test fails, the Dev is asked to make adjustments on the code and commit the changes on the same merge request. 

The CI pipeline is triggered again and if the code pass the tests, it is then approved and merge into the main branch. After the code is merged with the main branch, the same CI pipeline or another CI pipeline with additional steps and tests, is automatically executed to verify the merged code. 

If another Dev commits and sent a pull request on a different branch (B), the CI pipeline is triggered. Afther the code passes the test, it is then merged to the main branch, the CI pipeline is triggered again. This makes sures that the codes from Dev A and B work seamlessly together. This entire process, enables multipe developers to work on the same application while ensurinf that these changes integrate smoothly without introducing any issues, is known as `Continuous Integration`. 

NOTE: 
CI pipeline: When Developers merge their code to the main branch, every merge automatically triggered the CI pipeline. This runs tests to catch bugs, syntax errors or conflicts right away. 

<H3>CD (Continuous Development / Delivery </H3>
After CI and testing procedures, deploy the modified application to a non-production environment that resemble the live enviroment. This allows for live testing before processing with production development.

Following development to a staging or deployment environment, there are series of tests to ensure the quality of the application does not get degraded. 

After successful completion of CD, the merge request is approved and sent to the main branch. Within the main branch, another CI pipeline is triggered and if successful, it triggers the CD pipeline which results in a deployment of the application to the production environment. 

<H3>What is the difference between Continuous Delivery and Continuous Deployment</H3>
For Continuous Delivery, a human is REQUIRED to approve the changes before the sending the code to live production environment.

For Continous Development, there is no human approval at all. The code deploys straight to production automatically. 

NOTE:
After passing the CI pipeline, the CD pipeline is triggered. This runs tests on the code to make sure it running smoothly  on a development / staging environment before going to live production. If there is a human approval for the final push to live development, it is called Continuous Delivery. If there is no human approve and the code does straight to live production, it is called Continous Deployment. 
