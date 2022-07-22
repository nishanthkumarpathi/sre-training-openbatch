# Terraform AWS Setup

To use your IAM credentials to authenticate the Terraform AWS provider, set the `AWS_ACCESS_KEY_ID` environment variable.

```shell-session
export AWS_ACCESS_KEY_ID=
```

Now, set your secret key.

```shell-session
export AWS_SECRET_ACCESS_KEY=
```

Alternatvely you can use the following command

```
aws configure
```
