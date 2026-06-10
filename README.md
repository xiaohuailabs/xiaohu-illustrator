# xiaohu-illustrator 小互隐喻配图引擎

一个 Claude Code 技能:为中文深度文/方法拆解/产品解读生成**带固定 IP 角色的正文配图**。不是通用插画,不是样式库随机选风格——是把文章里一个关键判断/流程/机制,变成一张有记忆点、一眼怪但一秒懂的图。

核心方法:**挑认知锚点 → 深层提炼 → 现编隐喻 → 三轨分流 → 反 PPT 自检**。AI 负责画,这套流程负责"想清楚画什么"——后者才是配图的难点。

## 效果

| 3D 盲盒(默认) | 黑白线稿 | 扁平矢量 |
|---|---|---|
| ![3D](examples/皮肤样张/皮肤A-3D盲盒.jpg) | ![黑白](examples/皮肤样张/皮肤B-黑白线稿.jpg) | ![扁平](examples/皮肤样张/皮肤C-扁平矢量.jpg) |

| 编辑插画 | 水彩淡彩 | 马克笔手账 |
|---|---|---|
| ![编辑](examples/皮肤样张/皮肤D-编辑插画.jpg) | ![水彩](examples/皮肤样张/皮肤E-水彩淡彩.jpg) | ![马克笔](examples/皮肤样张/皮肤F-马克笔.jpg) |

同一个角色,7 种画风皮肤(还有一种混合媒介信息图风,见 `references/style-dna.md`)。**角色锁定、画风可换、表情随内容情绪变化**——这是和"每张图风格随机"的根本区别。

## 它解决什么问题

AI 配图的三个常见死法:

1. **画成 PPT**——贴满图标和方框的"专业示意图",读者一张都不会停下来看
2. **风格漂移**——一篇文章 6 张图 6 种画风,像 6 个号拼出来的
3. **图解表面**——文字说"三家竞争"就画三条赛道,没有任何文字之外的信息增量

本技能对应三道防线:反 PPT 负向清单(`anti-ppt-qa.md`)、视觉契约六维锁定(`style-dna.md`)、深层提炼三问+内容锁定(`deep-reading.md`)。

## 安装

```bash
git clone https://github.com/xiaohuailabs/xiaohu-illustrator.git ~/.claude/skills/xiaohu-illustrator
```

重启 Claude Code,对它说"给这篇文章配几张隐喻图"即可触发。

**唯一要自备的依赖**:一个支持「文生图 + 参考图」的生图途径(API 脚本 / MCP 工具都行,推荐 GPT-image 系列或 Gemini)。没有现成的,让 Claude Code 给你写个调图像 API 的小脚本,一次写好反复用。详见 `SKILL.md`「依赖」一节。

## 使用

```
给这篇文章配几张隐喻图: <文章路径>
```

流程(细节见 SKILL.md):

1. **逐节枚举**——文章每一节列进计划表,逐节判"配/不配"+理由,不凭感觉挑
2. **深层提炼**——每个配图点回答:作者真意?张力在哪?读者该留下哪句顿悟?
3. **三轨分流**——没共鸣→情绪图 / 没看懂结构→解释图 / 有转折时间线→四格漫画
4. **shot list 确认**——烧 API 前把整张计划表给你过目
5. **基准图先行**——先生 1 张定调,对了再批量,防全篇风格漂移
6. **QA 自检**——反 PPT 清单逐项核对,命中失败信号就重生

可选参数:`--style 3d/sketch/flat/...`(画风皮肤)、`--ratio 4:3`(强制统一比例)、`--density 精简/均衡/丰富`(配图密度)。

## 把小互换成你自己的角色(建议)

小互(红框眼镜+齐刘海+橙红背带裤+狐狸搭档)是仓库自带的示例 IP,装上就能跑。但**方法可以共享,辨识度只能是你自己的**——三步替换法见 [`references/customize-your-ip.md`](references/customize-your-ip.md):定义角色档案 → 生成你的锚点图 → 替换 prompt 模板 IP 段。

## 方法来源

本技能的方法骨架借鉴自两个项目,完整的"借了什么/没借什么"记录见 [`references/血统.md`](references/血统.md):

- [helloianneo/ian-xiaohei-illustrations](https://github.com/helloianneo/ian-xiaohei-illustrations) —— 认知锚点筛选、原创隐喻三步法、反 PPT 防线的结构
- [JimLiu/baoyu-skills](https://github.com/JimLiu/baoyu-skills) 的 baoyu-article-illustrator —— 文字渲染铁律、结构化 prompt 字段、配图密度参数

小黑的 IP 没有碰(那是 Ian 的招牌),小互是独立设计的角色——也建议你这样对待小互。

## License

MIT(代码与方法文档)。小互 IP 形象仅作示例用途,商用请替换为你自己的角色。
