# Worker Skills 仓库

这个目录是所有可分配给 Worker 的 skills 的中央仓库。Manager 负责管理这些 skills 的定义，并通过 `push-worker-skills.sh` 将其分发给特定 Worker。

## 目录结构

```
worker-skills/
├── README.md                  # 本文件
└── <skill-name>/
    └── SKILL.md               # Skill 的说明和使用方式
    └── scripts/               # （可选）Skill 附带的脚本
```

## 如何新增自定义 Skill

1. 在此目录下创建新的 `<skill-name>/` 子目录
2. 编写 `SKILL.md` 说明该 skill 的功能和使用方式
3. 如需脚本，放在 `<skill-name>/scripts/` 下
4. 使用 `push-worker-skills.sh --worker <name> --add-skill <skill-name>` 分配给 Worker

## 如何分配/更新 Skills

```bash
# 给指定 Worker 分配新 skill
bash /opt/hiclaw/agent/skills/worker-management/scripts/push-worker-skills.sh \
  --worker <name> --add-skill <skill-name>

# 推送某个 skill 的更新到所有持有该 skill 的 Worker
bash /opt/hiclaw/agent/skills/worker-management/scripts/push-worker-skills.sh \
  --skill <skill-name>

# 查看当前 Worker skill 分配情况
cat ~/hiclaw-fs/agents/manager/workers-registry.json
```

## 注意

- `file-sync` 是 bootstrap skill，内置于 Worker 镜像，无需通过此目录管理
- 此目录中的 skills 由 Manager 统一维护，Worker 不能修改自己的 skills
- Worker 的 skill 分配记录在 `~/hiclaw-fs/agents/manager/workers-registry.json`
