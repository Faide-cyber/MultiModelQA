#### [English Doc](README.md)

![Static Badge](https://img.shields.io/badge/%40Github-Faide-%2300FFFF) ![Static Badge](https://img.shields.io/badge/Platform-Dify-%238c37dc) ![Static Badge](https://img.shields.io/badge/Version-1.0.0-%23e87435) ![Static Badge](https://img.shields.io/badge/License-GNU3.0-%2314bbc1)

### 1. 项目概述

**MultiModelQA** 是一个基于 Dify 平台构建的多模型并行问答工作流，整合了当前主流的最新 AI 大模型，包括 DeepSeek-V3、Qwen3、Doubao-1.5、Claude-3.7、Gemini-2.5 等，实现单一问题多模型并行回答的功能。用户可以通过一个界面同时获取多个 AI 模型的回答，便于比较和分析不同模型的输出差异。

<img src="./snapshots/MultiModelQA-Demo.png" width="800px">

### 2. 系统架构与功能特点

#### 2.1 核心功能
- **多模型并行回答**：同时调用7个不同AI模型进行问答
- **统一结果展示**：将各模型回答以标准格式整合展示
- **模型对比分析**：便于用户比较不同模型的回答差异
- **可扩展架构**：支持随时添加新的AI模型接入

#### 2.2 集成模型列表
1. DeepSeek-V3 (深度求索)
2. Qwen3 (通义千问)
3. Doubao-1.5-pro-256k (豆包)
4. ChatGPT-o3-mini (OpenAI)
5. Claude-3.7-sonnet (Anthropic)
6. Gemini-2.5-flash (Google)
7. Grok-3-mini-beta (xAI)

### 3. 环境要求与依赖

**Dify 要求**
- Dify 版本 >= 0.13.0 (推荐1.0及以上)
- 已安装以下插件：
  - deepseek 插件
  - openrouter 插件
  - tongyi 插件
  - volcengine_maas 插件

**API 要求**
- 各模型对应的有效API密钥
- 网络连接需能访问各模型API端点

### 4. 安装与部署

#### 4.1 获取工作流文件
- 从本项目下载 `MultiModelQA.yml` 工作流文件

#### 4.2 导入Dify
1. 登录Dify控制台
2. 进入"工作流"页面
3. 点击"导入"按钮，选择下载的YML文件
4. 根据提示完成导入

#### 4.3 配置API密钥
1. 在工作流中配置各模型对应的API密钥
2. 测试连接确保各模型可用

### 5. 使用说明

1. 在Dify应用界面打开MultiModelQA
2. 输入您的问题
3. 系统将并行调用各模型进行回答
4. 结果将以统一格式展示，包含各模型的独立回答

### 6. 开发与扩展

- 核心逻辑集中在工作流设计，可通过Dify可视化编辑器修改
- 如需添加新模型，可在工作流中增加新的LLM节点并配置相应参数
- 回答模板可在Answer节点中自定义修改

### 7. 许可

您可以根据自由软件基金会发布的GNU通用公共许可证的条款进行再分发和/或修改。您可以选择使用第3版许可证，或者任何更高版本的许可证。

本程序是以希望它会有用的方式发布，但不提供任何明示或暗示的保证，包括但不限于适销性或特定用途的适用性。请参阅GNU通用公共许可证以获取更多详细信息。

您应该已经随此程序收到了GNU通用公共许可证的副本。如果没有，请参阅http://www.gnu.org/licenses/。

### 8. 免责声明

**MultiModelQA**（以下简称"本项目"）仅供学习和研究使用，禁止将其用于任何非法用途。如果您选择使用本项目的任何部分，您必须遵守所有相关法律和规定，并承担由此产生的所有责任。

作者不对因使用本项目而导致的任何损失或损害负责。如果您选择使用本项目的任何部分，您应该自己承担所有风险和责任。

本人保留追究任何非法使用本项目的人的法律责任的权利。如果您选择使用本项目的任何部分进行非法活动，您将面临法律诉讼和其他惩罚。

使用者应遵守相关法律法规，尊重作者的知识产权。任何因违反上述规定而引起的法律纠纷，由使用者承担全部责任。

本声明的解释权归作者所有。

### 9. 附加信息

- **最新源码与文档**
   请访问 GitHub 仓库获取最新的源码及文档更新：https://github.com/Faide-cyber/MultiModelQA
- **Dify 相关文档**
   详见 [Dify 官方文档](https://docs.dify.ai/)

### 10. 联系方式

微信或邮箱1350038426@qq.com

如果您有任何问题或疑问，也可以通过提交issue的方式与我进行交流。

在提交issue时，请确保描述清楚您的问题或反馈，并提供足够的上下文信息，以便我能够更好地理解和回答您的问题。

![QQ图片202310251908231](https://github.com/Faide-cyber/MouseCopy/assets/148406475/8b7ac122-d438-4d64-b6d0-330b514e4389)
