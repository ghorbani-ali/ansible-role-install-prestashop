Prestashop installation Ansible Role
=========

### Easy installation of PrestaShop 8.x on Debian/Ubuntu using Ansible

# Requirements

PrestaShop 8.x has the following [system requirements](https://devdocs.prestashop-project.org/8/basics/installation/system-requirements/):
* System: Linux.
* Web server: Apache Web Server 2.4 or any later version, Nginx 1.0 or later (recomended).
* PHP: 8.0~8.1 ([compatibility chart](https://devdocs.prestashop-project.org/8/basics/installation/system-requirements/#php-compatibility-chart)).
* MySQL: 5.6 minimum, a recent version is recommended.

# Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

### Prestashop version to deploy
If Prestashop has already been installed using this Ansible role, this version has to be higher than the current installed version (no downgrades for stability purpose).

see Prestashop releses on [github](https://github.com/PrestaShop/PrestaShop/releases)

```yml
prestashop_version: 8.1.0
```


### The URL to download Prestashop installer.

```yml
prestashop_download_url: "https://github.com/PrestaShop/PrestaShop/releases/download/{{ prestashop_version }}/prestashop_{{ prestashop_version }}.zip"
```

### Name of the Prestashop Back Office folder
for security reasons, it is highly recommended to change this value with a random name, so that directory enumeration is made difficult for a potential attacker.

```yml
prestashop_backoffice_admin_folder: 'adminklwfjlkhF3DgG'
```

### Prestashop installation web root path (to reference in your local webserver)

```yml
prestashop_root_path: "/var/www/{{ prestashop_domain }}"
```

### Shop region
* `prestashop_timezone` : Set timezone of instance.
* `prestashop_language` : Language ISO code to install.
* `prestashop_country` : Country of the shop.
```yml
prestashop_timezone: "America/New_York"
prestashop_language: "en"
prestashop_country: "en"
```

### Prestashop domain name
will be written in the database and `.htaccess` file if using apache.

```yml
prestashop_domain: "prestashop.test"
```
### Prestashop database parameters
* `prestashop_db_server` : Database server hostname. any valid MySQL valid server name or IP address.
* `prestashop_db_user` : Database server user (will be created).
* `prestashop_db_password` : Database server password. the valid password for `db_user`.
* `prestashop_db_name` : Database name.
* `prestashop_db_clear` : if set to `1`, the installation process will drop existing tables in `prestashop_db_name`.
* `prestashop_db_create` : if set to `1`, `prestashop_db_name` will be created by the installation process.
* `prestashop_db_prefix` : Prefix of table names.
* `prestashop_db_prefix` : Engine for MySQL (InnoDB, MyISAM).

```yml
prestashop_db_server: "127.0.0.1"
prestashop_db_user: "prestashop"
prestashop_db_password: "prestashop"
prestashop_db_name: "prestashop"
prestashop_db_clear: 1
prestashop_db_create: 1
prestashop_db_prefix: "ps_"
prestashop_db_engine: "InnoDB"
```

### Prestashop admin user account

* `prestashop_firstname` : Admin user firstname.
* `prestashop_lastname` : Admin user lastname.
* `prestashop_email` : Your email to connect to the Back Office.
* `prestashop_password` : Password for the administration Back Office.
```yml
prestashop_firstname: "PrestaShop"
prestashop_lastname: "Developer"
prestashop_email: "dev@{{ prestashop_domain }}"
prestashop_password: "p_prestashop"
```

### Other basic configuration options for your shop
Those values are passed to the PHP installation script of Prestashop (more information [here](https://devdocs.prestashop-project.org/8/basics/installation/advanced/install-from-cli/)).

* `prestashop_name` : Name of the shop.
* `prestashop_activity` : Id of an activity [(Complete list of activities)](https://github.com/PrestaShop/PrestaShop/blob/8.0.x/src/PrestaShopBundle/Form/Admin/Configure/ShopParameters/General/PreferencesType.php#L211-L230).
* `prestashop_rewrite` : Enable rewrite engine.
* `prestashop_fixtures` : Install fixtures. Equivalent of “Installation of demo products” in the GUI.

```yml
prestashop_name: "PrestaShop"
prestashop_activity: 0
prestashop_rewrite: 1
prestashop_fixtures: 0
```

### Name of the file used by Ansible to detect Prestashop installation.

```yml
prestashop_install_check: 'prestashop-install-ansible.txt'
```

# Dependencies

* unzip
* php (see [compatibility chart](https://devdocs.prestashop-project.org/8/basics/installation/system-requirements/#php-compatibility-chart))
* mysql

# Example Playbook

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:
```yml
- hosts: localhost
  remote_user: root
  roles:
    - ansible-role-install-prestashop
```
# ansible-galaxy
Install the role with ansible-galaxy command:

```
ansible-galaxy install -p ansible-role-install-prestashop -f
```
# License

### GPL-3.0

# Author Information

This role was created in 2024 by [ghorbani-ali](https://github.com/ghorbani-ali).
