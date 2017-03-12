
# Load Balancer

## Status

### Verify Connection
----
> `> ssh root@173.230.156.80 -o strictHostKeyChecking=no "echo"`<br />

Connect to the machine and wait until its ready (with automatic retry).  Also add the machine to the `known_hosts` file, to prevent an interactive prompt


## Repositories

### Force use of IPv4
----

> Write data to `/etc/apt/apt.conf.d/99force-ipv4`

```shell
Acquire::ForceIPv4 "true";
```
> `> scp /tmp/pvc20170312-26838-tk8z81 root@173.230.156.80:/etc/apt/apt.conf.d/99force-ipv4`<br />

Needed for Linode as there were intermittent problems connecting to their repositories over IPv6 (February 2017)


### Update Repositories
----
> `> ssh root@173.230.156.80  "apt update -y"`<br />

### Install Requirements
----
> `> ssh root@173.230.156.80  "apt install -y software-properties-common python-software-properties"`<br />

Install the requirements for adding more repositories


### Nginx
----
> `> ssh root@173.230.156.80  "apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 561F9B9CAC40B2F7"`<br />
> `> ssh root@173.230.156.80  "apt-get install -y apt-transport-https ca-certificates"`<br />

> Write data to `/etc/apt/sources.list.d/passenger.list`

```shell
deb https://oss-binaries.phusionpassenger.com/apt/passenger xenial main
```
> `> scp /tmp/pvc20170312-26838-54hgae root@173.230.156.80:/etc/apt/sources.list.d/passenger.list`<br />

Install the latest version using the Phusion repos.


See also:  [https://www.phusionpassenger.com/library/install/nginx/install/oss/xenial/](https://www.phusionpassenger.com/library/install/nginx/install/oss/xenial/)