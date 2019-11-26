# ansible playbooks and ad-hoc commands
To remember:
- ansible does not respect sudoers, you should be allowed all commands to use become
- ansible cannot change password with no sudo

## ansible ad-hoc commands
### ansible change password for another user_name with user_in_sudoers (should be in sudoers)
`ansible all [-i inventory_file] [-l host_name] -m user -a "name=user_name update_password=always password={{ 'your_password' | password_hash('sha512', rounds=10000) }}" [-u user_in_sudoers] --become -KD`

### ansible manage systemd service, should be a superuser (in sudoers), sometimes state do not work for me, so I use shell module to restart service
`ansible all [-i inventory_file] [-l host_name] -m systemd -a "name=service_name state=[reloaded,restarted,started,stopped]" -u user_name --become -KD`

### ansible manage systemd service using shell module, should be a superuser (in sudoers)
`ansible all [-i inventory_file] [-l host_name] -m shell -a "systemctl [start,stop,restart] service_name.service" -u user_name --become -KD`

## ansible playbooks
### ansible playbook add, change password, add or remove ssh key for linux users. All variables should be defined in users_var/username.yml
`ansible-playbook manage_user.yml [-i inventory] [-l hosts] [--tags add_user,change_password,ssh,ssh_remove] -KD`

### ansible playbook to change user password on linux
`ansible-playbook change_password.yml [-i inventory] [-l hosts] -KD`
