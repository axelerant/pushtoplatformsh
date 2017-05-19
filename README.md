The code in this repository can be used to push a drupal project to platform.sh. The script is configured for usage with gitlab-ci and can be used along with https://github.com/maxc0d3r/docker-platformshcli to allow for execution using autoscalable gitlab runners. However you can change the script to suite your own CI/CD server's variable naming conventions.

# Usage

- Copy the content of this repository to your drupal project's root directory.
- Add a .platform.app.yml, .platform/routes.yaml and .platform/services.yaml to your drupal project's root directory.
-  Create your own gitlab-ci.yml file with content similar to following - 
```
image: XXXX/platformshcli
  
deploy:
  variables:
    PLATFORM_PROJECT_ID: "XXXXXXX"
    PF_PARENT_ENV: "master"
    ALLOW_MASTER: '1'
    
  script:
  - chmod +x ./scripts/push-platform.sh
  - script -q -c "./scripts/push-platform.sh"
  tags:
    - autoscaler
```
Make sure that you've built and pushed the docker image using the code available at https://github.com/maxc0d3r/docker-platformshcli before you decide to use this.
- Commit the code to your gitlab repository. 


