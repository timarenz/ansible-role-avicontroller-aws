# timarenz.avicontroller-aws
Ansible role to deploy a single Avi Networks Controller on AWS

## Requirements
- boto
- boto3
- botocore
- python >= 2.6

## Installation
To install this Ansible module, please issue the command below in your Ansible roles directory.

`git clone https://github.com/timarenz/ansible-role-avicontroller-aws.git timarenz.avicontroller-aws`

## Role variables

### environment_name
This variable will be used to identify the environment and to pre/(ap)pend objects created in AWS.
### environment_state
Specifies the state of the environment. Analog to the state parameter. Default value is "present"
### avicontroller_ami_id
Can be used to specify a specific AMI id for the Avi Controller. If not specified the latest version will be used.
### avicontroller_instance_type
By default the Avi Controller will be created using an instance type of "m4.2xlarge"
### avicontroller_password
Passsword for the Avi Controller admin account.
### avicontroller_public_key
Public ssh key to access the Avi Controller instance.
### avicontroller_subnet_id
Subnet id of the AWS subnet the Avi Controller should be connected to
### avicontroller_vpc_id
VPC id of the AWS VPC the Avi Controller should be created in

## Dependencies
None 

## Example Playbook

    ---
    - hosts: localhost
      connection: local
      gather_facts: False
      vars:
        environment_name: "tim-staging"
        environment_state: "present"
      tasks:
      - include_role:
          name: timarenz.avicontroller-aws
        vars:
          avicontroller_vpc_id: "{{ vpc_id }}"
          avicontroller_subnet_id: "{{ vpc_public_subnet_id }}"
          avicontroller_password: "MyPassword"
          avicontroller_public_key: "{{ lookup('file', 'avi.key.pub') }}"

# License
[MIT](LICENSE)

# Author Information
[Tim Arenz](https://github.com/timarenz)