**1. Configuration Management**: As there are servers either cloud, on prem; so if we want to do any mandatory installations on servers or any security patches. while end up of writing mutliple scripts we can use ansible, chef, puppet type of tools.\

**2. Is Ansible better than other tools, if so why?** : As we knwo ansible is agnet less, like other tools have master slave architecture or need any agent but ansible doesnt need agnet. The only prerequisite is ansible need a password authentication b/w host and other server to configure ansible. Other imp is having good community like contains pythons and build module very rapidly. We can write script in YAML\

**3. write ansible playbook to install httpd service and get it runnong?**

install_httpd.yml

--- #start yaml
- name: Install and Start Apache HTTP Server\
  hosts: your_target_servers // dedicated target servers\
  become: true  # Run tasks with elevated privileges (sudo)\

  tasks:\
    - name: Install Apache HTTP Server\
      package:\
        name: httpd  # Package name for Apache HTTP Server\
        state: present  # Ensure the package is installed\

    - name: Start Apache service\
      service:\
        name: httpd  # Service name for Apache HTTP Server\
        state: started  # Ensure the service is started\
        enabled: true  # Ensure the service starts on boot\
**run this script**: ansible-playbook -i your_inventory_file install_httpd.yml

**4. ansible real life experience**: we used to shell scripts// real time exp.

**5. Ansible Dynamic Inventory**: lets assume we have 100 Vm in aws, we configures ansible to make some changes in vm. lets take an example of installion of mysql in vm with ansible scripts. later after 1 week the no has grown to 100, then we frequently cant go and see which are new vm and check
mysql is installed. Rather than that we can use this Dynamic Inventory concept. This mainly looks into AWS accunt and look new vm and automatically installed new softwares or security patches. 

**6. Ansible Tower**: Ansible Tower is a web-based interface and automation platform built on top of Ansible, the popular open-source automation tool. It provides a graphical user interface (GUI) and additional features to simplify the management and execution of Ansible playbooks and workflows.
key features are: web base UI, Role base access, Job scheduling, workflow editor, Inventory management, scaling, API Integration. 

**7. Manage RBAC in Ansible tower** : Role based access control; created group for tested; read only view; configure ansible with external identify provider sso ike LDAP. In AWS we can integrate with IAM.

**8. Ansible GAlaxy Command**: Used to bootstrap; this command is used to bootstap the whole stracture.\
command: ansible-galaxy role init kubernetes // these are the files it list:: readme default handlers meta task tests var 

**9. Explain me the structure of ansible playbook using role**: we can use ansible galaxy command to create structure // refer to above question

**10. Handlers in ansible and there use**: Handlers are similar to normal task, they run when they have notify directive. example like creation on nginx, if we want to create on conditional bases then we can call this directive. It is basically know conditional task or task on special notification.

**11. Run a specific task only on windows not on linux vm , is it possbile** : This is a pretty task, and if we want to use run only on windows we can use tags or use environment variable conditional basis to achive this use case. 

**12. Ansible support parrallel execution of task**: Ansible do parallel exec, if there are 5tasks to run on various servers; then ansible runs as task by task on a serial way. Even if we want to run all task at atime then we need to multiple instances of ansilbe. 
if he asks about the statergies here are they:/
1. Linear Strategy (Default): Executes tasks on hosts in the order they are defined in the playbook. Each task is completed on all hosts before moving to the next task.\
   ansible-playbook playbook.yml
2. Free Strategy: Executes tasks concurrently on all hosts. There is no specific order, and tasks on different hosts may overlap.\
   ansible-playbook -e ansible_strategy=free playbook.yml
3. Host-Pinned Strategy: Assigns each host a specific order for task execution. Tasks are executed on hosts in order, but tasks for different hosts can overlap.\
   ansible-playbook -e ansible_strategy=host_pinned playbook.yml
4. Debug Strategy: Used for debugging purposes. Outputs the order in which tasks would be executed without actually executing them.\
   ansible-playbook -e ansible_strategy=debug playbook.yml
5. Batch Strategy:Executes tasks in batches, where each batch completes on all hosts before moving to the next batch. Useful for managing resource-intensive tasks.\
   ansible-playbook -e ansible_strategy=batch -e ansible_batch_size=5 playbook.yml

**13. Protocol to ansible uses to connect to windows vms**: ansible uses vim rm to connect windows and it use ssh to connect linux. 

**14. Can you place them in order of presedence--> playbook group_var,role vars, extra vars** : there are lot of presedence order to store varialbe. gicen order is perfect.\
general precedence order from highest to lowest: 1. Variables defined in the task; 2. Variables defined in the play; 3. Variables defined in included files or roles; 4. Variables defined in inventory; 5. Fact variables:; 6. Variables defined in Ansible configuration files: 7. Variables defined as environment variables (lowest precedence):

**15. handle secret in ansible**: Hashicorp vault; Prompting for Passwords; SSH Key Agents

**16. Can we use ansible for IAC, if yes compare with terraform**: Ansible is a configuration management tool; there is a cross of path like it might do some terraform task but it is a config mangement tool.

**17. Ansible playbook you wrote in company**: installed oracle db in various servers. with this automated creation the time has reduced. i have also installed kubernetes orchestarion. 

**18. Ansible can approve/ downside:**  ansible cannot increase the verbosity(debuggin) on the task: Ansible windows support need to improve: Ansible need to work on IDE or develop plugin:  
