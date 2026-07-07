# Standard Skills

**Standard Skills** — AI Company OS 出品。我们是给 Agent Skill 定标准的工作室。

skills.sh 上有 18,000+ 个 skill，但我们对质量不放心。所以我们做了三件事：
1. 解剖了 42 个代表性 skill，建立了质量评估框架
2. 跑了 10 轮 benchmark 验证框架的预测力
3. 用这套框架自己设计了几个 skill

发布的都是验证过的、不依赖特定系统的独立 skill。

## 包含的 Skill

| Skill | 说明 | 适合 |
|---|---|---|
| **skill-intelligence-framework** | 元 Skill — 分析、分类、评估、改进任何 Agent Skill | 所有 skill 作者 |
| **cascade-review** | 四入口并行级联代码审查。比串行 checklist 多抓 30% bug | Claude / 强模型 |
| **local-code-review** | 为本地/弱模型设计的模式匹配代码审查。12 个模式 + 决策树 | qwen / 本地模型 |
| **local-code-gen** | 为弱模型设计的模板填充代码生成。10 个模板 + 填空约束 | qwen / 本地模型 |

## 安装

```bash
npx skills add standard-skills/standard-skills@cascade-review
npx skills add standard-skills/standard-skills@local-code-review
npx skills add standard-skills/standard-skills@local-code-gen
npx skills add standard-skills/standard-skills@skill-intelligence-framework
```

## 设计哲学

1. **探针是注意力引导，不是搜索边界。** 审查型 skill 的探针如果写成穷举清单，Agent 会停在清单边界。

2. **方法论税是真实的。** 每层结构都消耗上下文。对强模型，最好的 skill 往往是薄的。

3. **发现力和交付力是两回事。** 一个擅长挖 bug 的 skill 不一定擅长写报告。必要时拆成 hunter + consolidator。

4. **Skill 类型由收敛方向决定，不是由领域决定。** 不要问"这是代码 skill 还是美术 skill"，问"它最终收敛到问题列表、可用产物、还是判断结论"。

## 谁在用

AI Company OS 内部 11 个 agent 全部运行这套 skill 系统。

## License

MIT
