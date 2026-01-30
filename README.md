# Sub2API Docker Compose（可迁移）

**原项目（GitHub）**：<https://github.com/Wei-Shaw/sub2api>

## 部署

```bash
git clone https://github.com/zsh2401/sub2api-docker-compose.git
cd sub2api-docker-compose
cp env.example .env
docker compose up -d
```

停止：

```bash
docker compose down
```

说明：所有运行数据默认会写到当前目录的 `./data/` 下，直接打包整个目录即可迁移。
