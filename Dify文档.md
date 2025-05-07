### 1.0.0 Linux服务器部署

推荐Linux通过宝塔部署 

#### 1.1.0 云服务器 CVM配置

4核8G 带宽5M及以上 长期推荐按年付费 短期按量付费 如果需要本地Ollama模型则所需内存要求更高 可参考相关模型配置要求

地域看自身情况选择 登录密码自己填写

镜像随便选 一会重装系统

<img src="https://github.com/Faide-cyber/MultiModelQA/blob/main/img/image-20250407214625108.png" width="800px">
<img src="https://github.com/Faide-cyber/MultiModelQA/blob/main/img/image-20250407214742723.png" width="800px">
<img src="https://github.com/Faide-cyber/MultiModelQA/blob/main/img/image-20250407214342853.png" width="800px">
<img src="https://github.com/Faide-cyber/MultiModelQA/blob/main/img/image-20250407215104528.png" width="800px">

[云服务器CVM购买_云服务器CVM选购 - 腾讯云](https://buy.cloud.tencent.com/cvm?tab=custom&step=1&devPayMode=hourly&regionId=8&zoneId=800006&instanceType=SA5.LARGE8&dfwbindType=add&loginSet=SET_PASSWORD&platform=TencentOS&imageId=img-6n21msk1&systemDiskType=CLOUD_BSSD&systemDiskSize=50&systemDiskBackupQuota=0&bandwidthType=TRAFFIC_POSTPAID_BY_HOUR&bandwidth=5&wanIp=1&templateCreateMode=createLt&isBackup=false&backupDiskType=ALL&backupDiskCustomizeValue=&backupQuotaSegment=1&backupQuota=1)

检查后购买 跳转至控制台页面

##### 1.1.1 重装系统

点击实例-操作-更多操作-重装系统-公共镜像-选择Ubuntu Server 22.04LTS64位..点击确定等待重装完毕

##### 1.1.2 宝塔面板安装

实例-登录-进入命令行页面 输入命令

```cmd
宝塔面板安装命令：
wget -O install_panel.sh https://download.bt.cn/install/install_panel.sh && sudo bash install_panel.sh ed8484bec
Do you want to install Bt-Panel to the /www directory now?(y/n): y
```

成功后提示相关信息:

```cmd
【云服务器】请在安全组放行 17590 端口  //每个人的此端口不同 酌情修改
外网面板地址:https://119.45.117.64:17590/836acff5
内网面板地址:https://10.286.8.5:17598/8a6acff5
username: haefoya4
password: 966gda45
```

##### 1.1.3 端口放行

后面需要多次端口放行，可一次性配置:

进入实例页面-安全组ID/名称-添加规则

```cmd
类型   来源       协议端口              策略   备注

自定义 0.0.0.0/0  TCP:需要放开的端口号   允许   相关备注
```

除了宝塔放行端口每个人不同外 其他端口可按此写法

<img src="https://github.com/Faide-cyber/MultiModelQA/blob/main/img/image-20250407220657306.png" width="800px">

登录宝塔面板(外网面板地址)，使用cmd给的账号密码登录

绑定宝塔官网账号 没有的去注册一个即可

##### 1.1.4 初始化配置

<img src="https://github.com/Faide-cyber/MultiModelQA/blob/main/img/image-20250407221155800.png" width="800px">

#### 1.2.0 Dify安装

Docker安装完成后 在Docker-应用商店中找到 Dify，点击安装

- 名称：应用名称，默认Dify-随机字符
- 版本选择：默认latest 我使用的是最低版本0.15 最新版本傻逼Bug格外多 
- 域名：如需通过域名直接访问，在此配置域名并将域名解析到服务器 新手不推荐  IP+Port直接访问即可
- 允许外部访问：如需通过IP+Port直接访问，则勾选，如你已经设置了域名，则不要勾选此处
- 端口：默认8088，可自行修改(与开放端口一致 别忘记放行端口)

提交后面板会自动进行应用初始化，大概需要`1-3`分钟，初始化完成后即可访问。

##### 1.2.1 设置管理员账户

```
# 使用域名
http://yourdomain/install

# 使用IP+端口

http://your_server_ip:8088/install
```

Dify 主页面：

```
# 使用域名
http://yourdomain/

# 使用IP+端口

http://your_server_ip:8088
```

##### 1.2.2 设置模型供应商

登录后右上角-设置-填写Deepseek、Ollama等相关模型API Key

去相关开放平台申请API Key

```cmd
https://platform.deepseek.com/
https://openai.com/api/
https://cloud.siliconflow.cn/account/ak
https://console.cloud.tencent.com/lkeap/api
https://platform.baichuan-ai.com/console/apikey
```

##### 1.2.3 创建空白应用

创建应用-右上角设置模型和参数-发布

如果发布后无法访问 添加端口号(8088)后再次尝试 

```cmd
公开访问 URL
http://82.156.34.85/chat/qL3xgqZDevYjXXXL //如果无法访问
http://82.156.34.85:8088/chat/qL3xgqZDevYjXXXL//使用这个
```

如果访问后显示

```cmd
Application error: a client-side exception has occurred (see the browser console for more information)
```

同时控制台F12报错 显示

```js
TypeError: e.toReversed is not a function
```

则可能为浏览器兼容问题 Edge和微信端浏览器可以正常使用，Firefox、SLBrowser则不行 使用Edge即可

[宝塔面板部署 | Dify](https://docs.dify.ai/zh-hans/getting-started/install-self-hosted/bt-panel)

**知识库相关内容参考2.3.0**

#### 1.3.0 接入企业微信

##### 1.3.1 Dify开放API

Dify发布应用后开启 后端服务 API

复制API 访问凭据(里面加入端口 否则访问失败 如果有域名的话就没这事😅)和API 密钥 后面要用

```cmd
http://服务器ip:8088/v1        //API 访问凭据 
app-XXXXXXXXXaxavJ5uwSZTO7kM  //API 密钥
```

##### 1.3.2 企业微信应用创建

打开[企业微信](https://work.weixin.qq.com/wework_admin/register_wx?from=myhome)界面注册企业注册 点击应用管理，创建应用，填写机器人基本信息

##### 1.3.3 获取corpid

点击我的企业[企业微信](https://work.weixin.qq.com/wework_admin/frame#/profile)复制企业 ID(也叫corpid)

```cmd
ww760131bb8307exxx
```

点击安全与管理-管理工具-通讯录同步，然后开启接口同步

##### 1.3.4 获取contacts_secret

获取通讯录 Secret(也叫contacts_secret)

```cmd
Qa1hfTTLkWgYlMGD550kIiNSrxkm8dXBuOOXXXIcw74
```

配置企业可信 IP，填入服务器的公网 ip 比如82.156.35.35

##### 1.3.5 获取secret

点击应用管理-查看机器人的 Secret(也叫secret)

```cmd
m5Mf3E8X2iH8ZxiBASNy3gm3cbmF2OPjuIHBJZ2YXXX
```

##### 1.3.6 设置API接收

点击下方的接收消息，设置API接收

URL 填写示例：http://服务器的公网IP:2290/callback/command

Token，点击随机获取，记录下来得到 Token

EncodingAESKey，点击随机获取，记录下来得到 EncodingAESKey

```cmd
Token  v1tTV3AQVLkoJk6IDXXXX
EncodingAESKey  eNhwmn1X7W9t4OSJCA3W6cyMtJY1jFnncbXXXXRBFE3
```

⚠️⚠️⚠️注意：此时不要点保存！

##### 1.3.7 安装LangBot

在Docker-应用商店中找到 LangBot，点击安装(记得放行5300和2290端口)

打开LangBot页面-消息平台配置(platform.json)-消息平台适配器-企业微信填入-开启消息接收器(enable按钮)

<img src="https://github.com/Faide-cyber/MultiModelQA/blob/main/img/image-20250407231750021.png" width="800px">

应用后宝塔重启LangBot，点击企业微信保存按钮检测是否连接成功

点击下方的企业可信IP 填入你服务器的公网 ip 比如82.156.35.35



目前仅仅连接，还不能回答 

##### 1.3.8 dify接入消息平台

进入LangBot页面

<img src="https://github.com/Faide-cyber/MultiModelQA/blob/main/img/image-20250407232402782.png" width="800px">

修改请求运行器为

```cmd
dify-service-api
```

Dify Service API配置

<img src="https://github.com/Faide-cyber/MultiModelQA/blob/main/img/image-20250407232605677.png" width="800px">

重启LangBot即可连接成功

##### 1.3.9 设置管理员会话

发送一条消息进入LangBot页面 查看日志

<img src="https://github.com/Faide-cyber/MultiModelQA/blob/main/img/image-20250407233250635.png" width="800px">

复制用户名 进入设置-system.json-管理员会话添加即可

[宝塔面板部署 | LangBot 文档](https://docs.langbot.app/deploy/langbot/one-click/bt.html)

[部署企业微信机器人 | LangBot 文档](https://docs.langbot.app/deploy/platforms/wecom/wecom)



### 2.0.0 windows本地部署

#### 2.1.0 使用本地模型(不推荐 除非配置够用)

##### 2.1.1 下载ollama

```cmd
https://ollama.com/
```

检测是否安装成功

```cmd
ollama -v
```

本机电脑如果要映射到公网需要配置环境变量 用户/系统都行

```text
变量名(N):OLLAMA_HOST
变量值(V):0.0.0.0

变量名(N):OLLAMA_ORIGINS
变量值(V):*
```

ollama注意下载模型时版本一定符合要求,例如拉取embedding模型[dmeta-embedding-zh](https://ollama.com/shaw/dmeta-embedding-zh)时要求

```
Note: This model requires ollama version 0.5.4 or later. It can only be used to generate embeddings.
```

```cmd
ollama -v
ollama version is 0.1.32
//版本过低模型可以在ollama下载,但是无法使用,集成到cherry studio中报错:获取嵌入维度失败404
```

##### 2.1.2 拉取本地模型

选择合适参数大小 搜具体模型的所需配置 

默认下载至C盘 可通过修改环境变量的方式移到D盘 

```text
变量名(N):OLLAMA_MODELS
变量值(V):存放模型位置
```

拉取chat模型

```cmd
ollama run deepseek-r1:32b
```

Text embedding模型(选择合适参数大小)

```cmd
ollama pull bge-m3
```

##### 2.1.3 Docker配置

安装docker Desktop(参考版本24.0.6)，安装docker-compose(v2.22.0-desktop.2)，配置镜像源(找能用的)。

```cmd
https://www.docker.com/
```

```cmd
{
  "builder": {
    "gc": {
      "defaultKeepStorage": "20GB",
      "enabled": true
    }
  },
  "experimental": false,
  "registry-mirrors": [
    "https://docker.m.daocloud.io"
  ]
}
```

如果Windows Docker中有多个容器需要禁止Docker Desktop打开后自启动

```cmd
docker update --restart=no <容器名或ID>
```

##### 2.1.4 安装Dify

(默认端口 80，可对接Ngrok进行内网穿透)

[Docker Compose 部署 | Dify](https://docs.dify.ai/zh-hans/getting-started/install-self-hosted/docker-compose)

克隆 Dify 源代码至本地环境/Download zip也行

```cmd
# 假设当前最新版本为 0.15.3  我的是1.1.3
git clone https://github.com/langgenius/dify.git --branch 0.15.3
```

启动 Dify

进入 Dify 源代码的 Docker 目录 cmd

设置Dify访问Ollama的服务

dify/docker/.env文件末添加

```cmd
#启用自定义模型
CUSTOM_MODEL_ENABLED=true
#指定ollama的API地址 根据部署调整ip
OLLAMA_API_BASE_URL=host.docker.internal:11434
```

cmd启动 Docker 容器(第一次使用cmd打开 ，后续可以使用docker Desktop打开)

```cmd
如果版本是 Docker Compose V2，(目前是V2)使用以下命令：
docker compose up -d
如果版本是 Docker Compose V1，使用以下命令：
docker-compose up -d
```

运行命令后，会显示所有容器的状态和端口映射

```cmd
[+] Running 11/11
 ✔ Network docker_ssrf_proxy_network  Created                                                                 0.1s 
 ✔ Network docker_default             Created                                                                 0.0s 
 ✔ Container docker-redis-1           Started                                                                 2.4s 
 ✔ Container docker-ssrf_proxy-1      Started                                                                 2.8s 
 ✔ Container docker-sandbox-1         Started                                                                 2.7s 
 ✔ Container docker-web-1             Started                                                                 2.7s 
 ✔ Container docker-weaviate-1        Started                                                                 2.4s 
 ✔ Container docker-db-1              Started                                                                 2.7s 
 ✔ Container docker-api-1             Started                                                                 6.5s 
 ✔ Container docker-worker-1          Started                                                                 6.4s 
 ✔ Container docker-nginx-1           Started                                                                 7.1s
```

管理员设置页面(第一次需要设置)

```cmd
http://localhost/install
```

Dify主页面

```cmd
http://localhost/apps
```

##### 2.1.5 Dify连接Ollama

Dify主界面-右上角模型设置-模型供应商Ollama

基础URL

```text
http://host.docker.internal:11434
```

模型名称(通过cmd查看)

```cmd
ollama list
```

连接成功即可创建应用进行使用

#### 2.2.0 使用模型供应商模型

##### 2.2.1 Docker配置

安装docker Desktop(参考版本24.0.6)，安装docker-compose(v2.22.0-desktop.2)，配置镜像源，不再赘述。

##### 2.2.2 安装Dify

(默认端口 80)

[Docker Compose 部署 | Dify](https://docs.dify.ai/zh-hans/getting-started/install-self-hosted/docker-compose)

克隆 Dify 源代码至本地环境/Download zip也行

```cmd
# 假设当前最新版本为 0.15.3
git clone https://github.com/langgenius/dify.git --branch 0.15.3
```

启动 Dify

进入 Dify 源代码的 Docker 目录

```cmd
cd dify/docker
```

cmd启动 Docker 容器(第一次使用cmd打开 ，后续可以使用docker Desktop打开)

```cmd
如果版本是 Docker Compose V2，使用以下命令：
docker compose up -d
如果版本是 Docker Compose V1，使用以下命令：
docker-compose up -d
```

运行命令后，会显示所有容器的状态和端口映射

```cmd
[+] Running 11/11
 ✔ Network docker_ssrf_proxy_network  Created                                                                 0.1s 
 ✔ Network docker_default             Created                                                                 0.0s 
 ✔ Container docker-redis-1           Started                                                                 2.4s 
 ✔ Container docker-ssrf_proxy-1      Started                                                                 2.8s 
 ✔ Container docker-sandbox-1         Started                                                                 2.7s 
 ✔ Container docker-web-1             Started                                                                 2.7s 
 ✔ Container docker-weaviate-1        Started                                                                 2.4s 
 ✔ Container docker-db-1              Started                                                                 2.7s 
 ✔ Container docker-api-1             Started                                                                 6.5s 
 ✔ Container docker-worker-1          Started                                                                 6.4s 
 ✔ Container docker-nginx-1           Started                                                                 7.1s
```

管理员设置页面(第一次需要设置)

```cmd
http://localhost/install
```

Dify主页面

```cmd
http://localhost/apps
```

##### 2.2.3 Dify接入模型

去相关开放平台申请API Key

```cmd
https://platform.deepseek.com/
https://openai.com/api/
https://cloud.siliconflow.cn/account/ak
https://console.cloud.tencent.com/lkeap/api
https://platform.baichuan-ai.com/console/apikey
```

注意这里OpenAI API≠OpenAI的接口 腾讯云LKE的API≠腾讯混元API 

知识库效果上Chatbox<AnythingLLM≈Cherry Studio≈阿里云≈火山云<Dify<腾讯云LKE

但腾讯云LKE目前无法使用OpenAI API兼容的接口,只能通过WebSocket或SSE，测试发现耗费Token过多

相关文档

```cmd
https://cloud.tencent.com/document/product/1759/109380
https://cloud.tencent.com/online-service/faq?extraId=angpt-scs_faq_data_http_similarity-432996&from=sales_doc_1759&source=PRESALE&noTopNav=false&noFooter=true&noFloatBar=true
https://api-docs.deepseek.com/zh-cn/quick_start/pricing
https://openai.com/api/pricing/
```

Dify主界面-右上角模型设置-模型供应商

连接成功即可创建应用进行使用



#### 2.3.0 知识库嵌入

需要提前有一个Text Tmbedding模型或Reranker模型(无论是否本地，不同模型分段效果不同)

中文支持优先：Baichuan Text Embeddings或M3E（Moka Massive Mixed Embedding）(截止到2025.4)

数据隐私优先：采用M3E或Text2Vec本地部署

可参照C-MTEB查看相关表现

```cmd
https://huggingface.co/models?pipeline_tag=question-answering&language=zh
```

Reranker模型也可以用

推荐bge-reranker-v2

设置-模型供应商-系统模型设置-Embedding 模型

##### 2.3.1 RAG对话架构

<img src="https://github.com/Faide-cyber/MultiModelQA/blob/main/img/v2-d00d6b7ca7b1045f965e3eb74248c618_r-17437809903552-17438250691731.jpg" width="800px">


流程类文件尽量少分段 政策类文件多分段 推荐使用工作流或工具插件 可以提升检索精度

分段越少检索后耗费Token越多

txt=word>pdf>图片，最好使用文本形式的数据集

最影响数据回答质量的有 

- 分段标识符 
- Embedding模型选择 推荐商用模型
- 检索设置 推荐混合检索的Rerank模型
- 索引方式 推荐高质量 
- 应用提示词 
- 分段模式 推荐父子分段
- 对话模型温度(降低温度值（如0.3）可减少随机性，适用于需要确定性输出的场景)

Top K：召回片段数量

Score阈值：每次召回都有score得分 得分越高即正相关 Score阈值可以取消输出小于得分下的片段

相关文档

```cmd
https://www.pinecone.io/learn/chunking-strategies/

https://z0yrmerhgi8.feishu.cn/wiki/PiHWwkd3FioX5pkMvuvc5M6Wn6f

https://docs.dify.ai/zh-hans/guides/knowledge-base/create-knowledge-and-upload-documents/setting-indexing-methods

https://docs.dify.ai/zh-hans/guides/knowledge-base/create-knowledge-and-upload-documents/chunking-and-cleaning-text

https://api-docs.deepseek.com/zh-cn/quick_start/parameter_settings

```

##### 2.3.2 知识库创建

知识库-创建知识库-上传文本文件-进行相关设置-保存并处理

使用召回测试查询文本测试知识的召回效果



