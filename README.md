# MultiModelQA

#### [中文文档](https://github.com/Faide-cyber/MultiModelQA/README_ch.md)

![Static Badge](https://img.shields.io/badge/%40Github-Faide-%2300FFFF) ![Static Badge](https://img.shields.io/badge/Platform-Dify-%238c37dc) ![Static Badge](https://img.shields.io/badge/Version-1.0.0-%23e87435) ![Static Badge](https://img.shields.io/badge/License-GNU3.0-%2314bbc1)

### 1. Project Overview

**MultiModelQA** is a parallel multi-model question answering workflow built on the Dify platform. It integrates the latest mainstream AI models including DeepSeek-V3, Qwen3, Doubao-1.5, Claude-3.7, Gemini-2.5, and more, enabling simultaneous multi-model responses to a single question. Users can compare and analyze the outputs of different AI models through a unified interface.

Moreover, MultiModelQA offers high extensibility. Developers can expand the workflow according to specific needs, such as:

* **Answer Integration and Optimization**: Using Dify's variable aggregator and Jinja2 templates, developers can merge responses from multiple models into a more comprehensive and accurate final answer.

* **Dynamic Model Selection**: By utilizing Dify's conditional logic nodes (e.g., IF/ELSE), developers can automatically route questions to the most suitable model based on the question type.

* **Custom Tool Integration**: Dify supports external APIs and custom functions as tool nodes, allowing for powerful workflow extensions.

* **Parallel Processing and Performance Optimization**: With parallel branches, Dify enables concurrent calls to multiple models, significantly improving response speed and throughput.

These features make MultiModelQA not only suitable for standard QA tasks but also flexible enough for building smarter and more efficient question answering systems.

<img src="https://github.com/Faide-cyber/MultiModelQA/blob/main/images/Demo.png" width="800px">

### 2. Architecture & Key Features

#### 2.1 Core Features

* **Parallel QA Across Models**: Simultaneously queries 7 different AI models
* **Unified Result Presentation**: Responses from all models are displayed in a standard format
* **Comparison and Analysis**: Easily compare differences in model outputs
* **Extensible Design**: Add new AI models as needed

#### 2.2 Integrated Models

1. DeepSeek-V3
2. Qwen3 (Tongyi)
3. Doubao-1.5-pro-256k
4. ChatGPT-o3-mini (OpenAI)
5. Claude-3.7-sonnet (Anthropic)
6. Gemini-2.5-flash (Google)
7. Grok-3-mini-beta (xAI)

### 3. Environment & Dependencies

**Dify Requirements**

* Dify version >= 0.13.0 (v1.0+ recommended)
* Required plugins:

  * deepseek
  * openrouter
  * tongyi
  * volcengine\_maas

**API Requirements**

* Valid API keys for each model
* Network access to each model’s API endpoint

### 4. Installation & Deployment

#### 4.1 Get the Workflow File

* Download the `MultiModelQA.yml` file from this repository.

#### 4.2 Import into Dify

1. Log in to your Dify dashboard.
2. Go to the "Workflows" page.
3. Click "Import" and select the downloaded YML file.
4. Follow the prompts to complete the import.

#### 4.3 Configure API Keys

1. Set the API key for each model in the workflow settings.
2. Test connections to ensure all models are functional.

### 5. Usage Guide

1. Open MultiModelQA in the Dify app interface.
2. Enter your question.
3. The system will call all models in parallel to generate responses.
4. Answers will be displayed in a unified format for easy comparison.

### 6. Development & Customization

* Core logic is defined within the workflow design.
* New models can be added by inserting new LLM nodes and configuring them.
* Output formatting templates can be customized within the Answer node.

### 7. License

This project is distributed under the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but **without any warranty**; without even the implied warranty of **merchantability** or **fitness for a particular purpose**. See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with this program. If not, see [http://www.gnu.org/licenses/](http://www.gnu.org/licenses/).

### 8. Disclaimer

**MultiModelQA** is provided for educational and research purposes only. It must not be used for any illegal purposes. If you choose to use any part of this project, you are responsible for complying with all applicable laws and regulations.

The author is not liable for any loss or damage arising from the use of this project. If you choose to use any part of this project, you do so at your own risk.

The author reserves the right to take legal action against any unauthorized or illegal use of this project.

Users must comply with applicable laws and respect the author's intellectual property rights. All legal disputes arising from violations will be the sole responsibility of the user.

The author reserves the right to the final interpretation of this disclaimer.

### 9. Additional Information

* **Latest Source & Docs**
  Visit the GitHub repo for the latest updates: [https://github.com/Faide-cyber/](https://github.com/Faide-cyber/)

* **Dify Documentation**
  See [Dify Official Docs](https://docs.dify.ai/)

### 10. Contact

WeChat or Email: [1350038426@qq.com](mailto:1350038426@qq.com)

For any questions or issues, feel free to [open an issue](https://github.com/Faide-cyber/MultiModelQA/issues).

When submitting an issue, please provide a clear description and sufficient context so that I can better understand and respond.

![QQ Contact Image](https://github.com/Faide-cyber/MouseCopy/assets/148406475/8b7ac122-d438-4d64-b6d0-330b514e4389)

