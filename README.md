# api-backend-master

API open platform backend built with Spring Boot, Spring Cloud Gateway, Dubbo, Nacos, Redis, MyBatis-Plus, and a small Java client SDK.

## Modules

- `api-common`: shared entities, enums, VO objects, and internal service contracts.
- `api-client-sdk`: client SDK used to sign and invoke API requests.
- `api-interface`: demo API provider service.
- `api-gateway`: Spring Cloud Gateway service that validates requests and records invocation data.
- Root application: management backend for users, interface metadata, and invocation records.
- `sql/create_table.sql`: database initialization script.

## Tech Stack

- Java 8
- Spring Boot 2.7.x
- Spring Cloud Gateway 2021.0.x
- Apache Dubbo 3.0.9
- Nacos 2.x
- MySQL
- Redis
- MyBatis-Plus
- Knife4j

## Configuration

Sensitive values are read from environment variables and are intentionally not committed.

| Variable | Description | Default |
| --- | --- | --- |
| `MYSQL_HOST` | MySQL host | `localhost` |
| `MYSQL_PORT` | MySQL port | `3306` |
| `MYSQL_DATABASE` | MySQL database | `api` |
| `MYSQL_USERNAME` | MySQL username | `root` |
| `MYSQL_PASSWORD` | MySQL password | required for production |
| `API_CLIENT_ACCESS_KEY` | Demo client access key | `demo-access-key` |
| `API_CLIENT_SECRET_KEY` | Demo client secret key | `change-me` |
| `NACOS_HOST` | Nacos host | `localhost` |
| `NACOS_PORT` | Nacos port | `8848` |

Example PowerShell setup:

```powershell
$env:MYSQL_PASSWORD="your_mysql_password"
$env:API_CLIENT_ACCESS_KEY="your_access_key"
$env:API_CLIENT_SECRET_KEY="your_secret_key"
```

## Quick Start

1. Create the database and import `sql/create_table.sql`.
2. Start MySQL, Redis, and Nacos locally.
3. Install shared modules into the local Maven repository:

```powershell
cd api-common
mvn clean install
cd ..\api-client-sdk
mvn clean install
cd ..
```

4. Start the backend services as needed:

```powershell
mvn spring-boot:run
cd api-interface
mvn spring-boot:run
cd ..\api-gateway
mvn spring-boot:run
```

Default ports:

- Backend: `7529`, context path `/api`
- Interface service: `8123`, context path `/api`
- Gateway: `8090`

## Security Notes

- Do not commit real database passwords, API keys, tokens, or private service addresses.
- Use environment variables or ignored `application-local.yml` files for local secrets.
- Rotate any credential that was previously stored in a local config file before making the repository public.
