# Skills And Command Injection

skills 和 slash command 都会影响模型看到的上下文。

## 关键文件

- `restored-src/src/skills/loadSkillsDir.ts`
- `restored-src/src/skills/bundledSkills.ts`
- `restored-src/src/utils/processUserInput/processSlashCommand.tsx`
- `restored-src/src/tools/SkillTool/SkillTool.ts`

## 这部分的意义

- skill 不是“文档附件”
- slash command 也不只是 UI 命令
- 它们会进入系统上下文，影响模型接下来怎么行动

## 读法建议

先看 `loadSkillsDir.ts` 怎么发现技能，再看 `processSlashCommand.tsx` 怎么把命令变成会话里的实际输入。

