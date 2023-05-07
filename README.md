<h1 align="center"><a href="https://retool.com/">Retool 101</a></h1>

## Introduction

Retool helps you to build admin panels and dashboards with ease. Because of internet issues in Iran, I am going to use its on-promise setup.
The on-promise setup is done based on this [repository](https://github.com/tryretool/retool-onpremise).

## [Step-by-Step](https://retool.com/self-hosted)

- Clone Retool on premise repository:

```bash
git clone git@github.com:tryretool/retool-onpremise.git
```

- Create `docker.env` with the following configuration:

```bash
# Set node environment to production
#NODE_ENV=production

# Set the JWT secret for the API server
JWT_SECRET=randomstring

DEBUG=true
LOG_LEVEL=debug
IS_ADMIN=true
DATABASE_MIGRATIONS_TIMEOUT_SECONDS=600

# Set and generate postgres credentials
#
# These variables can be changed to point to a database you host yourself
POSTGRES_DB=postgres
POSTGRES_USER=root
POSTGRES_HOST=postgres
POSTGRES_PORT=5432
POSTGRES_PASSWORD=randomstring

RETOOLDB_POSTGRES_DB=postgres
RETOOLDB_POSTGRES_USER=root
RETOOLDB_POSTGRES_HOST=retooldb-postgres
RETOOLDB_POSTGRES_PORT=5432
RETOOLDB_POSTGRES_PASSWORD=randomstring

## If you need Google SSO
# CLIENT_ID={GOOGLE CLIENT ID}
# CLIENT_SECRET={GOOGLE CLIENT SECRET}

## If you wish for Retool to be hosted on a server with a public IP address, then you can use these configs to run the nginx container
# HOSTNAME=https://retool.company.com
# DOMAINS=http://localhost -> http://api:3000

## License key
COOKIE_INSECURE=true
LICENSE_KEY=CHANGE_ME
```

- Create `retooldb.env` with the following configuration:

```bash
# Set and generate postgres credentials
#
# These variables can be changed to point to a database you host yourself
POSTGRES_DB=postgres
POSTGRES_USER=root
POSTGRES_HOST=retooldb-postgres
POSTGRES_PORT=5432
POSTGRES_PASSWORD=randomstring
```

- Add your auto-generated license key to the `docker.env` file instead of `CHANGE_ME`.

- Remove `https-portal` service from `docker-compose.yml`.

- Start `docker compose`:

```bash
docker compose up
```

- Connect into database and add a dummy row into `organizations` table:

```sql
insert into organizations values (1, 'home', 'parham', 'host', now(), now());
```

- Restart `docker compose`:

```bash
docker compose restart
```

- Remove the dummy row from `organizations` table:

```sql
delete from organizations;
```

- Sign up and create a new user with organization.

```
http://192.168.73.3:3000/auth/signup
```
