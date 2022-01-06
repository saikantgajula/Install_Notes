!!! Kerberos install  

 yum install krb5-libs krb5-server -y
 
``` [root@m2-maprts-vm164-173 ~]# cat /etc/krb5.conf
[logging]
 default = FILE:/var/log/krb5libs.log
 kdc = FILE:/var/log/krb5kdc.log
 admin_server = FILE:/var/log/kadmind.log

[libdefaults]
 ticket_lifetime = 24000
 default_realm =EXAMPLE.COM

[realms]
EXAMPLE.COM = {
  kdc = 10.163.173.164:88
  admin_server = 10.163.173.164:749
  default_domain = uk.oracle.com
 }

[domain_realm]
 .uk.oracle.com =EXAMPLE.COM
 uk.oracle.com =EXAMPLE.COM

[kdc]
 profile = /var/kerberos/krb5kdc/kdc.conf

[pam]
 debug = false
 ticket_lifetime = 36000
 renew_lifetime = 36000
 forwardable = true
 krb4_convert = false
 ```
 
```[root@m2-maprts-vm164-173 ~]# cat /var/kerberos/krb5kdc/kdc.conf
[kdcdefaults]
    kdc_ports = 88
    kdc_tcp_ports = 88
    spake_preauth_kdc_challenge = edwards25519

[realms]
EXAMPLE.COM = {
     #master_key_type = aes256-cts
     acl_file = /var/kerberos/krb5kdc/kadm5.acl
     dict_file = /usr/share/dict/words
     admin_keytab = /var/kerberos/krb5kdc/kadm5.keytab
     supported_enctypes = aes256-cts:normal aes128-cts:normal des3-hmac-sha1:normal arcfour-hmac:normal camellia256-cts:normal camellia128-cts:normal
}
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
 
 
 
