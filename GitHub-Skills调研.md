# GitHub Skills 调研

调研日期 2026-11-09。针对 MATLAB/Simulink 风电—电池—超级电容设计任务筛选，已检查候选技能的实际 `SKILL.md`、来源仓库及主要依赖。

## 1. 调研方法与选择结果

使用现有 `find-skills` 技能，先查看 skills.sh 目录，再通过 Skills CLI 检索 MATLAB、Simulink、scientific-writing 和 literature-review，并用 GitHub API 核对仓库信息。

本项目优先考虑以下六个技能。安装量为 skills.sh / CLI 查询时显示的近似值，Stars 为整个来源仓库的数量，这些统计会随时间变化。筛选同时考虑项目匹配度、作者来源、实际内容和依赖。

| 优先级 | Skill | 来源 | 安装量 | 仓库 Stars | 对本项目的用途 |
| --- | --- | --- | --- | --- | --- |
| 核心 | building-simulink-models | MathWorks，matlab/simulink-agentic-toolkit | 168 | 1,329 | 建立风电、储能、分配控制和集成模型，检查连接与模型结构 |
| 核心 | simulating-simulink-models | 同上 | 139 | 1,329 | 使用 SimulationInput 配置三个工况、参数扫描和日志 |
| 核心 | matlab-read-documentation | MathWorks，matlab/matlab-agentic-toolkit | 43 | 1,279 | 按本机版本核对组件与函数，确认参数、单位及兼容性 |
| 辅助 | matlab | K-Dense-AI/scientific-agent-skills | 约 2.1K | 56,534 | 时间序列处理、数值计算、代码审阅和可重现 MATLAB 工作流 |
| 写作阶段 | literature-review | 同上 | 约 2.5K | 56,534 | 检索和组织储能文献，检查 DOI 与证据对应关系 |
| 写作阶段 | scientific-writing | 同上 | 约 2.6K | 56,534 | 组织技术报告，检查方法、结果、图表和引用的一致性 |

MathWorks 三项技能安装量偏低，尤其文档技能低于 100。它们仍列入核心候选，是因为来源和任务匹配度较高，需要在实际环境中验证可用性。K-Dense 的 MATLAB 技能侧重数值工作流，Simulink 模型操作由前两项技能支持。

## 2. 技能用途和依赖审查

### building-simulink-models

内容包括结构修改、块参数、端口与连线、物理连接及模型检查。当前版本使用 `model_edit` 和配套查询/检查工具，依赖 Simulink Agentic Toolkit 与 MATLAB MCP 连接。仅复制技能文件后，其所引用的工具仍需单独配置。适用于集成模型建设阶段。[GitHub 技能原文](https://github.com/matlab/simulink-agentic-toolkit/blob/main/skills-catalog/model-based-design-core/building-simulink-models/SKILL.md)

### simulating-simulink-models

内容包括 `Simulink.SimulationInput`、工况参数覆盖、外部输入、批量仿真与 `logsout` 输出。可用来保证三个工况和参数扫描共享同一模型。并行计算功能需要额外检查工具箱，基础串行仿真可先行验证。[GitHub 技能原文](https://github.com/matlab/simulink-agentic-toolkit/blob/main/skills-catalog/model-based-design-core/simulating-simulink-models/SKILL.md)

### matlab-read-documentation

按本地帮助、产品目录、用户指南和函数参考逐步查询版本对应文档。适合核对超级电容组件、电池模型、求解器与信号输入接口。该技能含 MATLAB/MCP 文档获取流程，运行时需具备相应连接。[GitHub 技能原文](https://github.com/matlab/matlab-agentic-toolkit/blob/main/skills-catalog/matlab-core/matlab-read-documentation/SKILL.md)

### matlab

支持数组、表格和时间数据、图形、项目、测试及 MATLAB/Octave 数值工作流。包含本地静态分析和执行规划工具，部分文档以 R2026a 为基线。可辅助清理风电时间序列、推导能量预算和核对计算。MATLAB 版本与许可证、相关工具箱以及 API 差异需要确认。[GitHub 技能原文](https://github.com/K-Dense-AI/scientific-agent-skills/blob/main/skills/matlab/SKILL.md)

### literature-review

支持检索规划、筛选、证据提取、综合和引用核验。针对本项目应选择电力与控制领域的数据库与来源，如 IEEE Xplore、出版社原文和学校图书馆。其辅助脚本依赖 Python 和网络，PDF 导出另有 Pandoc/XeLaTeX 等依赖，部分可选检索或图形服务需要账号/API。适合整理 12–15 篇候选文献与核实 DOI。[GitHub 技能原文](https://github.com/K-Dense-AI/scientific-agent-skills/blob/main/skills/literature-review/SKILL.md)

### scientific-writing

支持方法、数据和结论的证据追溯，以及引用、图表和报告一致性检查。核心指导跨平台，可选本地检查脚本需要 Python 3.11+。课程报告结构以任务书为依据，选用其与工程报告相关的部分。[GitHub 技能原文](https://github.com/K-Dense-AI/scientific-agent-skills/blob/main/skills/scientific-writing/SKILL.md)

## 3. 安装方案

下列命令供后续安装使用。当前状态为候选调研完成，安装和 MATLAB/MCP 配置待后续实施。

```powershell
npx skills add matlab/simulink-agentic-toolkit --skill building-simulink-models
npx skills add matlab/simulink-agentic-toolkit --skill simulating-simulink-models
npx skills add matlab/matlab-agentic-toolkit --skill matlab-read-documentation
npx skills add K-Dense-AI/scientific-agent-skills --skill matlab
npx skills add K-Dense-AI/scientific-agent-skills --skill literature-review
npx skills add K-Dense-AI/scientific-agent-skills --skill scientific-writing
```

以上为单独添加技能的命令。完整 Simulink 自动化环境优先参考 MathWorks 的 Toolkit 安装器，该流程负责 MCP 和配套工具配置。具体安装范围需要结合本机版本和现有配置确定。[Simulink Toolkit 安装说明](https://github.com/matlab/simulink-agentic-toolkit#readme)

按本次读取的 README，Simulink Toolkit 需要 MATLAB R2023a+ 和 Simulink，额外产品要求需查技能 manifest。MATLAB Toolkit 需要 MATLAB R2021a+。物理电路建模还需要检查 Simscape/Simscape Electrical，自动测试工具的使用需要检查 Simulink Test。[Simulink 环境要求](https://github.com/matlab/simulink-agentic-toolkit#requirements) [MATLAB 环境要求](https://github.com/matlab/matlab-agentic-toolkit#requirements)

本次在 PATH 与 `C:\Program Files\MATLAB` 常见安装目录中未检出 MATLAB，尚不能判断其他位置或 MATLAB Online 的可用情况。当前会话也未发现已配置的 MATLAB/Simulink 专用 MCP 工具，因此运行兼容性仍待验证。

## 4. 建议启用顺序

1. 环境确认后先配置 MathWorks Toolkit，并启用建模、仿真和版本文档三项核心技能。
2. 数值脚本复杂度上升时加入 MATLAB 辅助技能。
3. 文献与报告阶段启用 literature-review 和 scientific-writing。
4. 使用本次已具备的 pdf 技能进行最终 PDF 检查，必要时使用 documents 技能制作可编辑 Word 版本。

安装技能后，需用小型模型验证读取、编辑、保存和仿真，再应用于正式模型。

## 5. 其他检索结果

检索到 `simulink/skills`，由 Guy on Simulink 发布，包含模型交互和求解器分析等技能。其 README 声明该集合属于非官方产品，且依赖 Toolkit。对本阶段的模型建立与工况仿真，优先采用上方 MathWorks 核心技能，后续出现求解器问题时可评估其中的分析技能。[仓库及说明](https://github.com/simulink/skills)

## 6. 来源和复核入口

- MathWorks Simulink Toolkit 仓库、技能目录、依赖及许可证。[GitHub](https://github.com/matlab/simulink-agentic-toolkit)
- MathWorks MATLAB Toolkit 仓库与版本文档技能。[GitHub](https://github.com/matlab/matlab-agentic-toolkit)
- K-Dense 数值、文献及写作技能原仓库。[GitHub](https://github.com/K-Dense-AI/scientific-agent-skills)
- 安装量与目录页。[建模](https://skills.sh/matlab/simulink-agentic-toolkit/building-simulink-models) [仿真](https://skills.sh/matlab/simulink-agentic-toolkit/simulating-simulink-models) [文档](https://skills.sh/matlab/matlab-agentic-toolkit/matlab-read-documentation)
- 安装量与目录页。[MATLAB](https://skills.sh/k-dense-ai/scientific-agent-skills/matlab) [文献](https://skills.sh/k-dense-ai/scientific-agent-skills/literature-review) [写作](https://skills.sh/k-dense-ai/scientific-agent-skills/scientific-writing)

部分 skills.sh 详情页在浏览工具中未能打开，安装量取自实际 Skills CLI 查询，技能内容核验使用 GitHub 原文件。上述推荐均为来源与内容审查结果，实际运行能力需要完成本地环境验证。
