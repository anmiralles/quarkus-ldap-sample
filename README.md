# quarkus-ldap-sample

This project uses Quarkus, and shows how to implement security using LDAP server.

## Running a docker LDAP server

In order to work locally, we need an instance of a docker LDAP server. For that we will 
use Bitnami OpenLdap:

https://hub.docker.com/r/bitnami/openldap/

We need to create the following docker-compose file:

```
version: '3'

services:
ldap:
image: docker.io/bitnami/openldap:2.6
container_name: openldap
ports:
- '1389:1389'
- '1636:1636'
volumes:
- ./ldifs/quarkus-io.ldif:/ldifs/quarkus-io.ldif
environment:
- LDAP_ROOT=dc=quarkus,dc=io
- LDAP_CUSTOM_LDIF_DIR=/ldifs
```

And create a local folder called "ldifs" with the linked file inside:

https://github.com/quarkusio/quarkus/blob/main/test-framework/ldap/src/main/resources/quarkus-io.ldif


## Running the application in dev mode

You can run your application in dev mode that enables live coding using:

```shell script
./docker-compose up -d
```

```shell script
./mvnw compile quarkus:dev
```

## Related Guides

Quarkus guide: https://quarkus.io/guides/security-ldap