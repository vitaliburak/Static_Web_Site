# Static_Web_Site
- hosts: web
  tasks:
  - name: Install httpd
    yum:
      name: httpd
      state: latest
  - name: Start httpd
    systemd:
      name: httpd
      state: started
  - name: Enable httpd
    systemd:
      name: httpd
      enabled: yes
      masked: no
- hosts: web
  tasks:
  - name: Download Templates
    get_url:
      url: https://www.free-css.com/assets/files/free-css-templates/download/page259/vanilla.zip
      dest: /var/www/html
- hosts: web
  tasks:
  - name: uznip
    yum:
      name: unzip
      state: latest
  - name: unzip file
    unarchive:
      src: /var/www/html/vanilla.zip
      dest: /var/www/html
      remote_src: yes
- hosts: web
  tasks:
  - name: Move files
    shell: mv /var/www/html/templatemo_526_vanilla/*  /var/www/html/
- hosts: web
  tasks:
  - selinux:
      state: disabled
- hosts: web
  tasks:
  - name: Attempt to change ownership on directory
    file:
      path: /var/www/html
      state: directory
      recurse: yes
      owner: apache
      group: apache
