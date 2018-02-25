# Embedded Ldap KDC

This project implements an embedded LDAP and Kerberos service that can be used for Unit tests.
It is also useful for testing Hadoop clusters secured with Kerberos.
Also, I added few Microsoft AD schema object like sAMAccountName and memberOf to [mimic Active Directory](./EmbeddedLdapKDC/src/main/resources/krish.schema)

## EmbeddedLdapKDC

It is an project that can be run in your idea by using maven. The main class is `com.krish.ead.server.EADServer`.

## JUnit Integration

1. To write JUnit test refer to the class `com.krish.ead.server.KerberosLdapIntegrationTest`.
2. To generate keytabs refer to `com.krish.ead.server.KerberosLdapIntegrationTest.createKeytab`.
3. If you want to `kinit` from unix shell, copy the file `krb5.conf` from `./EmbeddedLdapKDC/src/main/resources/krb5.conf` to `/etc/krb5.conf` (or to another folder you like) and use this command.

```bash
 env KRB5_CONFIG="location of krb5.conf" kinit krish
```

4. To add programmatically a user or groups refer to the class `com.krish.directory.service.EadSchemaService`, where various methods are exposed to do the same.

> Alternatively, you may also use ldapsearch, ldapmodify, ldapadd etc from unix shell or in a script.
  refer to the command below to add an user through ldif which is in Resources folder here.

```bash
$ ldapmodify -H "ldap://localhost:10389" -D "cn=manager,ou=users,dc=jpmis,dc=com" -w manager -a -f captain.ldif
```

>  By default, the embedded server will add users as Read only user, so if you need to add, delete or modify any objects
one need to be login as `cn=manager,ou=users,dc=jpmis,dc=com` with password manager to do so,

The default port for LDAP Server is `10389` and Kerberos is `16088`. Feel free to change this.

You can also start the server from shell.
Go to StandaloneEmbeddedLdapKDC/bin and invoke ./ead.sh "instance name" "start or run"

If you want to read more take a look at this [blog post](http://krishdey5.blogspot.com/)


#LDAP #HADOOP #EMBEDDEDKDC #EMbedded LDAP #Embedded KDC
