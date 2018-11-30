# Empty Aws Cloudformation project

# Usage
* Create a new project folder
* Download this repo without cloning

  ```
  curl -L -o master.zip https://github.com/phcyso/empty_cloudformation_project/archive/master.zip
  unzip master.zip
  rm -f master.zip
  mv empty_cloudformation_project-master/* ./
  rmdir empty_cloudformation_project-master
  ```
* Unzip it into your project folder
* Remove any bits that are unneeded


# Helpful snippets for use in Aws Cloudformation templates

## Cfn init helpers

### Load param from param store into a file
```
SECRET_FILE=/etc/blah/secret/file
aws --region "$AWS_REGION" ssm get-parameter --with-decryption --name /path/to/secret/value --output text --query 'Parameter.Value' > /etc/mongo/keyfile
chown user:user ${SECRET_FILE}
chmod 0600 ${SECRET_FILE}
```

### Load param from param store into a variable and use sed to put in into a file
```
SECRET_FILE=/etc/blah/secret/file
SECRET_PASSWORD="$(aws --region "$AWS_REGION" ssm get-parameter --with-decryption --name /mongo/ops-manager/mongopassword --output text --query 'Parameter.Value')"

sed -i 's/^SecretPassword=.*//g' ${SECRET_FILE}
echo "SecretPassword=${SECRET_PASSWORD}" >> ${SECRET_FILE}
```
