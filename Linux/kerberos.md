### Kerberos install  
```
 yum install krb5-libs krb5-server -y
 ```
 
``` [root@m2-maprts-vm57-173 ~]# cat /etc/krb5.conf
[logging]
 default = FILE:/var/log/krb5libs.log
 kdc = FILE:/var/log/krb5kdc.log
 admin_server = FILE:/var/log/kadmind.log

[libdefaults]
 ticket_lifetime = 24000
 default_realm =MIP.STORAGE.HPECORP.NET

[realms]
MIP.STORAGE.HPECORP.NET = {
  kdc = m2-maprts-vm57-173.mip.storage.hpecorp.net:88
  admin_server = m2-maprts-vm57-173.mip.storage.hpecorp.net:749
  default_domain = mip.storage.hpecorp.net
 }

[domain_realm]
 .mip.storage.hpecorp.net =MIP.STORAGE.HPECORP.NET
 mip.storage.hpecorp.net =MIP.STORAGE.HPECORP.NET

[kdc]
 profile = /var/kerberos/krb5kdc/kdc.conf

[pam]
 debug = false
 ticket_lifetime = 36000
 renew_lifetime = 36000
 forwardable = true
 krb4_convert = false

 ```
 
```
[root@m2-maprts-vm57-173 ~]# cat /var/kerberos/krb5kdc/kdc.conf
[kdcdefaults]
 kdc_ports = 88
 kdc_tcp_ports = 88

[realms]
 MIP.STORAGE.HPECORP.NET = {
  #master_key_type = aes256-cts
  acl_file = /var/kerberos/krb5kdc/kadm5.acl
  dict_file = /usr/share/dict/words
  admin_keytab = /var/kerberos/krb5kdc/kadm5.keytab
  supported_enctypes = aes256-cts:normal aes128-cts:normal des3-hmac-sha1:normal arcfour-hmac:normal camellia256-cts:normal camellia128-cts:normal des-hmac-sha1:normal des-cbc-md5:normal des-cbc-crc:normal
 }
[root@m2-maprts-vm57-173 ~]#

```

```
[root@m2-maprts-vm164-173 ~]# kdb5_util create -s
Loading random data
Initializing database '/var/kerberos/krb5kdc/principal' for realm 'EXAMPLE.COM',
master key name 'K/M@EXAMPLE.COM'
You will be prompted for the database Master Password.
It is important that you NOT FORGET this password.
Enter KDC database master key:
Re-enter KDC database master key to verify:
[root@m2-maprts-vm164-173 ~]# kadmin.local
Authenticating as principal root/admin@EXAMPLE.COM with password.
```
 
 ```
  service krb5kdc start

```
```
[root@m2-maprts-vm57-173 ~]# kadmin.local
Authenticating as principal root/admin@MIP.STORAGE.HPECORP.NET with password.
kadmin.local:  listprincs
K/M@MIP.STORAGE.HPECORP.NET
kadmin/admin@MIP.STORAGE.HPECORP.NET
kadmin/changepw@MIP.STORAGE.HPECORP.NET
kadmin/m2-maprts-vm57-173.mip.storage.hpecorp.net@MIP.STORAGE.HPECORP.NET
kiprop/m2-maprts-vm57-173.mip.storage.hpecorp.net@MIP.STORAGE.HPECORP.NET
krbtgt/MIP.STORAGE.HPECORP.NET@MIP.STORAGE.HPECORP.NET
root/admin@MIP.STORAGE.HPECORP.NET
kadmin.local:  addprinc root
WARNING: no policy specified for root@MIP.STORAGE.HPECORP.NET; defaulting to no policy
Enter password for principal "root@MIP.STORAGE.HPECORP.NET":
Re-enter password for principal "root@MIP.STORAGE.HPECORP.NET":
Principal "root@MIP.STORAGE.HPECORP.NET" created.
kadmin.local:  listprincs
K/M@MIP.STORAGE.HPECORP.NET
kadmin/admin@MIP.STORAGE.HPECORP.NET
kadmin/changepw@MIP.STORAGE.HPECORP.NET
kadmin/m2-maprts-vm57-173.mip.storage.hpecorp.net@MIP.STORAGE.HPECORP.NET
kiprop/m2-maprts-vm57-173.mip.storage.hpecorp.net@MIP.STORAGE.HPECORP.NET
krbtgt/MIP.STORAGE.HPECORP.NET@MIP.STORAGE.HPECORP.NET
root/admin@MIP.STORAGE.HPECORP.NET
root@MIP.STORAGE.HPECORP.NET
kadmin.local:  quit
```

```
[root@m2-maprts-vm57-173 ~]# kinit
Password for root@MIP.STORAGE.HPECORP.NET:
[root@m2-maprts-vm57-173 ~]# klist
Ticket cache: FILE:/tmp/krb5cc_0
Default principal: root@MIP.STORAGE.HPECORP.NET

Valid starting       Expires              Service principal
01/05/2022 18:26:26  01/06/2022 01:06:26  krbtgt/MIP.STORAGE.HPECORP.NET@MIP.STORAGE.HPECORP.NET

```
 
 
 
