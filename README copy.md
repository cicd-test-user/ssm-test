ansible-test
============

## Setup ansible

### Install asdf

https://asdf-vm.com/guide/getting-started.html

### Setup python and ansible

```bash
asdf plugin add python
asdf install
pip install -r requirements.txt
asdf reshim python
```

```bash
# Using Zscaler
pip install -r requirements.txt --proxy http://185.46.212.88:443
```

> See: https://nttdataitm.service-now.com/infogrid?id=kb_article_view&table=kb_knowledge&sysparm_article=KB0072342


```bash
ansible --version
ansible [core 2.18.5]
  config file = None
  configured module search path = ['/home/ubuntu/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /home/ubuntu/.asdf/installs/python/3.13.3/lib/python3.13/site-packages/ansible
  ansible collection location = /home/ubuntu/.ansible/collections:/usr/share/ansible/collections
  executable location = /home/ubuntu/.asdf/installs/python/3.13.3/bin/ansible
  python version = 3.13.3 (main, Apr 24 2025, 08:45:45) [GCC 13.3.0] (/home/ubuntu/.asdf/installs/python/3.13.3/bin/python3.13)
  jinja version = 3.1.6
  libyaml = True
```

## Install collections and roles

```bash
ansible-galaxy install -r requirements.yaml
```

```bash
# If some SSL error occurs
ansible-galaxy install -r requirements.yaml --ignore-certs
```

## Get hosts using EC2 dynamic inventory

```bash
ansible-inventory -i inventories/poc/aws_ec2.yaml --list
{
    "_meta": {
        "hostvars": {
            "sakamotoy-ec2-instance-bastion001": {

    <-- snip -->

    "all": {
        "children": [
            "ungrouped",
            "aws_ec2",
            "poc",
            "bastion"
        ]
    },
    "aws_ec2": {
        "hosts": [
            "sakamotoy-ec2-instance-bastion001"
        ]
    },
    "bastion": {
        "hosts": [
            "sakamotoy-ec2-instance-bastion001"
        ]
    },
    "poc": {
        "hosts": [
            "sakamotoy-ec2-instance-bastion001"
        ]
    }
}
```

