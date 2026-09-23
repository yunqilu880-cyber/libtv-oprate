# LibTV + Codex + Edge Browser Automation Plan

## 目标

建立一个半自动化 AI 漫剧制作工作流：

剧本 + 资产库 + 制作规范

↓

Codex 分析与规划

↓

生成 LibTV 可执行任务

↓

（未来）通过浏览器自动化操作 Edge / LibTV

↓

生成视频素材

↓

人工审核

---

# 一、总体原则

不要一开始让 Codex 完全控制 LibTV。

第一阶段目标：让 Codex 成为 AI 制片助手，而不是鼠标机器人。

原因：

- AI 可以快速处理结构化信息
- AI 可以生成 Prompt
- AI 可以整理资产
- 但是视频质量判断需要人工参与

自动化顺序：

1. 剧本分析自动化
2. 镜头拆解自动化
3. 资产匹配自动化
4. Prompt生成自动化
5. LibTV操作半自动化
6. 最终审核人工完成

---

# 二、项目文件结构

## 输入资料

包括：

- 剧本文件
- 人物资产库
- 场景资产库
- 物品资产库
- 声音资产库
- 制作规范

资产库说明：

Excel/CSV主要用于管理，不直接作为视频素材输入。

图片资产需要单独整理：

```
assets/
├── characters/
├── scenes/
├── props/
└── voices/
```

---

# 三、Codex第一阶段工作流程

## Step 1：读取项目资料

Codex需要读取：

- project overview
- script
- asset mapping
- workflow规则

输出：

- 故事结构分析
- 主要人物列表
- 场景列表
- 道具列表

---

## Step 2：镜头拆解

每个镜头输出：

- 镜头编号
- 时长
- 景别
- 运镜
- 场景
- 人物
- 道具
- 对白
- 视频生成Prompt

示例：

```
镜头001
时间：0-3秒
场景：现代大学课堂
人物：教授、学生
景别：远景
运镜：缓慢推进
目标：建立现代课堂环境
```

---

# 四、LibTV操作自动化方案

## 技术路线

推荐：

Codex
↓
Python
↓
Playwright
↓
Microsoft Edge
↓
LibTV网页

Playwright负责：

- 打开网页
- 输入Prompt
- 上传素材
- 点击生成
- 下载结果

---

# 五、浏览器自动化环境

## 安装

Python：

```
pip install playwright
```

安装浏览器驱动：

```
playwright install
```

---

# 六、Edge控制方式

使用本机Edge：

Windows路径示例：

```
C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe
```

Playwright配置：

```python
browser = p.chromium.launch(
    executable_path="Edge路径",
    headless=False
)
```

---

# 七、自动化执行流程

## 阶段1：人工确认

人工完成：

- 登录LibTV
- 确认账号
- 检查资产

---

## 阶段2：Codex生成任务

Codex输出：

```
任务1：上传子产角色资产
任务2：上传郑国铸造作坊场景
任务3：输入镜头Prompt
任务4：生成视频
```

---

## 阶段3：Playwright执行

自动完成：

- 点击上传按钮
- 选择文件
- 填写Prompt
- 提交生成

---

# 八、质量检查

自动化完成后必须检查：

## 人物一致性

- 五官是否变化
- 服装是否变化
- 年龄是否变化

## 场景一致性

- 朝代是否正确
- 建筑是否符合时代
- 是否出现现代元素

## 视频质量

- 是否闪烁
- 是否变形
- 是否出现乱码
- 是否有错误文字

---

# 九、《子产》项目测试流程

第一次测试不要生成完整视频。

只测试三个镜头：

1. 现代课堂
2. 郑国铸造作坊
3. 郑国官署

确认：

- 风格统一
- 人物稳定
- Prompt有效

再扩大生产。

---

# 十、未来Agent目标

最终希望实现：

用户输入：

“制作《子产》第三幕"

Agent自动：

1. 读取剧本
2. 查找资产
3. 生成镜头表
4. 生成Prompt
5. 调用LibTV
6. 输出视频

但在早期阶段，必须保留人工审核环节。