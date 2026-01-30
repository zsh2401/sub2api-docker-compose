# Sub2API（可迁移）Docker Compose 部署

**原项目（GitHub）**：<https://github.com/Wei-Shaw/sub2api>

本目录提供一个可直接迁移的 Sub2API Docker Compose 部署环境：所有运行数据都落在当前目录的 `./data/` 下，方便备份/迁移/恢复。

## 启动 / 停止

准备：

```bash
mkdir -p ./data/sub2api ./data/postgres ./data/redis
cp env.example .env
# 编辑 .env（至少设置 POSTGRES_PASSWORD；建议同时固定 JWT_SECRET/TOTP_ENCRYPTION_KEY）
```

启动：

```bash
docker compose up -d
```

停止：

```bash
docker compose down
```

查看日志（首次启动如未设置 `ADMIN_PASSWORD`，会在日志里输出管理员密码）：
```bash
docker compose logs -f sub2api
```

更新镜像：

```bash
docker compose pull
docker compose up -d
```

访问：
- Web UI：`http://localhost:8080`

## 常见问题

### 容器名冲突（Conflict: container name is already in use）

说明你机器上已经存在同名容器（通常是之前在别的目录启动过 Sub2API）。

处理方式二选一：

```bash
# 方式 1：在旧目录执行 docker compose down
```

```bash
# 方式 2：直接删除旧容器（确认不再需要旧实例后再执行）
docker rm -f sub2api sub2api-postgres sub2api-redis
```

## 数据目录（迁移用）

- `./data/sub2api/`：Sub2API 运行数据（含自动生成的 `config.yaml` 等）
- `./data/postgres/`：PostgreSQL 数据目录
- `./data/redis/`：Redis 数据目录（AOF/RDB）

## 迁移

将整个目录（至少包含 `docker-compose.yml`、`.env`、`data/`）复制到新机器后，在目录内执行：

```bash
docker compose up -d
```
