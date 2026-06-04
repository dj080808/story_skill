# 儿童故事生成 Skill — 项目说明

## 项目目标

构建一个 Claude skill，让 Claude 能够根据用户提供的：
- **动画人物**（如小猪佩奇、哆啦A梦、汪汪队等）
- **故事主题**（如友谊、勇气、分享、环保等）

自动生成一篇符合儿童阅读水平、融入该角色性格设定的原创短故事。

---

## 技术架构

```
children-story-skill/
├── CLAUDE.md                     ← 本文件（项目说明）
├── SKILL.md                      ← Skill 入口
├── references/
│   ├── characters.md             ← 角色设定库索引（按需路由到独立文件）
│   ├── characters/               ← 每个动画独立一个文件（避免无关 token）
│   │   ├── peppa-pig.md
│   │   ├── doraemon.md
│   │   ├── paw-patrol.md
│   │   ├── super-wings.md
│   │   ├── xiyangyang.md
│   │   ├── boonie-bears.md
│   │   ├── calabash-brothers.md
│   │   └── shuke-and-beta.md
│   └── story-structure.md        ← 儿童故事结构指南
└── assets/
    └── example-stories/          ← 示例故事（3 个）
        ├── 01-doraemon-courage.md
        ├── 02-pawpatrol-environment.md
        └── 03-xiyangyang-friendship.md
```

---

## 开发任务（按顺序执行）

### Step 1：创建角色设定库
文件：`references/characters.md`
- 收录 10–15 个常见儿童动画角色
- 每个角色包含：性格特点、口头禅、擅长/不擅长的事、人际关系
- 格式统一，便于 SKILL.md 引用

### Step 2：编写故事结构指南
文件：`references/story-structure.md`
- 适合 3–8 岁儿童的故事结构（起因→经过→结局）
- 语言风格要求（简单词汇、短句、重复节奏）
- 字数建议：300–500 字
- 必须包含：角色特点的自然融入、主题的正向传递

### Step 3：编写 SKILL.md
- YAML frontmatter：name、description（触发时机要写清楚）
- 故事生成流程：解析输入 → 查角色设定 → 套用结构 → 输出故事
- 输出格式：故事标题 + 正文 + 一句话主题总结

### Step 4：准备示例故事
目录：`assets/example-stories/`
- 至少准备 3 个示例（不同角色 × 不同主题）
- 用于验证 skill 效果，也可作为 few-shot 参考

### Step 5：测试与迭代
- 测试提示词示例：
  - "帮我写一个关于小猪佩奇学会分享的故事"
  - "用哆啦A梦写一个关于勇气的儿童故事"
  - "写个汪汪队主题的环保故事"
- 根据输出质量调整 characters.md 和 story-structure.md

---

## 输出质量标准

一个好的故事输出应满足：
- [ ] 角色行为和台词符合其性格设定
- [ ] 故事有清晰的起因、经过、结局
- [ ] 语言适合目标年龄段（词汇简单、句子短）
- [ ] 主题传递自然，不说教
- [ ] 字数在 300–500 字之间

---

## 注意事项

- 角色版权：故事为原创内容，角色仅作为设定参考
- 语言：默认输出中文，用户指定时可切换
- 禁止内容：暴力、恐怖、负面价值观