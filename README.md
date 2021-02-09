**Repository to hold various wrappers/libraries/packages to be used as aws lambda layers**

### **How to create a lambda layer**

- Create a new directory for the new library/packages (let's say `xxx`) and `cd` into it.

- Create a new serverless project by running `serverless create --template aws-python3`

- Create a folder structure as follows, 

  ```
  └── xxx
        └── python
            └── lib
                └── python3.8
                    └── site-packages
  ```
  and `cd` into `site-packages` directory.

- `pip` install `xxx` as, `pip3 install xxx -t .` *by passing in `-t` parameter we specify where we want to install the libraries (the target directory) on our local folder.* **This is important**

- Go up and be in the same direcoty as the `serverless.yml`

- Update the `serverless.yml` as follows,

  ```
  service: awsLayer-xxx

  provider:
    name: aws
    runtime: python3.8
    profile: default # or the custom profile name 
    region: us-east-2
    stage: ${opt:stage, 'prod'}

  layers:
    xxx:
      name: xxx
      path: xxx/
      description: Description for XXX
      compatibleRuntimes:
        - python3.8
  ```
  
- Delete the `handler.py` file that default created.

- Then do `serverless deploy`

***

* To use this newly created lambda layer in your main serverless project, add this layer `arn` to the function of the the project `serverless.yml` as, 

  ```
    layers:
      - arn:aws:lambda:us-east-2:OMITTED:layer:xxx:1
  ```
  
