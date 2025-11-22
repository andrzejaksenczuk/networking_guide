# Overview

This is a template Ansible playbook structure.
It is designed to be the base for new Ansible Playbook projects setting out a folder structure along the lines of Ansible best practices guidelines.

## Precondition

## Important
Please set up proper values of following variables in `ansible/host_vars/localhost.yml` to point to the project and db backup folder:
- `project_src: /home/aak/rep/covitech/workshop_rental/workshop_rental_webapp`
- `backup_dest: /home/aak/rep/covitech/workshop_rental/backups`

### Ubuntu 22.04
 - install `ansible-galaxy collection install community.docker`
 - install ssh server : `sudo apt install openssh-server`
 - add/uncoment ssh with certificate option `sudo nano /etc/ssh/sshd_config` 
   - `PubkeyAuthentication yes`
   - `AuthorizedKeysFile %h/.ssh/authorized_keys`
   - `PasswordAuthentication yes`
   - `ChallengeResponseAuthentication no`
   - `UsePAM yes`
  
## Running the playbook

Place details about running your playbook here 

- `ansible-playbook site_backup.yml --extra-vars "env=prod" -e @vault.yml` 
- `ansible-playbook site_deploy.yml --extra-vars "env=stage" -e @vault.yml --skip-tags backup`
- `ansible-playbook site_deploy.yml --extra-vars "env=production" -e @vault.yml --skip-tags backup`
 
Backup is done when deploy is trigger as a first stage. Please use `--skip-tags backup` to omit it.
When deploy for the first time the `--skip-tags backup` must be used 
## Make a backup and restore of DB
### Backup
The backup need ~/backups folder to be available on the host
 - `ansible-playbook site_backup.yml --extra-vars "env=prod" -e @vault.yml`
  
### Restore
Use restore to load deafault database. 

setup proper restor file in `host_vars/localhost.yml` e.g.:
 - `restore_file_path: "{{ backup_dest }}/backup_workshop_prod_2024-06-28_14-50-54.psql.bin"`

pr use `--extra-vars` to set a path to restore file then run the command
 - `ansible-playbook site_restore.yml --extra-vars "env=prod" -e @vault.yml`

## Instant command mode
You can use ansible chosen module from the command line e.g.:

- `ansible <group> -m <module>` -> `ansible all -m ping`
- `ansible <group> -m shell -a "<command>"` -> `ansible all -m shell -a "touch test_file"`

# Cert managements

- install `ansible-galaxy collection install community.crypto`
- initial cert:
  - You need to use dummy certs in nginx for the first time otherwise the nginx will crush
  - `docker compose exec certbot sh`
  - `certbot certonly --webroot --webroot-path=/var/www/certbot -d radoxim-rental.pl -d www.radoxim-rental.pl --debug --verbose`

## Notes:

### Usefull commands:

- Module documentation: `ansible-doc <module>` -> `ansible-doc copy`
- Chcek servers uptime: `ansible all -m shell -a "uptime" -e @vault.yml`
- Ping: `ansible all -m ping -e @vault.yml`
- Copy the file: `ansible [group] -m copy -a "[src=sorce_path dest=destination_path]" -e @vault.yml` 
-> fact file copy: `ansible all -m copy -a "src=./roles/common/files/docker.fact dest=/etc/ansible/facts.d mode=0755" -e @vault.yml`
- Create/overwrite the file/directory: `ansible [group] -m file -a "dest=[where the file should be create] state=touch" -e @vault.yml`
-> Fact firectory: `ansible all -m file -a "dest=/etc/ansible/facts.d state=directory" -e @vault.yml`
- Get custom facts: `ansible all -m setup -e @vault.yml -a "filter=ansible_local"`
- Install package on client: `ansible all -m apt -a "name=nano state=latest" -e @vault.yml`

- Run Docker Compose Logs Command: `ansible ucd -m shell -a "cd /home/aak/web && docker compose logs web > /tmp/docker_web_logs.txt" -e @vault.yml`
- Display the Logs: `ansible ucd -m shell -a "cat /tmp/docker_web_logs.txt" -e @vault.yml`

- `rsync -av --exclude='.git' --exclude='.venv' /home/aak/rep/covitech/elemik/ucdrivers.eu/ ./roles/deploy/files/web`

# Crone 

Use crone to automatically perform backup od database 

- `crontab -e`
- `0 2 * * * ansible-playbook /home/aak/rep/covitech/workshop_rental/ansible/site_backup.yml --extra-vars "env=prod" -e @/home/aak/rep/covitech/workshop_rental/ansible/vault.yml >> /home/aak/rep/covitech/workshop_rental/backups/logfile.log 2>&1`
- `0 2 * * *`: This schedule runs the job every day at 2:00 AM.
