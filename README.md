# ansible_repo Public

This repo has the roles developed by me.
I'm happy to share some code and I really hope that it will save some time for those who is looking for something similar.

Repo has the following roles, playbooks:

* check_failed_tasks (Role)
* cisco_enable_ssh (playbook)
* cisco_os_upgrade (playbook)

check_failed_tasks Role
=========
This Role is about extracting the Job IDs with the status 'failed' as well as with 'job_explanation' != null from AWX in order to track such statuses and update status correctly in the microservice DB

Procedure will extract JobID of the sessions and send status 'FAILED' to microservice API endpoint as well as the message='Job terminated due to timeout by AWX'.

Example Playbook
----------------
```
- name: check_failed_tasks role
  hosts: all
  gather_facts: no
  vars:
  roles:
    - check_failed_tasks
```

These two playbooks where developed for simplifying Cisco devices management.
The following playbooks are running by Jenkins job and AWX plugin used there to put the task on directly to AWX for one or another playbooks.

```
* cisco_enable_ssh
* cisco_os_upgrade
```


Thanks,
Yury