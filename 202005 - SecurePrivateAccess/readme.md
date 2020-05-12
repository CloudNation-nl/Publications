# Secure private access
This folder contains a cloudformation template which can be used to deploy a bastion host to a private subnet. This bastion host
can be used with EC2 instance connect and Session manager. 

After deploying the cloudformation stack to your account, set up you can connect to this host using SSM.

To simplify this setup, you can use AWS Gate: https://github.com/xen0l/aws-gate

Assuming you have python 3.X installed, you set up your workstation using the following commands
```
pip install aws-gate

# Bootstrap only works on MacOs. For windows, check https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager-working-with-install-plugin.html
aws-gate bootstrap  

# List available instances

aws-gate list -p <profile name> -r <region>
```

And then set up a tunnel using the following commands

```
aws-gate ssh-config -p <profile name> -r <region>

ssh <instance-id>.<region>.<profile name> -L 127.0.0.1:<source port>:<destination host>:<destination port> -N

```

