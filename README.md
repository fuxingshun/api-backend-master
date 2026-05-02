# api-backend-master

基于 Spring Boot、Spring Cloud Gateway、Dubbo、Nacos、Redis、MyBatis-Plus 和 Java 客户端 SDK 搭建的 API 开放平台后端项目。

## 项目模块

- `api-common`：公共实体类、枚举、VO 对象和内部服务接口。
- `api-client-sdk`：用于 API 请求签名和调用的 Java 客户端 SDK。
- `api-interface`：模拟 API 接口服务。
- `api-gateway`：基于 Spring Cloud Gateway 的网关服务，负责请求校验、签名校验和调用统计。
- 根目录主应用：负责用户、接口信息、接口调用关系等后台管理能力。
- `sql/create_table.sql`：数据库初始化脚本。

## 技术栈

- Java 8
- Spring Boot 2.7.x
- Spring Cloud Gateway 2021.0.x
- Apache Dubbo 3.0.9
- Nacos 2.x
- MySQL
- Redis
- MyBatis-Plus
- Knife4j

## 配置说明

项目中的敏感配置通过环境变量读取，不会直接提交真实密码、密钥或 token。

| 环境变量 | 说明 | 默认值 |
| --- | --- | --- |
| `MYSQL_HOST` | MySQL 地址 | `localhost` |
| `MYSQL_PORT` | MySQL 端口 | `3306` |
| `MYSQL_DATABASE` | MySQL 数据库名 | `api` |
| `MYSQL_USERNAME` | MySQL 用户名 | `root` |
| `MYSQL_PASSWORD` | MySQL 密码 | 生产环境必填 |
| `API_CLIENT_ACCESS_KEY` | 示例客户端 Access Key | `demo-access-key` |
| `API_CLIENT_SECRET_KEY` | 示例客户端 Secret Key | `change-me` |
| `NACOS_HOST` | Nacos 地址 | `localhost` |
| `NACOS_PORT` | Nacos 端口 | `8848` |

PowerShell 配置示例：

```powershell
$env:MYSQL_PASSWORD="your_mysql_password"
$env:API_CLIENT_ACCESS_KEY="your_access_key"
$env:API_CLIENT_SECRET_KEY="your_secret_key"
```

## 快速启动

1. 创建数据库，并导入 `sql/create_table.sql`。
2. 启动本地 MySQL、Redis 和 Nacos。
3. 先将公共模块和 SDK 安装到本地 Maven 仓库：

```powershell
cd api-common
mvn clean install
cd ..\api-client-sdk
mvn clean install
cd ..
```

4. 根据需要启动各个后端服务：

```powershell
mvn spring-boot:run
cd api-interface
mvn spring-boot:run
cd ..\api-gateway
mvn spring-boot:run
```

默认端口：

- 后台服务：`7529`，接口前缀 `/api`
- 模拟接口服务：`8123`，接口前缀 `/api`
- 网关服务：`8090`

## 安全提醒

- 不要提交真实数据库密码、API 密钥、token 或私有服务地址。
- 本地敏感配置建议放到环境变量，或放到已被忽略的 `application-local.yml` 文件中。
- 如果某些密码或密钥曾经写在本地配置文件里，公开仓库前建议先进行轮换。
