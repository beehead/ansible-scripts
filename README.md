# ansible-scripts
## ansible from command prompt
### change password for user_name with your_password on all hosts or host_name:

`ansible all [-i inventory_file] [-l host_name] -m user -a "name=user_name update_password=always password={{ 'your_password' | password_hash('sha512', rounds=10000) }}" -u user_name -kD`

### to change password for another user (yours should be in sudoers)
ansible all [-i inventory_file] [-l host_name] -m user -a "name=user_name update_password=always password={{ 'your_password' | password_hash('sha512', rounds=10000) }}" -u user_in_sudoers --become -KD

### manage systemd service, should be a superuser (in sudoers)
`ansible all [-i inventory_file] [-l host_name] -m shell -a "systemctl [start,stop,restart] service_name.service" -u user_name --become -KD`
