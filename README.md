***<h1>Ansible Configuration in Linux (Ubuntu)</h1>***
<html>
<h2>Pre-requisites</h2>
<h4>1. Remote or Local Servers with Public IP and Enabled SSH Connection</h4>
<p>We used linux virtual machines on Microsoft Azure</p>
Refer to: https://docs.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-portal
<h4>2. Familiarity with Bash</h4>

<h2>Step 01: Configuring your Master Machine</h2>
<p> 1. Update your machine <code>sudo apt update</code></p>
<p> 2. Add Dependencies <code>sudo apt install software-properties-common</code> </p>
<p> 3. Add Ansible Repo <code>sudo apt-add-repository --yes --update ppa:ansible/ansible </code></p>
<p> 4. Install Ansible <code>sudo apt install ansible</code> (press “y” if asked for confirmation)</p>
<p> 5. Check if installed correctly <code>ansible –version</code></p>
<h2>Step 02: For Password Based Authentication:</h2>
<p>1. Install sshpass <code>sudo apt-get install sshpass</code></p>
<p>2. Navigate to etc/ansible: cd etc/ansible</p>
<p>3. Initialize ansible.cfg: ansible-config init --disabled -t all > ansible.cfg</p>
<p>4. Edit the ansible.cfg file using nano or vi: nano ansible.cfg or vi ansible.cfg</p>
<p>5. change <code>;host_key_checking=true</code> to <code>host_key_checking=false</code> (also uncommenting the file by removing the semicolon) or uncomment the line “#host_key_checking=false” by removing the “#” </p>
<h2>Step 03: Making an inventory </h2>
<p>1. mkdir inventory</p>
<p>2. cd inventory</p>
<p>3. touch hosts</p>
<p>4. vi hosts and enter your hosts public IP Addresses under a group</p>
<mark><p>For Example:</p>
<p></p>
<p>[ubuntu]</p>
<p>20.219.73.195</p>
<p>20.219.88.104</p>
<p>52.140.54.107 ansible_user=USERNAME ansible_password=PASSWORD</p>
<p>[ubuntu:vars]</p>
<p>ansible_user=USERNAME</p>
<p>ansible_password=PASSWORD</p>
</mark>
<p>5.ansible -i <host-file-path> ubuntu –m ping</p>
<p>Example:</p>
<p> ansible -i ./inventory/hosts ubuntu –m ping</p>
<h2>Step 04: Make an inventory</h2>
<p>1. mkdir playbook</p>
<p>2. cd playbook</p>
<p>3. touch <filename>.yml (ex: apt.yml)</p>
<p>4. vi apt.yml and enter your yml playbook</p>
</html>

hosts: "*"

become: yes

tasks:

- name: apt update_cache and upgrade

apt:

update_cache: yes

upgrade: 'yes'








