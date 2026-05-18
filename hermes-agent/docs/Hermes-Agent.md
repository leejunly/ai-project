<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778683022197-01a8457b-d61c-41dc-80b0-ea66a8cad89e.png)

# <font style="color:rgb(24, 25, 28);">1 简单介绍</font>
Hermes Agent 是 NousResearch 开源的 Al Agent 框架，相比 OpenClaW，其亮点在于：配置友好、多模型路由、记忆系统完善、自动沉淀技能，且使用国内模型（如 Qwen 系列）也能稳定运行<font style="color:rgb(24, 25, 28);">，其有以下显著的优点：</font>

<font style="color:rgb(24, 25, 28);">1、token消耗较少</font>

<font style="color:rgb(24, 25, 28);">2、持久的记忆能力（能够长期记忆并且“自我进化”）</font>

<font style="color:rgb(24, 25, 28);">3、内置自我学习循环</font>

**<font style="color:#74B602;">（1）自动从交互中生成skill：自动将有价值的操作流程总结固化为可复用的技能  *</font>**

<font style="color:rgb(24, 25, 28);">（2）在使用中持续迭代技能</font>

**<font style="color:#74B602;">（3）主动持久化知识和用户偏好 *</font>**

<font style="color:rgb(24, 25, 28);">（4）跨会话构建对用户的深度理解</font>

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778940063920-563f446b-194a-49f5-b8b8-5d16c8098395.png)

# <font style="color:rgb(24, 25, 28);">2 官网地址</font>
## <font style="color:rgb(24, 25, 28);">2.1 官方地址</font>
<font style="color:rgb(24, 25, 28);">github地址：https://github.com/nousresearch/hermes-agnet</font>

<font style="color:rgb(24, 25, 28);">官网地址：https://hermes-agent.nousresearch.com</font>

# <font style="color:rgb(24, 25, 28);">3 安装</font>
## <font style="color:rgb(24, 25, 28);">3.1 前提条件</font>
<font style="color:rgb(24, 25, 28);">（1）安装</font>**<font style="color:rgb(28, 30, 33);">git</font>**

<font style="color:rgb(24, 25, 28);">（2）安装</font>**<font style="color:rgb(28, 30, 33);">WSL2（win下的Linux子系统）</font>**<font style="color:rgb(24, 25, 28);">，hermes-agent不支持原生win（可能现在已经支持，但仍在早期beta测试阶段，有很多bug，不建议用），需要借助wsl2安装运行：</font>

<font style="color:rgb(24, 25, 28);">安装wsl： </font>`<font style="color:rgb(24, 25, 28);">wsl --install</font>`

<font style="color:rgb(24, 25, 28);">安装Ubuntu系统：</font>`<font style="color:rgb(24, 25, 28);">wsl --install -d Ubuntu-24.04</font>`<font style="color:rgb(24, 25, 28);"> 如果提示</font><font style="color:rgba(0, 0, 0, 0.85);background-color:rgba(0, 0, 0, 0.04);">无效的分发名称: “Ubuntu-24.04”</font><font style="color:rgb(24, 25, 28);">，则执行： </font>`<font style="color:rgb(24, 25, 28);">wsl </font><font style="color:rgb(0, 0, 0);background-color:rgba(0, 0, 0, 0);">--</font><font style="color:rgb(24, 25, 28);">install </font><font style="color:rgb(0, 0, 0);background-color:rgba(0, 0, 0, 0);">-</font><font style="color:rgb(24, 25, 28);">d Ubuntu</font>`<font style="color:rgb(24, 25, 28);">  安装最新版本</font>

<font style="color:rgb(24, 25, 28);">查看安装结果：</font>`<font style="color:rgb(24, 25, 28);">wsl --list --verbose</font>`

<font style="color:rgb(24, 25, 28);">如下图表示安装成功：</font>

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778685440826-bbc28ba7-203c-4b41-bed6-0802b0348e2b.png)

（3）安装完wsl后， 软件源还没更新 ，需先进行更新：

`<font style="color:rgb(0, 0, 0);background-color:rgba(0, 0, 0, 0);">sudoapt</font> update <font style="color:rgb(0, 0, 0);background-color:rgba(0, 0, 0, 0);">&&sudoapt</font> upgrade <font style="color:rgb(0, 0, 0);background-color:rgba(0, 0, 0, 0);">-y</font>`

## 3.2 安装hermes-agent
1、安装命令

`curl -fsSL [https://raw.githubusercontent.com/NousResearch/hermes-agent/main/scripts/install.sh](https://raw.githubusercontent.com/NousResearch/hermes-agent/main/scripts/install.sh) | bash`

或

`curl -fsSL [https://hermes-agent.nousresearch.com/install.sh](https://hermes-agent.nousresearch.com/install.sh) | bash`

2、安装前先还原pip和npm的镜像源（否则安装会很慢）

（1）查询备份当前源：

查询pip源：`pip config list`

global.extra-index-url='[https://download.pytorch.org/whl/cu118'](https://download.pytorch.org/whl/cu118')

global.index-url='[https://pypi.tuna.tsinghua.edu.cn/simple'](https://pypi.tuna.tsinghua.edu.cn/simple')

global.timeout='120'

global.trusted-host='pypi.tuna.tsinghua.edu.cn\ndownload.pytorch.org'

<font style="color:rgb(0, 0, 0);background-color:rgba(0, 0, 0, 0);">查询pip源：</font>`<font style="color:rgb(0, 0, 0);background-color:rgba(0, 0, 0, 0);">npm</font> config get registry` 

[https://registry.npmmirror.com](https://registry.npmmirror.com)

（2）还原

pip config unset global<font style="color:rgb(0, 0, 0);background-color:rgba(0, 0, 0, 0);">.</font>index-url  

<font style="color:rgb(0, 0, 0);background-color:rgba(0, 0, 0, 0);">npm</font> config <font style="color:rgb(0, 0, 0);background-color:rgba(0, 0, 0, 0);">set</font> registry https://registry.npmjs.org/ 

3、输入Y，选择安装 ripgrep ffmpeg

## 3.3 配置
1、快速配置

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778687879018-c3e76629-e36c-4212-9094-50bd56c0f9f0.png)

2、选择模型

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778688026622-4d9315c4-9047-4bad-9d49-e09a75f94dfc.png)

选择deepseek-v4-pro（不支持多模态）

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778688433654-68f921af-5141-46c7-807c-e30d87fd5c01.png)

## 3.4 启动
<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778688669236-b75fd2e5-a093-40c8-9b85-f3a0de819823.png)

启动：`hermes`，启动成功，会显示如下界面，包括内置tool、skill、当前模型等信息，ctrl+c退出

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778688916450-596ea962-1bfd-493c-8e62-a6f3f65ebcf3.png)

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778689020960-c4334cb1-9c93-434f-b97f-36a05b14d5a7.png)

## 3.5 配置接入微信/飞书/QQ等
启动hermes agent：在cmd输入`wsl`，进入<font style="color:rgb(24, 25, 28);">Ubuntu系统，输入</font>`<font style="color:rgb(24, 25, 28);">hermes gateway setup</font>`<font style="color:rgb(24, 25, 28);">开始配置接入社交APP，我们选择接入微信：</font>

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778769925875-e16e1d8b-deee-4b38-b104-b2b5849dcc0d.png)

接下来会遇到缺少二维码生成类库的问题，直接打开链接，再扫码即可：

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778770844901-c1d3b94d-3a85-43a4-bf5f-7d848f9f013f.png)

后续，一路按照推荐（recommend）的安装就行

启动网关：`hermes gateway run`

此时会受到一个配对信息：

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778772218009-7cb6bcd6-bd61-439b-8f21-dd5b71fd43e7.png)

命令行也会有配对提示：

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778772243367-9b4d45ff-ceb8-4f07-b8af-0ec26f6f0b8f.png)

执行：`<font style="color:rgb(53, 53, 53);background-color:rgb(249, 249, 249);">hermes pairing approve weixin ZCH6CAV3</font>`<font style="color:rgb(53, 53, 53);background-color:rgb(249, 249, 249);">配对</font>

配对成功：

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778772313407-7287ade2-5da9-4db8-9657-8ad178a76afe.png)

重启网关（后台启动），先关闭：`<font style="color:rgb(0, 0, 0);background-color:rgba(0, 0, 0, 0);">pkill -f "hermes gateway run"</font>`

再启动：

`nohup hermes gateway run > /dev/null 2>&1 &`

或者直接重启：`hermes gateway restart`

开始干活：

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778775171053-857a7a49-bdac-4cd8-99b2-e2199b2013b6.png)

完成：

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778774799859-e9f69181-b170-494a-bdc9-82b0ca49b6fd.png)

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778856369768-0e7898df-dbe3-4c94-a58a-efacee436d6a.png)

# 4 简单案例
使用如下prompt，制作一个静态网页：

帮我上网看下最近比较火热的Agent有哪些？然后总结成文档，注意文档中要附上和这个技术相关的重要链接，例如：官网网站，重要博客，GitHub等。

接着，帮我生成一个静态页面，专门用来展示这个文档。网页要有科技感，告诉我资源存放在哪里，帮我在本地启动这个前端页面。

生成过程：

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778858840704-ce43f426-1d44-412b-9a2a-a55d472c0b17.png)

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778858863689-a91cbfce-5a9e-4882-af0f-4996f365d61e.png)

效果演示：

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778858890948-077d88eb-1158-4e2a-a6f6-8e7f9df3de11.png)

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778858928091-2805c46f-7add-4ee4-826b-2600b48effde.png)

# 5 工具和工具集
常见工具：

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778915762446-90ad7713-2fae-460d-8776-eefa39c3ddbc.png)

使用工具：

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778915884507-e1d4b25c-6217-43ba-88bb-1b2c1f43e52f.png)

配置工具集（为所有平台配置）：`hermes tools`

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778918501079-607f5a3c-87aa-4a77-ae53-4b5e709680e7.png)

可用工具列表，选择并回车后配置完成：

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778918539514-415309e2-0860-46c4-93d6-46b0678f3e6b.png)

交互式启用或关闭工具：

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778918826353-d935caef-dfd5-4d02-9365-22c88aa538d8.png)

# 6 skills
所在目录：~/.hermes/skills/

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778919120438-289f8594-cd5d-4ec5-af6a-102c46cd8625.png)

查看已存在的技能：`hermes skills list`

Source：builtin 安装时自带的；local：自主生成的

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778919314157-b9609d5c-15ea-4ab2-9802-510186756838.png)

浏览官方技能列表：

分页查询第2也技能列表：`hermes skills browse --page 2`

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778919855457-9412d080-9894-45b9-a3b9-ad15a00d60a5.png)

搜索并安装skills：

`hermes skills search`

`hermes skills install`

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778919911914-2d931ef4-0fd1-4e81-ac6f-d7d188571786.png)

创建skill：

在win文件系统地址使用`\\wsl$`，进入Ubuntu，将自己的skill放入某个分类中，如：creative

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778920480530-9ce6bb79-3e4e-40a5-8eff-9662ce5307a2.png)

如图已经放入正确：

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778921194002-63556a8d-65a8-4216-ad74-4871d0dc178a.png)

重新启动，验证skill

默认城市天气

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778921978647-0c30efca-a738-48fd-bb0f-bafcfdf661e8.png)

指定城市天气，使用的skill中的天气查询接口：

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778922082434-5dc866f0-a8c0-4757-9d64-8b52548153a7.png)

# 7 mcp及扩展AI工具能力
## 7.1 内置+可扩展能力
<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778926136385-689043cf-edc5-4775-90df-4744461a5440.png)

## 7.2 Stdio服务器（本地）
<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778926418441-e147ab4f-5ef2-4787-80e4-4951a45bde98.png)

配置github mcp：

```yaml
# ~/.hermes/config- yaml
# ghp_Xxx为github的developer token
mcp_servers:
  github:
    command: "npx"
    args: ["-y","@modelcontextprotocol/server-github"]
    env:
      GITHUB_PERSONAL_ACCESS_TOKEN: "ghp_Xxx'
```

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778928927310-43df4d92-28dd-445b-a129-094992a22b44.png)

验证mcp：

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778929264496-3f2b75b3-750f-43bc-b50c-6047ea5dc603.png)

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778929306067-2c26f6ca-9a8e-4efa-8b9f-c8a17ca2a775.png)

## 7.4 常见的mcp
## 服务器推荐
<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778929176797-715d0772-795e-4b71-a112-37fac8362a6a.png)

## 7.3 http服务器（远程）
<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778926680685-0e2cc7b5-7a85-4dd5-ac2d-852d55a3b6e1.png)

# 8 持久记忆能力
## 8.1 hermes agent拥有受限且经过精选的记忆
Hermes Agent 拥有受限且经过精选的记忆，**<font style="color:#74B602;">这些记忆可以跨会话持久存在</font>**。这使得它能够记住你的偏好、你的项目、你的环境以及它所学到的知识。

## 8.2 持久记忆原理
<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778923144682-31b8d06c-dd8c-476c-9420-f356176a714f.png)

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778923885670-bf0a2906-1dd7-4f90-af80-a66fb24e6721.png)

MEMORY.md是自带的，USER.md是随着用户规定偏好后生成的：

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778923585580-f470bb3e-4a45-469c-af75-14efeb84dafd.png)

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778924602545-2948487a-7374-4c03-9b00-d014d4a3b29c.png)

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778924616573-51a84f4e-54a3-4667-8b73-b8b707b066fd.png)

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1779023630278-903c5ea6-9148-4623-abf3-b3500d2c5dc2.png)

memory操作：

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778924555013-f646a067-3d0f-408a-9919-c68a872a969b.png)

## 8.3 记忆内容如何出现在系统提示词中
<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778925418473-dbb4c9d2-02c7-4a93-807b-7cefa3f51c9a.png)

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778925455147-bfe1b371-03ac-4547-b39e-e49564ec480a.png)

## 8.4 记忆文件内容存取原则
<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778924851638-3cf42e17-7b70-4a1a-b8b0-6a0d4bc12327.png)

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778924899618-534b0dfc-d558-4ac1-bb7a-4c311053f25e.png)

## 8.5 记忆容量管理
<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778925099323-02cf81f9-9152-47a8-952b-91fd7f44776c.png)

## 8.6 历史会话搜索
查看历史会话：`hermes sessions list`

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778922940242-c5d4c4e6-dbf3-48c2-af23-d024ce462044.png)

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778925216893-2d506404-d7e7-44f6-bb07-5e2196e98290.png)

## 8.7 自我介绍
文件大小有限制，满了之后会：手动判断合并/精简/删除

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778923929177-de34cede-a626-43d9-9c68-3fa094c72295.png)

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778924103191-7baaa6f9-1e3f-472a-a934-c4d7affc70a7.png)

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778925604169-82512e62-212c-495e-a9b0-4c20cbd2ae74.png)

## 8.8 记忆力测试
关闭后，重新启动，询问2天之前的会话内容，依然记得：

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1779118693697-39e5fb75-e6b2-45f5-a4e9-2549aa6a4fda.png)

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1779118773684-83bc2dbb-501d-4fb7-8404-843921d5e65e.png)

# 9 定时任务
## 9.1 工作原理
Cron 执行由网关守护进程处理。网关每 60 秒触发一次调度器，在独立的 Agent 会话中运行所有到期的任务。

## 9.2 CLI形式创建定时任务
/cron命令：

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778929985219-6be2e155-e09e-430d-9816-7ef22b094f77.png)

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778930475641-3ce8cf65-d6fc-4cc7-affe-2d40ee26fb36.png)

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778930429457-0c953963-2ef3-4ddd-81e9-190cef7fc8b6.png)

/cli命令：

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778930619556-8706c930-5f2c-4034-aa8e-24ff9e496025.png)

注意：定时任务可以使用skill技能

```powershell
/cron add 'every lh' '看一次天预报' --skill xian-weather
```

## 9.3 通过飞书/微信设置定时任务
<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778930020500-d8fa9a82-28ae-4167-b743-00dc93004d08.png)

# 10 web dashboard
<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778931078299-fbc9cbe9-d203-4766-a32b-c34180f84a9f.png)

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778931674835-1e4abb00-136d-43ec-904b-fc595714fcfc.png)

启动web界面：`hermes dashboard`

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778931536269-48cb00e2-fe94-4567-8bd7-72ea28e4ec8c.png)

访问：[http://127.0.0.1:9119/sessions](http://127.0.0.1:9119/sessions)

可以看到：已对接的平台，历史会话，skill技能，模型，定时任务

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778931516227-8b856ad1-c9aa-4205-90c3-930f300cae36.png)

# 11 最佳实践
## 11.1 安装和配置
支持macOS、Linux和 WSL2（Windows 用户需先安装 WSL2 并在其中运行）：

加-×参数可以看到每一步的执行过程，便于排查问题

```powershell
curl -fssL https://raw.githubusercontent.com/NousResearch/hermes-agent/main/scripts/install.sh I bash -x
```

## 11.2 配置防爬浏览器（Camofox)
（1）为什么需要：

普通的后端浏览器（如Chromiumheadless）访问大多数网站会立即被反爬机制拦截。Camofox提供了一个「像真人一样」的浏览器环境，使 Hermes 能够：

a. 自动读取网页文章

b. 文章自动填写表单

c. 操作需要登录的后台系统

d. 执行复杂的网页自动化任务

（2）配置步骤

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778932212612-6d3926e6-3c94-4c33-9e97-7e8d3cdf5687.png)

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778932578600-5f1d02da-6ab5-430f-a810-91f92d1a59d8.png)

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778932676153-c6f92070-4a9b-463b-b94c-2454db9f6958.png)

## 11.3 让hermes来总结并配置你的风格
<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778938521447-db1b9813-0e45-4ed9-844c-9875eb542608.png)

参考配置：

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778938673853-542f8876-f990-47fa-bca5-724a77439e22.png)

## 11.4 配置Auxiliary副驾模型路由
<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778938720906-45880bf3-c70d-448b-8e38-ee7b91e0c55b.png)

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778938817235-bc81dcb8-1ce5-4f85-9306-cbcc9e19d94e.png)

## 11.5 配置三层记忆系统
<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778938894773-00b087ee-07aa-4206-a8ca-7bcd1a7e3edb.png)

```yaml
memory:
  memory_enabled: true       # MEMORY.md－项目事实、踩坑记录
  user_profile_enabled: true # USER.md -用户画像与偏好
  memory_char_1imit: 4000    # 默认2200，重度使用建议调到4000
  user_char_1imit: 1375      # 用户画像字符上限
  nudge_interval: 5          # 每5轮提醒存记忆（默认10，调小更积
  flush_min_turns: 6         # 至少6 轮才触发退出时的记忆刷新
```

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778939088709-fa8af4e0-1434-415e-bd2d-1204efb3d699.png)

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778939127978-8020238a-9f51-426a-beee-94b406c4d4f6.png)

## 11.6 配置web search
<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778939178050-d76a72bf-be0b-4499-88fe-d41f20da98d9.png)

## 11.7 配置自动化审计（Hooks）
<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778939213058-2cacf00d-dd4e-4d7b-9925-905d7ab089b3.png)

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778939289962-611de7ae-342c-4903-a2c9-63a64d67fa2e.png)

## 11.8 配置Docker沙箱
<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778939443819-093e6127-5784-4d7e-bf26-0f0f0a3ed330.png)

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778939404398-97ba57db-341d-46e4-adf4-c03393c011b1.png)

## 11.9 使用多Agent
<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778939498472-4f971b71-3ead-4b14-9ed7-fd6f2bbf3c40.png)

## 11.10 建立备份系统
<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778939542650-cda0e66c-1786-4975-a7ba-87c064e48e4d.png)

```shell
#!/bin/bash
BACKUP_NAME="hermes_backup_$(date +%Y%m%d_%H%M%s)"
BACKUP_DIR="/tmp/$BACKUP_NAME"
DEST_DIR=~/hermes_backups

mkdir -p $BACKUP_DIR/hermes $DEST_DIR

echo"正在备份核心配置..."
cp ~/.hermes/config.yaml $BACKUP_DIR/hermes/
cp ~/.Hermes/.enV $BACKUP_DIR/hermes/
cp ~/.hermes/MEMORY.md $BACKUP_DIR/hermes/ 2>/dev/nul1

echo "正在备份数据库与会话..."
cp ~/.hermes/state.db $BACKUP_DIR/hermes/
cp -r ~/.hermes/sessions $BACKUP_DIR/hermes/ 2>/dev/nul1

echo "正在备份扩展与技能..."
cp -r ~/.hermes/plugins $BACKUP_DIR/hermes/ 2>/dev/nul1
cp -r ~/.hermes/ski11s $BACKUP_DIR/hermes/ 2>/dev/nul1
cp -r ~/.hermes/audit_logs $BACKUP_DIR/hermes/ 2>/dev/nul1

echo "正在备份所有 Profile..."
cp -r ~/.hermes/profiles $BACKUP_DIR/hermes/ 2>/dev/nul1
I
echo"压缩中..."
tar -czf $DEST_DIR/$BACKUP_NAME.tar.gz -C /tmp $BACKUP_NAME
rm -rf $BACKUP_DIR

echo "✅️备份完成：$DEST_DIR/$BACKUP_NAME.tar.gz"
echo "大小: $(du -h $DEST_DIR/$BACKUP_NAME.tar.gz | cut -f1)"
```

## 11.11 安装与沉淀技能（Skills）
<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1778939932574-53ee6102-bb44-43cc-9840-47907972883a.png)

## 11.12 安装hermes agent web ui
hermes agent官方并未提供web界面，我们可以借助社区的第三方项目实现：

**方式1：**nesquena的hermes-webui

```shell
git clone https://github.com/nesquena/hermes-webui.git

cd hermes-webui

python3 bootstrap.py
```

`bootstrap.py` 会：

1. 自动检测你已有的 Hermes Agent
2. 安装 WebUI 依赖
3. 启动 Web 服务器，默认端口**8787**
4. 自动打开浏览器进入引导页

装好后浏览器访问 `http://localhost:8787` 就能用了

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1779021265624-138b3ee1-ed6b-4488-aeeb-311b13defd46.png)

**方式2：**EKKOLearnAI/hermes-web-ui

`http://localhost:8648` — 令牌：`81ebeb27a1a7409d5dc258a4ee55f9eaac05cca65327757bd4e73434da2d6d31`

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1779119666871-ab1cd1ab-54ba-4ec2-bd74-0cd5ce1cf36e.png)

## 11.13 创建skill并验证
<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/12372452/1779120150366-d6d969ff-2eb5-4640-89ab-5d8d6d9a6b2a.png)

