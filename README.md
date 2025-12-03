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

## Author

John Wadleigh

## Links

- [3 Ways to Install Ansible on Windows](https://www.automatesql.com/blog/3-ways-to-install-ansible-on-windows)