# Dockerized Atlassian Crucible

"Review code, discuss changes, share knowledge, and identify defects across SVN, Git, Mercurial, CVS, and Perforce." - [[Source](https://www.atlassian.com/software/crucible)]

## Supported tags and respective Dockerfile links

| Product |Version | Tags  | Dockerfile |
|---------|--------|-------|------------|
| Crucible | 4.4.1 | 4.4.1, latest | [Dockerfile](https://github.com/blacklabelops/crucible/blob/master/Dockerfile) |

## Related Images

You may also like:

* [blacklabelops/jira](https://github.com/blacklabelops/jira): The #1 software development tool used by agile teams
* [blacklabelops/confluence](https://github.com/blacklabelops/confluence): Create, organize, and discuss work with your team
* [blacklabelops/bitbucket](https://github.com/blacklabelops/bitbucket): Code, Manage, Collaborate
* [blacklabelops/crowd](https://github.com/blacklabelops/crowd): Identity management for web apps

# Make It Short

Docker-CLI:

Just type and follow the manual installation procedure in your browser:

~~~~
$ docker run -d -p 8060:8060 --name crucible blacklabelops/crucible
~~~~

> Point your browser to http://yourdockerhost:8060

# Setup

1. Start database server for Crucible.
1. Start Crucible.
1. Manual Crucible setup.

Firstly, start the database server for Crucible:

> Note: Change Password!

~~~~
$ docker run --name postgres_crucible -d \
    -e 'POSTGRES_DB=crucibledb' \
    -e 'POSTGRES_USER=crucibledb' \
    -e 'POSTGRES_PASSWORD=jellyfish' \
    -e 'POSTGRES_ENCODING=UTF8' \
    blacklabelops/postgres
~~~~

Secondly, start Crucible:

~~~~
$ docker run -d --name crucible \
	  --link postgres_crucible:postgres_crucible \
	  -p 8060:8060 blacklabelops/crucible
~~~~

>  Starts Crowd and links it to the postgresql instances. JDBC URL: jdbc:postgresql://postgres_crucible/crucibledb

Thirdly, configure your Crucible yourself and fill it with a test license.

Point your browser to http://yourdockerhost:8060

1. Create and enter license information
1. Fill out the rest of the installation procedure.
1. Login to the application and enter the administration area.
1. Go to `System Settings` -> `Database`
1. Click `Edit` and fill out the form:
  * Type: `PostgreSQL`
  * Driver Location: `Bundled`
  * URL: `jdbc:postgresql://postgres_crucible:5432/crucibledb`
  * User Name: `crucibledb`
  * Password: `jellyfish`
  * Minimum Pool Connections: `5`
  * Maximum Pool Connections: `20`
  * Parameters:
1. Press `Test connection`and then `Save & Migrate`

Enjoy Crucible!

# Vagrant

First install:

* [Vagrant](https://www.vagrantup.com/)
* [Virtualbox](https://www.virtualbox.org/)

Vagrant is fabulous tool for pulling and spinning up virtual machines like docker with containers. I can configure my development and test environment and simply pull it online. And so can you! Install Vagrant and Virtualbox and spin it up. Change into the project folder and build the project on the spot!

~~~~
$ vagrant up
$ vagrant ssh
[vagrant@localhost ~]$ cd /vagrant
[vagrant@localhost ~]$ docker-compose up
~~~~

> Crucible will be available on http://localhost:8080 on the host machine.

# References

* [Atlassian Crucible](https://www.atlassian.com/software/crucible)
* [Docker Homepage](https://www.docker.com/)
* [Docker Compose](https://docs.docker.com/compose/)
* [Docker Userguide](https://docs.docker.com/userguide/)
* [Oracle Java](https://java.com/de/download/)
