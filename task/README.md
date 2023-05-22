# Explanation of my work .
## For Test 1 and 2
In fact we can have only one Dockerfile that's enough, Because we can use ansible to render that file as a template to get the PROD and NONPROD dockerfile. We can simply use command with a variable `rails_env` .

```console
ansible-playbook ansible-render.yaml -e rails_env=production
```

## For Test 3
### How would a privileged developer trigger the deploy
- For deveoper i recommend to use Github-action to deploy non-prod evrionment component with a simple workflow , it has a UI you can fill the variables in and trigger it by a click . All of the variables can be configured by ansible-playbook. it's high flexible. You can check here for an example.
https://github.com/guinan34/Piktochart-Test/actions/workflows/deploy.yml
</br>
Click `Deploy rail-app ...` on the left ,and click `run workflow` on the right .

### What system will be used for building the containers
- Same as above, use github-action is the most convenient way, just need a workflow to trigger it . see `https://github.com/guinan34/Piktochart-Test/actions`

### Strategy for tagging the container images
- In github action we have multiple ways to tag images, such as use branch name , commit hash. Refer to https://docs.github.com/en/actions/publishing-packages/publishing-docker-images
- I have example of use branch name as the tags, you can see it here https://hub.docker.com/repository/docker/66418500/piktochart/tags?page=1&ordering=last_updated

### How are Kubernetes deployment.yml files updated
- same,use github-action and ansible-playbook,we just need a deployment template file,and set some key value as variables. Pass the variable through github-action UI, and the ansible will render to the right deployment file and deploy it in kubernetes. We can simply configure context of k8s in Github ,then we can use it through action.

### How would your system authenticate with the cluster
- Configure its context in github as a varible, then use `Azure/k8s-set-context@v1` module to set it in runner server. But only suggestion use NON-PROD environment in github.
- For PROD environment, we can have a server with whitelist then use ansible-playbook to deploy it . or use a jump tool such as Teleport.

### How to track the status of a deploy, whether successful or otherwise.
- For NON-PROD configured in github, `Azure/k8s-deploy@v4` module can show the status of the deploy.
- For PROD configured in server , we can use ansible module to get the status.

### What other containers or components may be required in a production Rails app. Explain the strategies for linking other containers or services together.
- In Kubernetes , we can simply use service name to call each other, since they are in a same network layer in k8s.
- In Docker, we can set them in one same network layer, and use their name to call each other.

### Discuss how code deployments can be performed gracefully. E.g. when there are schema changes to the database, or when the asset (Javascripts, images, etc) filenames differ after asset compilation.
- We can use same Dockerfile but with another command to perform fot fix, set it as a job in k8s. It only performs once. 
- For regular update, also use github-action build process to build and push the image automatically .






