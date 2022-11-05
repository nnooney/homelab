# hashicorp-common

A collection of common tasks used by other `hashicorp` roles.

## Requirements

None

## Role Variables

None

## Dependencies

None

## Example Role

Each file in `tasks` contains useful chunks of functionality to include in
another role. Use the module `ansible.builtin.include_role` to include tasks
like in the example below.

```yaml
- name: Run tasks/add_repository.yml
  ansible.builtin.include_role:
    name: hashicorp-common
    tasks_from: add_repository
  vars:
    rolevar1: value from task
  when: ...
```

## License

Apache 2.0
