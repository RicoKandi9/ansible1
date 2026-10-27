# Lab 3: Veebiserveri laiendamine PHP toega (Ansible)

Ansible playbookid PHP paigaldamiseks ja eemaldamiseks kliendiserverites.

| Klient | OS | Veebiserver | Paketihaldur |
|---|---|---|---|
| 192.168.45.198 | Debian 13 | apache2 | apt |
| 192.168.45.23 | CentOS Stream 9 | httpd | dnf |

Inventory: `/root/hosts`, grupp `[webservers]`.

## Failid

- `php.yml` – paigaldab PHP (Debian: `php`, `libapache2-mod-php`, `php-mysql`; CentOS: `php`, `php-fpm`, `php-mysqlnd`), käivitab Apache ja php-fpm teenused, avab CentOS-i tulemüüris http ning loob testfailid `/var/www/html/phpinfo.php` ja `/var/www/html/info.php` (Iseseisev ülesanne 1).
- `uninst_php.yml` – leiab kõik paigaldatud PHP paketid ja eemaldab need koos seadistusfailide ja sõltuvustega, kustutab testfailid ja kontrollib, et `php` käsku enam pole (Iseseisev ülesanne 2).

## Kasutamine

```bash
# kontroll (midagi ei muudeta)
ansible-playbook --check /etc/ansible/playbooks/php.yml
# PHP paigaldus + phpinfo.php
ansible-playbook /etc/ansible/playbooks/php.yml
# PHP eemaldamine
ansible-playbook /etc/ansible/playbooks/uninst_php.yml
```

Kontroll brauseris: `http://<kliendi_ip>/phpinfo.php`
