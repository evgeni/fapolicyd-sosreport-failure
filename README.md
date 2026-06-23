# fapolicyd 1.6 crash when running sos report

1. `vagrant up quadlet`
2. `./vagrant.py --yaml > inventories/vagrant`
3. `ansible-playbook -i inventories/ fapolicyd.yaml`
4. `ansible-playbook -i inventories/ sos.yaml`

```
PLAY [all] ****************************************************************************************

TASK [Gathering Facts] ****************************************************************************
[WARNING]: Host 'quadlet' is using the discovered Python interpreter at '/usr/bin/python3.9', but future installation of another Python interpreter could cause a different interpreter to be discovered. See https://docs.ansible.com/ansible-core/2.20/reference_appendices/interpreter_discovery.html for more information.
ok: [quadlet]

TASK [install sos] ********************************************************************************
changed: [quadlet]

TASK [Generate sosreport] *************************************************************************
[WARNING]: Module invocation had junk after the JSON data: /bin/sh: line 1: /usr/bin/sleep: Operation not permitted
[WARNING]: Error deleting remote temporary files (rc: 1, stderr: /bin/bash: Operation not permitted
})

changed: [quadlet]

TASK [Find sosreport file] ************************************************************************
[ERROR]: Task failed: Failed to create temporary directory. In some cases, you may have been able to authenticate and did not have permissions on the target directory. Consider changing the remote tmp path in ansible.cfg to a path rooted in "/tmp", for more error information use -vvv. Failed command was: ( umask 77 && mkdir -p "` echo ~/.ansible/tmp `"&& mkdir "` echo ~/.ansible/tmp/ansible-tmp-1782226406.6366792-2710980-43111554034392 `" && echo ansible-tmp-1782226406.6366792-2710980-43111554034392="` echo ~/.ansible/tmp/ansible-tmp-1782226406.6366792-2710980-43111554034392 `" ), exited with result 1
Origin: /home/evgeni/Devel/fapolicyd-sosreport-failure/sos.yaml:14:7

12       ignore_errors: true
13
14     - name: 'Find sosreport file'
         ^ column 7

fatal: [quadlet]: UNREACHABLE! => {"changed": false, "msg": "Task failed: Failed to create temporary directory. In some cases, you may have been able to authenticate and did not have permissions on the target directory. Consider changing the remote tmp path in ansible.cfg to a path rooted in \"/tmp\", for more error information use -vvv. Failed command was: ( umask 77 && mkdir -p \"` echo ~/.ansible/tmp `\"&& mkdir \"` echo ~/.ansible/tmp/ansible-tmp-1782226406.6366792-2710980-43111554034392 `\" && echo ansible-tmp-1782226406.6366792-2710980-43111554034392=\"` echo ~/.ansible/tmp/ansible-tmp-1782226406.6366792-2710980-43111554034392 `\" ), exited with result 1", "unreachable": true}

PLAY RECAP ****************************************************************************************
quadlet                    : ok=3    changed=2    unreachable=1    failed=0    skipped=0    rescued=0    ignored=0   
```
