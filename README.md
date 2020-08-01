**Repository to hold various wrappers/libraries/packages to be used as aws lambda layers**

### **How to create a lambda layer**

- Create a new directory for the new library/packages (let's say `xxx`) and `cd` into it.

- Create a folder structure as follows, 

  ```
  └── lambda_layers
        └── python
            └── lib
                └── python3.8
                    └── site-packages
  ```
  and `cd` into `site-packages` directory.

- Create a new serverless project by running `serverless create --template aws-python3`

- `pip` install `xxx` as, `pip3 install xxx -t .` *by passing in `-t` parameter we specify where we want to install the libraries (the target directory) on our local folder.* **This is important**

- Update the `serverless.yml` as follows,

  ```
  service: awsLayer-xxx

  provider:
    name: aws
    runtime: python3.8
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
      - arn:aws:lambda:us-east-2:OMITTED:layer:xxx:9
  ```
  
