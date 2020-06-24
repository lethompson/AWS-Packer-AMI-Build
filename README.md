# AWS Packer AMI Build

* Provide example for creating AWS AMIs with packer.
* Details about packer, visit http://packer.io

### Install Packer
```
navigate to the website, https://www.packer.io/downloads.html
click on OS option, for this demo click Linux
```
### Instructions to install Packer on Linux OS (ubuntu)
```
> wget https://releases.hashicorp.com/packer/1.6.0/packer_1.6.0_linux_amd64.zip 

> unzip packer_1.6.0_linux_amd64.zip

> sudo mv packer /usr/local/bin

> packer (enter, to test if packer is installed)
```

### Setup files for Packer
```
> touch example.json provision.sh

.
├── example.json
└── provision.sh

0 directories, 2 files

```

#### example.json
```
{
  "variables": {
    "aws_access_key": "",
    "aws_secret_key": ""
  },
  "builders": [
    {
      "type": "amazon-ebs",
      "access_key": "{{user `aws_access_key`}}",
      "secret_key": "{{user `aws_secret_key`}}",
      "region": "us-east-1",
      "source_ami": "ami-04169656fea786776",
      "instance_type": "t2.micro",
      "ssh_username": "ubuntu",
      "ami_name": "packer-apache-aws-example {{timestamp}}"
    }
  ],
  "provisioners": [
    {
      "type": "shell",
      "script": "provision.sh"
    }
  ]
}
```

### provision.sh (shell script to install git, apache & update libraries)
```
#!/usr/bin/env bash

set -e

sudo apt-get -y update
sudo apt-get install apache2 -y
sudo apt-get install unzip -y
sudo apt-get install git -y
```
