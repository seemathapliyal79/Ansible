Create simple playbook with one task
Task runs command and exits

---
- hosts: localhost 
  tasks: 
  - name: Check if tree is available
    command: date
Learn to use register
You will capture command output in a variable using register

---
- hosts: localhost 
 tasks: 
 - name: Good Task 
   command: date
   register: command_output
How to read variable value or check command output in this case
---
- hosts: localhost 
  tasks: 
  - name: Good Task 
    command: date
    register: command_output
  
  - name: Check command output 
    debug: 
      msg: {{ command_output }}