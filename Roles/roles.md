Ansible role is an independent component that allows reuse of common
configuration steps.Roles provide a framework for fully independent or interdependent collections
of variables, tasks, files, templates, and modules.

Roles are not playbooks. They are small functions that can be used individually
within the playbooks.
Each role is a directory tree in itself. So, the role name is the directory name within
the /roles directory.

A role directory structure contains the following directories: defaults, vars,
tasks, files, templates, meta, and handlers.
Each directory must contain a main.yml file that contains relevant
content.