# Easy automated cost control with cloud custodian

This folder contains resources used in the video 'Easy automated cost control' on the CloudNation website.

## Installing cloud custodian
Make sure you have python and pip installed. Run `pip install c7n` to install cloud custodian.
Optionally, install the mailer plugin by running `pip install c7n-mailer`.

You can prepare your AWS environment by running
```
aws cloudformation deploy --stack-name c7n-bootstrap --template-file c7n-bootstrap.yaml --capabilities CAPABILITY_NAMED_IAM --parameter-overrides IncludeC7NMailerSupport=True
```
This deploys a role and SQS queue used by the mailer. 

> NOTE: Make sure to update the `mailer/mailer-config.yaml` and the 'notify' actions in the policies with your SQS queue!

## Creating a policy
Deploying a policy can be done with the command `custodian run -s . <policy name>`.

To deploy a whole folder of policies, first update the mailer configuration and notification action in the policies. Then run
```
custodian run -s . policies/* 
```

This will deploy lambda's in your AWS environment, which automatically shuts down resources.

## Tagging resources
Make sure to tag the resources to be shut down using tags with a key of `offhours:OptIn` and a value of `on`. 
This can also be found in the 'offhours' policy documentation of cloud custodian.

## Further reading
For more information, please visit the documentation at https://cloudcustodian.io/
`