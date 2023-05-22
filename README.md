# README
The following test requires you do containerize a sample ruby app and deploy to production. Commands in the Dockerfile should be explained thoroughly.
You may use inline comments on the Dockerfile, or simply provide a txt file discussing your implementation.

# Test 1
Create a dockerfile to dockerize the sample ruby app for development usage, you may ignore handling the database.

# Test 2
Produce another dockerfile for production deployment. How would you improve it to make it production ready?

# Test 3
Discuss how you would deploy the app on production using Kubernetes. Some topics to cover including:
- Describe the high level flow for pushing new code out
  - How would a privileged developer trigger the deploy
  - What system will be used for building the containers
  - Strategy for tagging the container images
  - How are Kubernetes deployment.yml files updated
  - How would your system authenticate with the cluster
  - How to track the status of a deploy, whether successful or otherwise.
- What other containers or components may be required in a production Rails app. Explain the strategies for linking other containers or services together.
- Discuss how code deployments can be performed gracefully. E.g. when there are schema changes to the database, or when the asset (Javascripts, images, etc) filenames differ after asset compilation.

Some of the topics suggested cannot be easily explained in a short report. Where suitable, a high level summary will suffice and may be discussed further during the interview.

