```
---
- hosts: localhost
  tasks:
  - name: 1 Good Task
    command: which tree
    register: command_output

  - name: 2 Check command output
    debug:
      msg: "{{ command_output.stdout }}"
  ```
  If the task failes install tree package and re run 
  
  How to install tree package?
```
  sudo apt-get install tree
```
  
# Run play on all hosts 
  Change the hosts to all and re run the playbook 
  Notice careful th eresults 
  
 ![image](https://user-images.githubusercontent.com/78414554/216779169-52dc6ee3-a2aa-4b11-bb4a-85aa599a8296.png)

```  
  ---
- hosts: all
  tasks:
  - name: 1 Good Task
    command: which tree
    register: command_output

  - name: 2 Check command output
    debug:
      msg: "{{ command_output.stdout }}"
```
  output : watch play recap section 
```
  PLAY RECAP *************************************************************************************************************
172.31.56.202              : ok=1    changed=0    unreachable=0    failed=1    skipped=0    rescued=0    ignored=0   
172.31.58.111              : ok=1    changed=0    unreachable=0    failed=1    skipped=0    rescued=0    ignored=0   
localhost                  : ok=3    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

```
  
# Watch individuak tasks
```
  PLAY [all] *************************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************
ok: [172.31.56.202]
ok: [172.31.58.111]
ok: [localhost]

TASK [1 Good Task] *****************************************************************************************************
fatal: [172.31.56.202]: FAILED! => {"changed": true, "cmd": ["which", "tree"], "delta": "0:00:00.002610", "end": "2023-02-04 15:42:38.496030", "msg": "non-zero return code", "rc": 1, "start": "2023-02-04 15:42:38.493420", "stderr": "", "stderr_lines": [], "stdout": "", "stdout_lines": []}
fatal: [172.31.58.111]: FAILED! => {"changed": true, "cmd": ["which", "tree"], "delta": "0:00:00.002757", "end": "2023-02-04 15:42:38.504801", "msg": "non-zero return code", "rc": 1, "start": "2023-02-04 15:42:38.502044", "stderr": "", "stderr_lines": [], "stdout": "", "stdout_lines": []}
changed: [localhost]

TASK [2 Check command output] ******************************************************************************************
ok: [localhost] => {
    "msg": "/usr/bin/tree"
}
```

![image](https://user-images.githubusercontent.com/78414554/216778275-37a15cc2-12b7-43a7-9450-4ed688d1e084.png)

# Error handling 
code 
```
#checks if  package (tree) is installed 
# if any tasks fail in any of server just exit 
---
- hosts: all 
  any_errors_fatal: true 
  tasks: 
  - name: Check if package is installed 
    command: which tree
    register: command_output
  - name: check what is in output 
    debug: 
      msg: " {{ command_output }}"

```

# 5
![image](https://user-images.githubusercontent.com/78414554/216779451-56ea278b-cc66-4924-a5cf-ea3639014e83.png)

```
#checks if  package (tree) is installed 
# if any tasks fail in any of server just exit 
---
- hosts: all 
  any_errors_fatal: true 
  tasks: 
  - name: Check if package is installed 
    command: which tree
    register: command_output
  - name: check what is in output 
    debug: 
      msg: " {{ command_output }}"
```

# 6 
![image](https://user-images.githubusercontent.com/78414554/216779467-4b865118-aaa4-46ca-bbef-36a075170381.png)

```
#checks if  package (tree) is installed 
# if any tasks fail in any of server dont just exit but ignore 
---
- hosts: all 
  any_errors_fatal: true 
  tasks: 
  - name: Check if package is installed 
    command: which tree
    register: command_output
    ignore_errors: yes
  - name: check what is in output 
    debug: 
      msg: " {{ command_output }}"
```

