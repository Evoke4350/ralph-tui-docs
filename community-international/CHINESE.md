# Chinese Resources (中文资源)

## Overview

The Chinese developer community has created extensive documentation for Ralph Loop, OpenCode, and agentic AI development tools.

## Key Chinese Articles

### Juejin (掘金) Articles

| Title | Description |
|-------|-------------|
| [手把手配置Ralph -- 火爆X 的全自动AI 编程工具](https://juejin.cn/post/7592089325913440256) | Step-by-step Ralph configuration |
| [Ralph Wiggum 技巧：让Claude Code 自主运行数小时](https://juejin.cn/post/7591375103521210408) | Ralph Wiggum technique guide |
| [Claude Code 四大核心技能使用指南](https://juejin.cn/post/7593232758128574470) | Four core skills including Ralph Loop |
| [开发者神器来了！Anthropic官方Ralph Wiggum插件深度实测](https://juejin.cn/post/7591066233670156314) | Deep review of Ralph Wiggum plugin |

### CSDN Articles

| Title | Focus |
|-------|-------|
| [Claude Code 永动机：ralph-loop 无限循环迭代插件详解](https://blog.csdn.net/qq_44866828/article/details/156736656) | Installation, principles, best practices |
| [【保姆级教程】Claude Code 必备插件Ralph Wiggum](https://blog.csdn.net/zsr154278963/article/details/156637281) | Beginner-friendly tutorial |
| [Ralph Loop让AI持续工作直到真正完成](https://aicoding.csdn.net/696499d46554f1331aa1710c.html) | Ralph Loop continuous work |

### Zhihu (知乎) Articles

| Title | Focus |
|-------|-------|
| [开发者神器来了！Anthropic官方Ralph Wiggum插件深度实测](https://zhuanlan.zhihu.com/p/1991105524469608711) | Deep review of Ralph Wiggum |
| [从单模型到多代理协作的AI 编程革命](https://zhuanlan.zhihu.com/p/1993677669213156270) | AI programming revolution |

## Community Forums

### linux.do

**[这就是我喜欢用opencode的原因](https://linux.do/t/topic/1436111)**
- Active discussion about opencode and ralph-loop
- "Machine doesn't sleep" concept

## Chinese GitHub Repositories

| Repository | Description |
|------------|-------------|
| [code-yeongyu/oh-my-opencode](https://github.com/code-yeongyu/oh-my-opencode) | Chinese README available (README.zh-cn.md) |
| [guyskk/claude-code-supervisor](https://github.com/guyskk/claude-code-supervisor) | Alternative to Ralph with Chinese docs |

## Key Chinese Terminology

| English | Chinese (中文) |
|---------|---------------|
| Ralph Loop | 拉尔夫循环 |
| Stop Hook | 停止钩子 |
| Ralph Wiggum | 拉尔夫·威刚 |
| Promise Token | 承诺令牌 |
| Autonomous Development | 自主开发 |
| Multi-Agent Orchestration | 多智能体编排 |

## Chinese Community Best Practices

From Juejin and CSDN articles:

1. **从较低迭代限制开始** (Start with lower iteration limits)
   - Begin with 10-20 iterations for new tasks

2. **明确完成标准** (Define clear completion criteria)
   - Use specific completion markers for early exit

3. **使用版本控制** (Use version control)
   - Always run Ralph loops in git-tracked directories

4. **错误处理策略** (Error handling strategies)
   - `retry`: For flaky operations
   - `skip`: For non-critical tasks
   - `abort`: For critical workflows

## Cost Considerations

Chinese documentation emphasizes cost awareness:
- Typical 50-iteration loop: $50-100+
- Use `--max-iterations` for cost control
- "一个节省 20 小时工作的 100 美元循环是值得的" (A $100 loop saving 20 hours is worth it)
