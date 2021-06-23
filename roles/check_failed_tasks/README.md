check_failed_tasks role
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