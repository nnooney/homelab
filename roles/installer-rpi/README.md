# installer-rpi

Install and setup a Raspberry Pi for further management.

## Requirements

None

## Role Variables

See `defaults/main.yml`.

## Dependencies

None

## Example Playbook

```yaml
- name: Install Raspberry Pi
  hosts: servers
  remote_user: "{{ pi_remote_user }}"
  become: yes
  vars_prompt:
    - name: pi_remote_user_new_password
      prompt: "new password for user '{{ pi_remote_user }}'"
      private: yes
      confirm: yes
  roles:
    - role: installer-rpi
      vars:
        pi_remote_user_change_password: true
```

## License

Apache 2.0
