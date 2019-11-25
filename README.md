# ansible playbooks and ad-hoc commands
## ansible ad-hoc commands
### ansible change password for user_name with your_password on all hosts or host_name:
`ansible all [-i inventory_file] [-l host_name] -m user -a "name=user_name update_password=always password={{ 'your_password' | password_hash('sha512', rounds=10000) }}" -u user_name -kD`

### ansible change password for another user_name with user_in_sudoers (should be in sudoers)
`ansible all [-i inventory_file] [-l host_name] -m user -a "name=user_name update_password=always password={{ 'your_password' | password_hash('sha512', rounds=10000) }}" -u user_in_sudoers --become -KD`

### ansible manage systemd service, should be a superuser (in sudoers), sometimes state do not work for me, so I use shell module to restart service
`ansible all [-i inventory_file] [-l host_name] -m systemd -a "name=service_name state=[reloaded,restarted,started,stopped]" -u user_name --become -KD`

### ansible manage systemd service using shell module, should be a superuser (in sudoers)
`ansible all [-i inventory_file] [-l host_name] -m shell -a "systemctl [start,stop,restart] service_name.service" -u user_name --become -KD`
