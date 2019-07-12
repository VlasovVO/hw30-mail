Vagrant.configure(2) do |config|
  config.vm.box = "centos/7"
  config.vm.box_check_update = true
  config.vm.network :forwarded_port, guest: 25, host: 2000
  config.vm.define "mail", primary: true do |d|
    d.vm.network "private_network", ip: "192.168.111.10"
    d.vm.provision "shell", inline: <<-SHELL
      sudo sed -i 's/SELINUX=enforcing/SELINUX=disabled/' /etc/selinux/config
      yum install -y postfix dovecot
      postconf -n > /etc/postfix/main.cf-new
      mv /etc/postfix/main.cf /etc/postfix/main.cf-orig && mv /etc/postfix/main.cf-new /etc/postfix/main.cf
      # postconf -e myhostname=otus.test
      # postconf -e virtual_alias_domains=otus.test
      postconf -e virtual_alias_maps=hash:/etc/postfix/virtual
      postconf -e virtual_gid_maps=static:5000
      postconf -e virtual_mailbox_base=/var/mail
      postconf -e virtual_mailbox_domains=otus.test
      postconf -e virtual_mailbox_maps=hash:/etc/postfix/vmailbox
      postconf -e virtual_minimum_uid=100
      postconf -e virtual_uid_maps=static:5000
      mkdir /var/mail/otus.test
      chmod 777 /var/mail/otus.test
      echo "postmaster@otus.test postmaster" >> /etc/postfix/virtual
      cd /etc/postfix
      postmap virtual
      echo "info@otus.test    otus.test/info" >> /etc/postfix/vmailbox
      echo "sales@otus.test   otus.test/sales" >> /etc/postfix/vmailbox
      postmap vmailbox
      echo "mail_location = mailbox:/var/mail/otus.test/%u" >> /etc/dovecot/dovecot.conf
      # useradd -m -s /bin/bash info
      # echo "info" | passwd --stdin info
      # useradd -m -s /bin/bash sales
      # echo "sales" | passwd --stdin sales
      systemctl restart dovecot
      postfix reload
      # for debug
      yum install -y telnet mailx
    SHELL
  end
end
