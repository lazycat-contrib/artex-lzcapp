# ARTEXX - LazyCat App

[ARTEXX](https://github.com/trhhubsd/ARTEXX)（AI 自主渗透测试系统，百度“agent+”攻防挑战赛冠军项目 ARTEX 的延续）的懒猫微服（LazyCat）打包。

## 模式

- **镜像模式（mirror）**：`docker.io/tomicdd/artex` 镜像经 `docker.1ms.run` 加速器拉取，`require_digest_match: true` 校验镜像内容与上游一致。
- **自动跟随上游**：上游仅发布 `latest` 可变 tag（amd64），采用 digest 比对 + `bump: patch` 模式——manifest 固定 `latest@sha256:...` 基线，镜像内容变化时自动 patch +1、更新 pin 并发布。
- **喵喵商店发布**：仅私有商店（MiaoMiao private store），不发布官方商店。

## 配置

- 双服务：`artex` + `postgres:16-alpine`（密码 `stable_secret` 自动生成）
- 数据卷：`/lzcapp/var/artex/data:/app/data`（jwt.key、SQLite 等）+ `skills`（技能目录）+ `pgdata`
- LLM 配置：部署参数可选填 Anthropic/OpenAI Key（也可之后在「LLM 配置」页填写）
- 首次进入 `/setup` 设置管理员密码
- 流量录制代理端口 8788 仅容器内监听（上游默认绑定 127.0.0.1）

## 安全提示

⚠️ 本应用为渗透测试工具，仅限在**授权环境**下对**自有资产**进行安全测试使用。

## 所需 Secrets

| Secret | 说明 |
| --- | --- |
| `APPSTORE_URL` / `APPSTORE_TOKEN` | 喵喵商店 API 地址与发布令牌 |
| `APP_ID` | 可选 |
| `PRIVATE_STORE_GROUP_CODES` | 可选，私有分组码 |

## 许可

AGPL-3.0（上游）
