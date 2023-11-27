<p align="center">
	<img src="docs/jira.png" alt="Jira">
</p>

This project comes as a pre-built docker image that enables you to easily installation Jira without having to know too much about setup Jira.

## Features
- Supports almost all plug-ins.
- Support DataCenter mode.
- Compared with traditional crack, you can easily upgrade your service without having to crack it again.
- Provides a java-based command line keygen, which is more convenient to use in a terminal environment.

## Quick Setup

1. Install Docker and Docker-Compose
- [Docker Install documentation](https://docs.docker.com/install/)
- [Docker-Compose Install documentation](https://docs.docker.com/compose/install/)

2. Bring up your stack by running
```shell
git clone https://github.com/trants/jira.git \
    && cd jira \
    && cp .env.example .env
```

3. Edit environment variable
```bash
# Jira
VERSION=9.4.12
PORT=8080
ATL_PROXY_NAME=localhost
ATL_PROXY_PORT=443
ATL_TOMCAT_PORT=8090
ATL_TOMCAT_SCHEME=https
ATL_TOMCAT_SECURE=true
JVM_CODE_CACHE_ARGS="-XX:InitialCodeCacheSize=1g -XX:ReservedCodeCacheSize=8g"
JVM_MAXIMUM_MEMORY=12g
JVM_MINIMUM_MEMORY=1g
TZ=UTC

# MySQL
MYSQL_USER=user
MYSQL_DATABASE=database
MYSQL_PASSWORD=password
MYSQL_ROOT_PASSWORD=rootpassword

# Backup
SCHEDULE=@weekly
BACKUP_KEEP_DAYS=7
PASSPHRASE=wxHw26GJZQBDenA8
S3_BUCKET=my-s3-bucket
S3_REGION=us-east-1
S3_PREFIX=prefix
S3_ACCESS_KEY_ID=AKIA3M3ZKBJPQUBT2UK6
S3_SECRET_ACCESS_KEY=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
MYSQL_HOST=mysql
```

4. Start Jira
```shell
docker-compose up -d
```

## How to hack Jira
```shell
docker exec jira java -jar /var/agent/atlassian-agent.jar \
    -d \
    -p conf \
    -m email@example.com \
    -n email@example.com \
    -o http://yourdomain.com \
    -s you-server-id-xxxx
```

## How to hack Jira plugin
- Example I want to use BigGantt plugin
1. Install BigGantt from jira marketplace.
2. Find `App Key` of BigGantt is : `eu.softwareplant.biggantt`
3. Execute :
```shell
docker exec jira java -jar /var/agent/atlassian-agent.jar \
    -d \
    -p eu.softwareplant.biggantt \
    -m email@example.com \
    -n email@example.com \
    -o http://yourdomain.com \
    -s you-server-id-xxxx
```
4. Paste your license

## How to upgrade

```shell
cd jira && git pull
docker pull walruship/jira:latest && docker-compose stop
docker-compose rm
```

## Security
- If you discover any security related issues, please email 286.trants@gmail.com instead of using the issue tracker.

## License
- This software is released under the [BSD 3-Clause][link-license] License. Please see the [LICENSE](LICENSE) file or https://walruship.com/LICENSE.txt for more information.

[link-license]: https://opensource.org/license/bsd-3-clause/