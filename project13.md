## dynamic assignments branch in ansible-config-mgt github repo

created a new folder called dynamic assignment to store the env-vars.yml file in.

created an env-vars folder also to store all related environment variable files in.

this is what the file layout looks like:

![](images/layoutlook1.png)

added the following yaml script in the dynamic-assignments/env-vars.yml file:

![](images/dynamicassgenvvars.png)

## ansible galaxy and installing specific ansible roles

preserving github repo in its actual state and pushing codes directly to master branch from jenkins-ansible server without needing webhook.

`$ git init`

`$ git pull https://github.com/demiladee/ansible-config-mgt.git`

`$ git remote add origin https://github.com/demiladee/ansible-config-mgt.git`

`$ git branch roles-feature`

`$ git switch roles-feature`

![](images/ansibleconfigmgttorolesfeatureswitch1.png)

installed geerlingguy's mysql role inside the roles directory

`$ cd roles`

`$ ansible-galaxy install geerlingguy.mysql`

changed geerlingguy.mysql to mysql

`$ mv geerlingguy.mysql/ mysql`

![](images/rolesgeerlinguy2.png)

edited the roles configuration files to use correct credentials for mysql required for the tooling website and pushed to github

![](images/mysqldefaultsmain.png)

![](images/staticassgndbyml.png)

`$ git add .`

`$ git commit -m 'commit messaage'`

`$ git push --set-upstream origin roles-feature`

checked out into the folder that has the main branch and merged them

` $ cd ..`

`$ git checkout main`

` git merge dynamic assignment`

![](images/readmeedit3.png)

## load balancer roles

creating two load balancers, apache x nginx, to use interchangeably.

`$ ansible-galaxy install geerlingguy.nginx`

`$ mv geerlingguy.nginx/ nginx`

`$ ansible-galaxy install geerlingguy.apache`

`$mv geerlingguy.apache/ apache`

![](images/nginxandapacheroles4.png)

editing apache and nginx's role configuration file to serve the purpose needed.

declared variables in defaults/main.yml file of nginx and apache roles.

![](images/apachedefaultsmain.png)

![](images/nginxdefaultsmain.png)

updating lb.yml and site.yml with the loadbalancer information

![](images/staticassgnlbyml.png)

![](images/playbookssite.png)

updating inventory/uat.yml with the lb ip addresses

![](images/inventoryuatyml.png)

updating env-vars/uat.yml to enable apache loadbalancer

![](images/envvarsapache.png)

running apache play

`$ ansible-playbook -i inventory/uat.yml playbooks/site.yml`

![](images/ansibleplayapache.png)

![](images/ansibleplayapache2.png)

![](images/ansibleplayapache3.png)

![](images/ansibleplayapache4.png)

additional nginx configuration before running play

![](images/nginxtaskmain.png)

![](images/nginxtemplatesconf.png)

running nginx play

`$ ansible-playbook -i inventory/uat.yml playbooks/site.yml`

![](images/ansibleplaynginx.png)

![](images/ansibleplaynginx2.png)

![](images/ansibleplaynginx3.png)

![](images/ansibleplaynginx4.png)