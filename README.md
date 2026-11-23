# Ansible Windows Automation

Template repository to help kickstart windows automation using Ansible.

```shell
# Install system package dependencies
sudo dnf install $(cat bindep.txt)
# Install python dependencies
pip install -r requirements.txt
# Install collection dependencies
ansible-galaxy collection install -r collections/requirements.yml

# Edit inventory file and ensure variables; domain has to be uppercase
vi hosts/inventory

# Test playbook
ansible-playbook -i hosts/inventory playbooks/example.yml
```

## Example Kerberos Config

As an example of a valid Kerberos configuration file, you can generate one using this script:

```shell
# Install python kerberos, for authentication
pip install -r requirements.txt

# Create a file and specify Windows AD domains you are going to authenticate against
export GUID=`hostname | awk -F"." '{print $2}'`
export GUID_CAP=`echo ${GUID} | tr 'a-z' 'A-Z'`
cat << EOF > /etc/krb5.conf.d/ansible.conf

[realms]

 AD1.${GUID_CAP}.EXAMPLE.OPENTLC.COM = {

 kdc = ad1.${GUID}.example.opentlc.com
 }

[domain_realm]
 .ad1.${GUID}.example.opentlc.com = AD1.${GUID_CAP}.EXAMPLE.OPENTLC.COM
EOF

# Verify that you are able to authenticate as Administrator, the password is available in the /etc/ansible/hosts file
kinit administrator@AD1.${GUID_CAP}.EXAMPLE.OPENTLC.COM
klist
```

## Author

John Wadleigh

## Links

- [3 Ways to Install Ansible on Windows](https://www.automatesql.com/blog/3-ways-to-install-ansible-on-windows)