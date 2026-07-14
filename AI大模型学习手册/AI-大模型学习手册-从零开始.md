# 🤖 AI/大模型应用开发学习手册 —— 从零开始

> **面向读者**：有 Java / 前端编程基础，想学习大模型应用开发的小白  
> **学习目标**：能独立搭建 AI 聊天应用、知识库问答系统、Agent 智能体  
> **预计总时长**：约 40 小时（每周 5 小时，8 周完成）  
> **编写日期**：2025 年 7 月  
> **版本**：v1.1

---

## 目录

- [前言：这份手册怎么用](#前言这份手册怎么用)
- [第 0 章：概念扫盲 —— 大模型到底是什么](#第-0-章概念扫盲--大模型到底是什么)
- [第 1 章：环境准备 —— 动手前的准备工作](#第-1-章环境准备--动手前的准备工作)
- [第 2 章：第一个 AI 应用 —— 跑通你的第一个聊天机器人](#第-2-章第一个-ai-应用--跑通你的第一个聊天机器人)
- [第 3 章：Prompt 工程入门 —— 学会和 AI 好好说话](#第-3-章prompt-工程入门--学会和-ai-好好说话)
- [第 4 章：RAG 知识库问答 —— 让 AI 读懂你的文档](#第-4-章rag-知识库问答--让-ai-读懂你的文档)
- [第 5 章：Function Calling 与 Agent —— 让 AI 动手干活](#第-5-章function-calling-与-agent--让-ai-动手干活)
- [第 6 章：流式输出与生产化 —— 从 Demo 到上线](#第-6-章流式输出与生产化--从-demo-到上线)
- [第 7 章：GitHub 实战项目推荐 —— 向优秀开源项目学习](#第-7-章github-实战项目推荐--向优秀开源项目学习)
- [附录 A：推荐资源清单](#附录-a推荐资源清单)
- [附录 B：常见问题 FAQ](#附录-b常见问题-faq)
- [附录 C：Java AI 工具栈速查](#附录-cjava-ai-工具栈速查)
- [附录 D：术语表](#附录-d术语表)

---

## 前言：这份手册怎么用

### 适合谁？

- ✅ 你会 Java 或前端（至少一种），能独立写 CRUD
- ✅ 你对 AI / ChatGPT / 大模型感兴趣，但不知道从哪里开始
- ✅ 你想做 AI 应用开发，而不是研究算法
- ❌ 你完全不会编程 → 建议先学一门语言再回来看

### 怎么读？

| 你的情况 | 建议阅读方式 |
|----------|------------|
| 完全小白，连 ChatGPT 都没用过 | 从第 0 章开始，逐章阅读，每章动手练习 |
| 用过 ChatGPT，了解基本概念 | 快速扫一遍第 0 章，从第 1 章开始 |
| 已经调用过 API | 跳到第 4 章（RAG）和第 5 章（Agent） |

### 学习路径速览

```
第 0 章（2h）     概念扫盲：LLM、Token、Prompt 是什么
    ↓
第 1 章（1h）     环境准备：注册账号、拿 API Key
    ↓
第 2 章（4h）     第一个应用：Java + 前端聊天机器人
    ↓
第 3 章（3h）     Prompt 工程：学会写好提示词
    ↓
第 4 章（8h）     RAG 知识库：让 AI 读懂你的文档 ⭐ 重点
    ↓
第 5 章（8h）     Agent：让 AI 调用工具、执行任务 ⭐ 重点
    ↓
第 6 章（6h）     生产化：流式输出、缓存、限流、部署
```

### 学习原则

1. **先跑通，再理解** —— 代码跑起来比看懂所有概念更重要
2. **每章必动手** —— 读完不练 = 没读
3. **遇到报错是好事** —— 每个报错都是一次学习机会
4. **不要跳章** —— 每章依赖前一章的知识

---

## 第 0 章：概念扫盲 —— 大模型到底是什么

> ⏱ 预计时间：2 小时 | 🎯 目标：理解核心概念，能跟人聊 AI 不露怯

### 0.1 AI → 机器学习 → 深度学习 → 大模型

这四个词的关系就像 **俄罗斯套娃**，一层套一层：

```
人工智能 (AI)
  └── 机器学习 (Machine Learning)
        └── 深度学习 (Deep Learning)
              └── 大语言模型 (LLM / 大模型)
```

| 概念 | 一句话解释 | 类比 |
|------|-----------|------|
| **人工智能 (AI)** | 让机器表现出智能 | 造一个会思考的机器人 |
| **机器学习 (ML)** | 让机器从数据中学习规律，而不是人工写规则 | 教小孩认猫：给他看 1000 张猫的照片，而不是一条条描述 |
| **深度学习 (DL)** | 用多层神经网络学习，是机器学习的一种方法 | 小孩的大脑有很多层神经元来处理信息 |
| **大语言模型 (LLM)** | 用海量文本训练的超大深度学习模型，能理解和生成文字 | 一个读过整个图书馆所有书的人 |

> 🔑 **关键认知**：你不需要懂机器学习或深度学习就能做大模型应用开发！就像你不需要懂发动机原理就能开车一样。

---

### 0.2 核心概念速通

#### LLM（Large Language Model，大语言模型）

一个超大型的"文字预测器"——你给它一段文字（Prompt），它预测下一段最合适的文字。

```
你输入：  "今天天气真"
LLM 输出："好，适合出去走走。"
```

它之所以"聪明"，是因为训练时读了互联网上几乎所有的公开文本，学会了人类的语言模式、知识、推理方式。

**主流大模型一览（2025 年 7 月）**：

| 模型 | 开发者 | 特点 | 适合场景 |
|------|--------|------|----------|
| **DeepSeek-V3** | 深度求索 | 性价比极高，中文最强，API 兼容 OpenAI | 首选推荐，日常开发 |
| **GPT-4o** | OpenAI | 综合能力最强，多模态 | 复杂推理、图片理解 |
| **Claude 3.5 Sonnet** | Anthropic | 代码能力强，长文本 | 编程辅助、长文档 |
| **Qwen 2.5** | 阿里 | 开源，中文好 | 私有化部署 |
| **Gemini 2.0** | Google | 多模态，免费额度大方 | 图片/视频理解 |

---

#### Token（令牌）

大模型不直接处理"字"，而是把文本切成一个个小块，每个小块叫一个 Token。

```
中文："我是一个程序员"
      → ["我", "是", "一个", "程序员"]  ← 约 4 个 Token

英文："I am a programmer"
      → ["I", " am", " a", " programmer"]  ← 4 个 Token
```

**经验法则**：
- 中文：1 个字 ≈ 1-2 个 Token
- 英文：1 个单词 ≈ 1-2 个 Token
- 1000 个 Token ≈ 750 个英文单词 ≈ 1500 个中文字

> 💰 Token 是计费单位——你花的每一分钱，都是按 Token 算的。

---

#### Prompt（提示词）

你发给大模型的**输入文本**。Prompt 写得好不好，直接决定输出质量。

```
❌ 差的 Prompt："帮我写个代码"
✅ 好的 Prompt："你是一个 Java 后端专家。请帮我写一个 Spring Boot 的
   RESTful 接口，功能是接收用户名和密码，验证后返回 JWT Token。要求：
   1. 使用 Spring Security
   2. Token 有效期 2 小时
   3. 加上完整的异常处理"
```

---

#### Context Window（上下文窗口）

大模型一次能"记住"的最大文本量。超过这个长度的内容会被遗忘。

| 模型 | 上下文窗口 | 相当于 |
|------|-----------|--------|
| DeepSeek-V3 | 128K Token | 约一部《三体》 |
| GPT-4o | 128K Token | 约一部《三体》 |
| Claude 3.5 | 200K Token | 约两部《三体》 |

> ⚠️ 上下文不是越大越好——内容越多，模型越容易"分心"，且费用越高。

---

#### Temperature（温度）

控制输出的**随机性**，范围 0 ~ 2：

| Temperature | 效果 | 适合场景 |
|-------------|------|----------|
| 0 ~ 0.3 | 确定性强，每次回答基本一致 | 代码生成、数学计算、事实问答 |
| 0.5 ~ 0.7 | 平衡创造性和准确性 | 日常对话、翻译 |
| 0.8 ~ 1.2 | 创造性高，每次回答可能不同 | 创意写作、头脑风暴 |

---

#### Embedding（嵌入向量）

把一段文字变成一串数字（向量），用于计算两段文字的"相似度"。

```
"猫" → [0.12, -0.34, 0.56, ..., 0.78]  ← 一个 1536 维的向量
"猫咪" → [0.11, -0.33, 0.57, ..., 0.77] ← 和"猫"的向量非常接近！
"汽车" → [0.89, 0.42, -0.12, ..., -0.55] ← 和"猫"的向量差很多
```

这是 RAG（知识库问答）的基石——用向量相似度来"搜索"最相关的文档片段。

---

#### RAG（Retrieval-Augmented Generation，检索增强生成）

让大模型在回答问题之前，**先查资料**，再基于资料回答。

```
传统方式：用户提问 → 大模型凭记忆回答（可能胡说八道）
RAG 方式：用户提问 → 搜索知识库 → 把相关文档 + 问题一起给大模型 → 大模型基于文档回答
```

这是目前最主流的 AI 应用模式，第 4 章会详细讲解。

---

#### Function Calling（函数调用）

让大模型**不是输出文字，而是输出"我想调用哪个函数"**。

```
用户："今天北京天气怎么样？"

大模型不是直接回答（它不知道实时天气），而是输出：
{
  "function": "get_weather",
  "parameters": { "city": "北京" }
}

→ 你的程序调用天气 API → 把结果返回给大模型 → 大模型整理成自然语言回复
```

这是 Agent 的基础，第 5 章会详细讲解。

---

### 0.3 自测题

做完这 5 道题，确认你理解了核心概念：

1. Token 是什么？1000 个 Token 大约等于多少中文字？
2. Temperature 设为 0.1 和 1.0 有什么区别？各适合什么场景？
3. Embedding 是干什么用的？
4. RAG 的全称是什么？解决了什么问题？
5. Function Calling 和普通对话有什么区别？

> 答案见附录 B 末尾。

---

## 第 1 章：环境准备 —— 动手前的准备工作

> ⏱ 预计时间：1 小时 | 🎯 目标：拿到 API Key，准备好开发工具

### 1.1 注册 DeepSeek 并获取 API Key

DeepSeek 是目前性价比最高的选择，中文能力强，API 完全兼容 OpenAI 格式。

**步骤**：

1. 打开 [DeepSeek 开放平台](https://platform.deepseek.com/)
2. 点击右上角「注册」，用手机号或邮箱注册
3. 注册后进入「API Keys」页面
4. 点击「创建 API Key」，命名为 `learning`
5. **立即复制保存**！Key 只显示一次，丢了只能重新生成

> 💰 DeepSeek 价格极低：输入 1 元/百万 Token，输出 2 元/百万 Token。充值 10 块钱够你学完整本手册。

**备用方案**：如果你有 OpenAI 账号，也可以用 GPT-4o-mini（更便宜）。操作类似，去 [OpenAI Platform](https://platform.openai.com/) 拿 Key。

---

### 1.2 开发工具准备

**后端（Java）**：

| 工具 | 说明 | 安装方式 |
|------|------|----------|
| JDK 17+ | Java 开发环境 | `brew install openjdk@17` (Mac) 或官网下载 |
| IntelliJ IDEA | IDE（社区版免费） | [官网下载](https://www.jetbrains.com/idea/download/) |
| Maven/Gradle | 依赖管理 | IDEA 自带 |
| Postman 或 Apifox | API 调试工具 | [官网下载](https://www.postman.com/) |

**前端（可选）**：

| 工具 | 说明 |
|------|------|
| VS Code | 前端编辑器 |
| Node.js 18+ | 前端运行环境 |

**验证安装**：

```bash
java --version    # 应该显示 17 或以上
node --version    # 如果做前端的话
```

---

### 1.3 测试 API Key 是否能用

用 curl 快速测试（把 `your-api-key` 替换成你的真实 Key）：

```bash
curl https://api.deepseek.com/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer your-api-key" \
  -d '{
    "model": "deepseek-chat",
    "messages": [
      {"role": "user", "content": "你好，请用一句话介绍你自己"}
    ]
  }'
```

如果返回类似这样的内容，说明成功了：

```json
{
  "choices": [
    {
      "message": {
        "content": "你好！我是 DeepSeek，一个由深度求索公司创造的 AI 助手。"
      }
    }
  ]
}
```

> 🎉 恭喜！你已经完成了一次 API 调用！

---

### 1.4 安全提醒 ⚠️

**API Key 是密码，不是配置！**

```
❌ 不要做的：
- 把 Key 写在代码里提交到 Git
- 把 Key 发到群里或截图分享
- 把 Key 写在前端代码里

✅ 应该做的：
- Key 放在环境变量中
- Key 放在 application.yml 中，且该文件加入 .gitignore
- 使用 Spring Boot 的 @Value 或配置中心管理
```

---

## 第 2 章：第一个 AI 应用 —— 跑通你的第一个聊天机器人

> ⏱ 预计时间：4 小时 | 🎯 目标：用 Java 搭建一个能对话的 AI 聊天后端 + 简单前端页面

### 2.1 项目概览

我们要做的东西：

```
浏览器 ←→ 前端页面（聊天 UI）←→ Java 后端（Spring Boot）←→ DeepSeek API
```

用户在前端输入消息 → 后端转发给 DeepSeek → DeepSeek 回复 → 后端返回给前端显示。

---

### 2.2 创建 Spring Boot 项目

**方式一：Spring Initializr（推荐）**

1. 打开 [start.spring.io](https://start.spring.io/)
2. 配置：
   - Project: Maven
   - Language: Java
   - Spring Boot: 3.x 最新版
   - Group: `com.example`
   - Artifact: `ai-chat`
   - Dependencies: **Spring Web**, **Lombok**
3. 点击 Generate，下载后解压，用 IDEA 打开

**方式二：IDEA 直接创建**

File → New → Project → Spring Initializr → 同上配置

---

### 2.3 编写后端代码

项目结构：

```
src/main/java/com/example/aichat/
├── AiChatApplication.java        ← 启动类
├── config/
│   └── RestTemplateConfig.java   ← HTTP 客户端配置
├── controller/
│   └── ChatController.java       ← 聊天接口
├── dto/
│   ├── ChatRequest.java          ← 请求体
│   └── ChatResponse.java         ← 响应体
└── service/
    └── ChatService.java          ← 调用 DeepSeek API 的逻辑
```

#### 2.3.1 配置 application.yml

```yaml
# src/main/resources/application.yml
server:
  port: 8080

deepseek:
  api-key: ${DEEPSEEK_API_KEY}   # 从环境变量读取
  api-url: https://api.deepseek.com/v1/chat/completions
  model: deepseek-chat
```

设置环境变量（Mac / Linux）：

```bash
export DEEPSEEK_API_KEY="你的真实Key"
```

Windows：

```cmd
set DEEPSEEK_API_KEY=你的真实Key
```

#### 2.3.2 ChatRequest.java —— 前端发给后端的请求

```java
package com.example.aichat.dto;

import lombok.Data;

@Data
public class ChatRequest {
    private String message;  // 用户输入的消息
}
```

#### 2.3.3 ChatResponse.java —— 后端返回给前端的响应

```java
package com.example.aichat.dto;

import lombok.Data;

@Data
public class ChatResponse {
    private String reply;  // AI 的回复
    private int tokensUsed; // 消耗的 Token 数（可选）
}
```

#### 2.3.4 RestTemplateConfig.java —— HTTP 客户端

```java
package com.example.aichat.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.client.RestTemplate;

@Configuration
public class RestTemplateConfig {

    @Bean
    public RestTemplate restTemplate() {
        return new RestTemplate();
    }
}
```

#### 2.3.5 ChatService.java —— 核心逻辑

```java
package com.example.aichat.service;

import com.example.aichat.dto.ChatRequest;
import com.example.aichat.dto.ChatResponse;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.http.*;
import org.springframework.stereotype.Service;
import org.springframework.web.client.RestTemplate;

import java.util.*;

@Service
public class ChatService {

    @Value("${deepseek.api-key}")
    private String apiKey;

    @Value("${deepseek.api-url}")
    private String apiUrl;

    @Value("${deepseek.model}")
    private String model;

    private final RestTemplate restTemplate;

    public ChatService(RestTemplate restTemplate) {
        this.restTemplate = restTemplate;
    }

    public ChatResponse chat(ChatRequest request) {
        // 1. 构建请求头
        HttpHeaders headers = new HttpHeaders();
        headers.setContentType(MediaType.APPLICATION_JSON);
        headers.set("Authorization", "Bearer " + apiKey);

        // 2. 构建请求体（OpenAI 格式，DeepSeek 兼容）
        Map<String, Object> body = new HashMap<>();
        body.put("model", model);
        body.put("temperature", 0.7);  // 适中创造性

        List<Map<String, String>> messages = new ArrayList<>();

        // 系统提示词：设定 AI 的角色
        Map<String, String> systemMsg = new HashMap<>();
        systemMsg.put("role", "system");
        systemMsg.put("content", "你是一个友好的编程助手，回答简洁、准确。");
        messages.add(systemMsg);

        // 用户消息
        Map<String, String> userMsg = new HashMap<>();
        userMsg.put("role", "user");
        userMsg.put("content", request.getMessage());
        messages.add(userMsg);

        body.put("messages", messages);

        // 3. 发送请求
        HttpEntity<Map<String, Object>> entity = new HttpEntity<>(body, headers);
        ResponseEntity<Map> response = restTemplate.postForEntity(apiUrl, entity, Map.class);

        // 4. 解析响应
        Map<String, Object> responseBody = response.getBody();
        List<Map<String, Object>> choices =
                (List<Map<String, Object>>) responseBody.get("choices");
        Map<String, Object> message = (Map<String, Object>) choices.get(0).get("message");
        String content = (String) message.get("content");

        // 5. 返回
        ChatResponse chatResponse = new ChatResponse();
        chatResponse.setReply(content);
        return chatResponse;
    }
}
```

#### 2.3.6 ChatController.java —— 对外接口

```java
package com.example.aichat.controller;

import com.example.aichat.dto.ChatRequest;
import com.example.aichat.dto.ChatResponse;
import com.example.aichat.service.ChatService;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/api")
@CrossOrigin(origins = "*")  // 允许前端跨域访问
public class ChatController {

    private final ChatService chatService;

    public ChatController(ChatService chatService) {
        this.chatService = chatService;
    }

    @PostMapping("/chat")
    public ChatResponse chat(@RequestBody ChatRequest request) {
        return chatService.chat(request);
    }
}
```

---

### 2.4 测试后端接口

启动项目后，用 curl 测试：

```bash
curl -X POST http://localhost:8080/api/chat \
  -H "Content-Type: application/json" \
  -d '{"message": "用 Java 写一个 Hello World"}'
```

预期返回：

```json
{
  "reply": "这是用 Java 写的 Hello World 程序：\n\n```java\npublic class HelloWorld {\n    public static void main(String[] args) {\n        System.out.println(\"Hello, World!\");\n    }\n}\n```\n\n运行方式：...",
  "tokensUsed": null
}
```

---

### 2.5 前端聊天页面（选做）

如果你也想搭个前端，创建一个简单的 HTML 页面：

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AI 聊天助手</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
            background: #f5f5f5;
            display: flex; justify-content: center; align-items: center;
            height: 100vh;
        }
        .chat-container {
            width: 600px; max-width: 100%; height: 80vh;
            background: white; border-radius: 12px; box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            display: flex; flex-direction: column; overflow: hidden;
        }
        .chat-header {
            padding: 16px 20px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white; font-size: 18px; font-weight: 600;
        }
        .chat-messages {
            flex: 1; overflow-y: auto; padding: 20px;
            display: flex; flex-direction: column; gap: 12px;
        }
        .message {
            max-width: 80%; padding: 10px 14px;
            border-radius: 12px; line-height: 1.6;
            white-space: pre-wrap; word-break: break-word;
        }
        .message.user {
            align-self: flex-end;
            background: #667eea; color: white;
        }
        .message.assistant {
            align-self: flex-start;
            background: #f0f0f0; color: #333;
        }
        .chat-input {
            display: flex; padding: 12px; border-top: 1px solid #eee; gap: 8px;
        }
        .chat-input input {
            flex: 1; padding: 10px 16px;
            border: 1px solid #ddd; border-radius: 24px;
            font-size: 14px; outline: none;
        }
        .chat-input input:focus { border-color: #667eea; }
        .chat-input button {
            padding: 10px 20px; background: #667eea; color: white;
            border: none; border-radius: 24px; cursor: pointer; font-size: 14px;
        }
        .chat-input button:hover { background: #5a6fd6; }
        .chat-input button:disabled { background: #ccc; cursor: not-allowed; }
    </style>
</head>
<body>
    <div class="chat-container">
        <div class="chat-header">🤖 AI 聊天助手</div>
        <div class="chat-messages" id="messages"></div>
        <div class="chat-input">
            <input type="text" id="userInput"
                   placeholder="输入消息，按回车发送..."
                   onkeydown="if(event.key==='Enter') sendMessage()">
            <button onclick="sendMessage()">发送</button>
        </div>
    </div>

    <script>
        const API_URL = 'http://localhost:8080/api/chat';

        function addMessage(content, role) {
            const messagesDiv = document.getElementById('messages');
            const msgDiv = document.createElement('div');
            msgDiv.className = 'message ' + role;
            msgDiv.textContent = content;
            messagesDiv.appendChild(msgDiv);
            messagesDiv.scrollTop = messagesDiv.scrollHeight;
        }

        async function sendMessage() {
            const input = document.getElementById('userInput');
            const message = input.value.trim();
            if (!message) return;

            // 显示用户消息
            addMessage(message, 'user');
            input.value = '';
            document.querySelector('button').disabled = true;

            try {
                const response = await fetch(API_URL, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({ message: message })
                });
                const data = await response.json();
                addMessage(data.reply, 'assistant');
            } catch (error) {
                addMessage('出错了：' + error.message, 'assistant');
            } finally {
                document.querySelector('button').disabled = false;
            }
        }
    </script>
</body>
</html>
```

直接用浏览器打开这个 HTML 文件就能用。

---

### 2.6 你完成了什么？

✅ 一个可以对话的 AI 聊天机器人  
✅ 理解了 API 调用的完整流程  
✅ 掌握了最基础的 Java + AI 集成方式

> 🎉 你已经从一个"AI 使用者"变成了"AI 应用开发者"！

---

## 第 3 章：Prompt 工程入门 —— 学会和 AI 好好说话

> ⏱ 预计时间：3 小时 | 🎯 目标：写出高质量的 Prompt，让 AI 输出更精准

### 3.1 什么是 Prompt 工程

Prompt 工程 = **设计和优化给 AI 的输入**，让输出符合预期。

它不是"玄学"，而是一套有章可循的技巧。

---

### 3.2 Prompt 的四大要素

一个好的 Prompt 通常包含：

| 要素 | 说明 | 示例 |
|------|------|------|
| **角色 (Role)** | 设定 AI 的身份 | "你是一个资深的 Java 后端架构师" |
| **任务 (Task)** | 明确要做什么 | "请审查以下代码的安全漏洞" |
| **格式 (Format)** | 输出格式要求 | "用表格列出问题、严重程度和修复建议" |
| **约束 (Constraint)** | 限制条件 | "不要修改业务逻辑，只指出安全问题" |

**完整示例**：

```
【角色】你是一个资深 Java 后端架构师，擅长代码安全审查。

【任务】审查以下代码，找出所有安全漏洞。

【格式要求】用 Markdown 表格输出，包含三列：
- 问题描述
- 严重程度（高/中/低）
- 修复建议

【约束】
- 只关注安全问题，不评价代码风格
- 如果没发现问题，回复"未发现安全漏洞"

【代码】
[粘贴你的代码]
```

---

### 3.3 三大核心技巧

#### 技巧一：Few-Shot（少样本提示）

给 AI 看几个示例，让它照猫画虎。

```
请将以下用户反馈分类为「Bug」「需求」「咨询」。

示例：
"登录页面打不开了" → Bug
"能不能加个导出Excel的功能" → 需求
"这个功能怎么用" → 咨询

现在请分类："上传文件总是超时"
```

#### 技巧二：Chain of Thought（思维链，CoT）

让 AI "一步步想"，而不是直接给答案。

```
❌ 直接问：
"鸡兔同笼，35个头，94只脚，问鸡和兔各几只？"

✅ 加一句：
"鸡兔同笼，35个头，94只脚，问鸡和兔各几只？
请一步一步推理，先设未知数，再列方程，最后求解。"
```

#### 技巧三：结构化输出

要求 AI 输出 JSON、XML 等结构化格式，方便程序解析。

```
请分析以下用户评论的情感，以 JSON 格式输出。

格式：{"sentiment": "正面/负面/中性", "score": 0-1, "keywords": ["关键词1", "关键词2"]}

评论："这个产品非常好用，但是价格有点贵"
```

---

### 3.4 实战练习

修改你第 2 章的 ChatService，加入系统提示词：

```java
// ChatService.java 中的 system 消息
Map<String, String> systemMsg = new HashMap<>();
systemMsg.put("role", "system");
systemMsg.put("content",
    "你是一个专业的编程助手。回答问题时请遵循以下规则：\n" +
    "1. 先给出简洁的答案\n" +
    "2. 再提供代码示例（如果有）\n" +
    "3. 最后给出注意事项\n" +
    "4. 如果问题不明确，先确认需求再回答"
);
```

然后分别测试这些 Prompt，感受差异：

| 测试 | Prompt | 观察点 |
|------|--------|--------|
| 1 | "写个排序" | 太模糊，AI 会猜 |
| 2 | "用 Java 写一个冒泡排序，对 int[] 排序" | 明确语言、算法、类型 |
| 3 | 第 2 个 + "要求：有注释，时间 O(n²)，返回排序后的数组" | 更精确的约束 |

---

### 3.5 Prompt 模板管理

当 Prompt 变多时，不要硬编码在代码里。推荐做法：

```java
// 使用 Spring 的 @ConfigurationProperties 管理 Prompt 模板
@ConfigurationProperties(prefix = "prompt")
@Component
@Data
public class PromptConfig {
    private String codeReview;
    private String translate;
    private String summarize;
}
```

```yaml
# application.yml
prompt:
  code-review: |
    你是一个资深 Java 后端架构师。请审查以下代码：
    {code}
    输出格式：JSON，包含 issues 数组。
  translate: |
    请将以下内容翻译成{target_lang}，保持原意和专业术语：
    {text}
  summarize: |
    请用 3 句话总结以下内容，每句话不超过 30 字：
    {content}
```

> 💡 第 4 章做 RAG 时，Prompt 模板管理会更加重要。

---

## 第 4 章：RAG 知识库问答 —— 让 AI 读懂你的文档

> ⏱ 预计时间：8 小时 | 🎯 目标：搭建一个能基于文档回答问题的知识库系统  
> ⚠️ 这是本手册最重要的章节，请认真完成

### 4.1 RAG 是什么，为什么需要它？

**问题**：大模型的知识截止于训练日期，它不知道你公司内部的文档、最新的信息。

**RAG 的解决思路**：

```
1. 提前把文档切成小块 → 用 Embedding 转成向量 → 存入向量数据库
2. 用户提问 → 把问题也转成向量 → 在向量数据库中搜索最相关文档块
3. 把搜索到的文档块 + 用户问题一起发给大模型 → 大模型基于文档回答
```

```
                    ┌─────────────┐
                    │  用户提问    │
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │ Embedding   │
                    │ 转成向量     │
                    └──────┬──────┘
                           │
              ┌────────────▼────────────┐
              │   向量数据库（Milvus等）  │
              │   搜索最相似的文档片段    │
              └────────────┬────────────┘
                           │
                    ┌──────▼──────┐
                    │ 用户问题 +   │
                    │ 相关文档片段  │
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │   大模型      │
                    │   生成回答    │
                    └──────────────┘
```

---

### 4.2 RAG 的技术栈选择

| 组件 | 推荐方案 | 备选方案 |
|------|---------|----------|
| 大模型 | DeepSeek-V3 | GPT-4o-mini |
| Embedding 模型 | text-embedding-3-small (OpenAI) 或 bge-large-zh (开源) | DeepSeek Embedding |
| 向量数据库 | **Chroma**（轻量，适合学习） | Milvus / pgvector / Qdrant |
| 文档解析 | Apache PDFBox + Apache POI | LangChain4j 内置 |

> 为什么先选 Chroma？它是 Python 生态中最简单的向量数据库，几行代码就能跑。等你理解了原理，再换 Milvus 做生产部署。

---

### 4.3 搭建 RAG 系统

由于 Java 生态的 RAG 工具链不如 Python 成熟，这里提供两种方案：

**方案 A（推荐学习用）**：Python + Chroma 快速原型 → 理解原理后迁移到 Java  
**方案 B（生产用）**：Java + LangChain4j + Milvus/pgvector

本手册以方案 A 为主（快速理解原理），再介绍方案 B 的 Java 实现。

---

#### 4.3.1 方案 A：Python 快速原型（2 小时）

**安装依赖**：

```bash
pip install chromadb openai python-dotenv pypdf2 langchain-text-splitters
```

**完整 RAG 脚本**：

```python
# rag_demo.py —— 一个最简 RAG 系统
import os
from openai import OpenAI
import chromadb
from chromadb.utils import embedding_functions

# ===== 1. 初始化 =====
client = OpenAI(
    api_key=os.getenv("DEEPSEEK_API_KEY"),  # 也可以用 DeepSeek
    base_url="https://api.deepseek.com/v1"
)

# Chroma 向量数据库（数据存在本地）
chroma_client = chromadb.PersistentClient(path="./chroma_db")

# Embedding 函数（用 OpenAI 的）
embedding_fn = embedding_functions.OpenAIEmbeddingFunction(
    api_key=os.getenv("OPENAI_API_KEY"),
    model_name="text-embedding-3-small"
)

# 创建或获取集合
collection = chroma_client.get_or_create_collection(
    name="my_knowledge_base",
    embedding_function=embedding_fn
)

# ===== 2. 导入文档 =====
def load_documents(folder_path):
    """读取文件夹中的所有 txt 文件，切成小块存入向量数据库"""
    from langchain_text_splitters import RecursiveCharacterTextSplitter

    splitter = RecursiveCharacterTextSplitter(
        chunk_size=500,      # 每块 500 字
        chunk_overlap=50,    # 块之间重叠 50 字（防止切断上下文）
        separators=["\n\n", "\n", "。", "！", "？", "，", " ", ""]
    )

    for filename in os.listdir(folder_path):
        if filename.endswith(".txt"):
            with open(os.path.join(folder_path, filename), "r", encoding="utf-8") as f:
                content = f.read()
                chunks = splitter.split_text(content)

                # 存入 Chroma
                collection.add(
                    documents=chunks,
                    ids=[f"{filename}_{i}" for i in range(len(chunks))],
                    metadatas=[{"source": filename} for _ in chunks]
                )
                print(f"✅ {filename}: {len(chunks)} 个文本块")

# ===== 3. 检索 =====
def search(query, top_k=3):
    """搜索最相关的文档块"""
    results = collection.query(
        query_texts=[query],
        n_results=top_k
    )
    return results["documents"][0]  # 返回最相关的 top_k 个文本块

# ===== 4. 生成回答 =====
def ask(query):
    """基于检索到的文档回答问题"""
    # 先搜索
    relevant_docs = search(query)
    context = "\n\n---\n\n".join(relevant_docs)

    # 构建 Prompt
    prompt = f"""你是一个知识库助手。请基于以下文档内容回答问题。

【规则】
- 如果文档中有答案，请引用文档内容
- 如果文档中没有答案，请回答"根据现有资料，我无法回答这个问题"
- 回答要简洁，不超过 200 字

【文档内容】
{context}

【用户问题】
{query}

【回答】"""

    # 调用大模型
    response = client.chat.completions.create(
        model="deepseek-chat",
        messages=[{"role": "user", "content": prompt}],
        temperature=0.3  # 低温度，减少幻觉
    )

    return response.choices[0].message.content

# ===== 5. 使用 =====
if __name__ == "__main__":
    # 第一步：导入文档（只做一次）
    load_documents("./my_documents")

    # 第二步：提问
    while True:
        q = input("\n🔍 请输入问题（输入 q 退出）：")
        if q == "q":
            break
        answer = ask(q)
        print(f"\n🤖 {answer}")
```

**使用方式**：

```bash
# 1. 创建文档目录，放几个 txt 文件
mkdir my_documents
echo "公司成立于2020年，主要产品是智能客服系统..." > my_documents/公司介绍.txt
echo "Java 后端使用 Spring Boot 3.x，数据库用 PostgreSQL..." > my_documents/技术栈.txt

# 2. 运行
python rag_demo.py

# 3. 提问
🔍 请输入问题：公司是什么时候成立的？
🤖 根据文档，公司成立于2020年。
```

---

#### 4.3.2 方案 B：Java + LangChain4j（4 小时）

LangChain4j 是 Java 版的 LangChain，专门为 Java 生态设计。

**Maven 依赖**：

```xml
<dependency>
    <groupId>dev.langchain4j</groupId>
    <artifactId>langchain4j-open-ai</artifactId>
    <version>0.36.2</version>
</dependency>
<dependency>
    <groupId>dev.langchain4j</groupId>
    <artifactId>langchain4j-pgvector</artifactId>
    <version>0.36.2</version>
</dependency>
<dependency>
    <groupId>dev.langchain4j</groupId>
    <artifactId>langchain4j-document-parser-apache-pdfbox</artifactId>
    <version>0.36.2</version>
</dependency>
```

**核心代码**：

```java
// RagService.java —— Java 版 RAG 服务
package com.example.rag.service;

import dev.langchain4j.data.document.Document;
import dev.langchain4j.data.document.DocumentParser;
import dev.langchain4j.data.document.DocumentSplitter;
import dev.langchain4j.data.document.parser.apache.pdfbox.ApachePdfBoxDocumentParser;
import dev.langchain4j.data.document.splitter.DocumentSplitters;
import dev.langchain4j.data.embedding.Embedding;
import dev.langchain4j.data.segment.TextSegment;
import dev.langchain4j.model.embedding.EmbeddingModel;
import dev.langchain4j.model.openai.OpenAiChatModel;
import dev.langchain4j.model.openai.OpenAiEmbeddingModel;
import dev.langchain4j.store.embedding.EmbeddingStore;
import dev.langchain4j.store.embedding.pgvector.PgVectorEmbeddingStore;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Service;

import java.io.InputStream;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.List;

@Service
public class RagService {

    private final OpenAiChatModel chatModel;
    private final EmbeddingModel embeddingModel;
    private final EmbeddingStore<TextSegment> embeddingStore;

    public RagService(
            @Value("${deepseek.api-key}") String apiKey,
            EmbeddingStore<TextSegment> embeddingStore) {

        // 用 DeepSeek（兼容 OpenAI 格式）
        this.chatModel = OpenAiChatModel.builder()
                .apiKey(apiKey)
                .baseUrl("https://api.deepseek.com/v1")
                .modelName("deepseek-chat")
                .temperature(0.3)
                .build();

        // Embedding 模型（用 OpenAI，因为 DeepSeek 的 Embedding 需要单独开通）
        this.embeddingModel = OpenAiEmbeddingModel.builder()
                .apiKey(System.getenv("OPENAI_API_KEY"))
                .modelName("text-embedding-3-small")
                .build();

        this.embeddingStore = embeddingStore;
    }

    // 导入 PDF 文档
    public void importPdf(Path pdfPath) throws Exception {
        DocumentParser parser = new ApachePdfBoxDocumentParser();
        try (InputStream is = Files.newInputStream(pdfPath)) {
            Document doc = parser.parse(is);

            // 切成小块
            DocumentSplitter splitter = DocumentSplitters.recursive(500, 50);
            List<TextSegment> segments = splitter.split(doc);

            // 向量化并存储
            for (TextSegment segment : segments) {
                Embedding embedding = embeddingModel.embed(segment).content();
                embeddingStore.add(embedding, segment);
            }
        }
    }

    // 基于文档问答
    public String ask(String question) {
        // 1. 检索相关文档
        Embedding questionEmbedding = embeddingModel.embed(question).content();
        List<TextSegment> relevant = embeddingStore
                .findRelevant(questionEmbedding, 3); // 取最相关的 3 块

        // 2. 拼成上下文
        StringBuilder context = new StringBuilder();
        for (TextSegment seg : relevant) {
            context.append(seg.text()).append("\n\n---\n\n");
        }

        // 3. 构建 Prompt 并调用
        String prompt = String.format("""
            基于以下文档内容回答问题。如果文档中没有答案，请如实说明。

            文档内容：
            %s

            问题：%s
            """, context.toString(), question);

        return chatModel.generate(prompt);
    }
}
```

**PgVector 配置**：

```java
@Configuration
public class VectorStoreConfig {

    @Bean
    public EmbeddingStore<TextSegment> embeddingStore() {
        return PgVectorEmbeddingStore.builder()
                .host("localhost")
                .port(5432)
                .database("rag_db")
                .user("postgres")
                .password("password")
                .table("embeddings")
                .dimension(1536)  // text-embedding-3-small 是 1536 维
                .build();
    }
}
```

---

### 4.4 RAG 的核心参数调优

| 参数 | 推荐值 | 说明 |
|------|--------|------|
| chunk_size（分块大小） | 300-800 | 太小丢失上下文，太大检索不精准 |
| chunk_overlap（重叠大小） | 50-100 | 防止关键信息被切断在边界 |
| top_k（检索数量） | 3-5 | 太少信息不足，太多引入噪声 |
| 检索时的 Temperature | 0.1-0.3 | 低温度减少幻觉 |

---

### 4.5 常见问题

**Q: 为什么回答不准确？**

按以下顺序排查：
1. 文档切块是否合理？（调整 chunk_size）
2. Embedding 模型是否合适？（中文用 bge-large-zh 更好）
3. Prompt 是否清晰？（明确告诉它"基于文档回答，不知道就说不知道"）
4. top_k 是否合适？（试着调到 5）

**Q: 搜索结果不相关？**

可能原因：
- 文档和问题的表述差异太大 → 试试混合搜索（Hybrid Search）：向量搜索 + 关键词搜索
- Embedding 模型对特定领域不友好 → 试试微调 Embedding 模型

---

## 第 5 章：Function Calling 与 Agent —— 让 AI 动手干活

> ⏱ 预计时间：8 小时 | 🎯 目标：让 AI 不仅能聊天，还能调用函数、执行任务

### 5.1 什么是 Function Calling？

到目前为止，AI 只能"说话"。Function Calling 让它能"做事"——调用你定义的函数。

```
用户："今天北京天气怎么样？"

没有 Function Calling：
  AI："抱歉，我无法获取实时天气。" ❌

有 Function Calling：
  1. AI 输出：{ "function": "get_weather", "args": { "city": "北京" } }
  2. 你的程序调用天气 API，得到结果："北京今天晴天，25°C"
  3. 把结果发回给 AI
  4. AI 整理回复："北京今天天气晴朗，气温 25°C，适合出行！" ✅
```

---

### 5.2 Function Calling 实战（Java）

#### 5.2.1 定义函数

```java
// WeatherTool.java —— 天气查询工具
package com.example.agent.tool;

import com.fasterxml.jackson.annotation.JsonProperty;
import com.fasterxml.jackson.annotation.JsonPropertyDescription;
import org.springframework.stereotype.Component;
import org.springframework.web.client.RestTemplate;

@Component
public class WeatherTool {

    // 这个注解告诉 AI：这个函数是做什么的
    @JsonPropertyDescription("查询指定城市的实时天气")
    public record WeatherRequest(
        @JsonProperty(required = true)
        @JsonPropertyDescription("城市名称，如北京、上海")
        String city
    ) {}

    public String getWeather(String city) {
        // 模拟天气查询（实际项目中调用天气 API）
        // 例如：https://api.openweathermap.org/data/2.5/weather?q={city}
        return String.format("城市：%s，天气：晴，温度：25°C，湿度：60%", city);
    }
}
```

#### 5.2.2 让 AI 调用函数

```java
// AgentService.java —— 核心 Agent 逻辑
package com.example.agent.service;

import com.fasterxml.jackson.databind.ObjectMapper;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Service;
import org.springframework.web.client.RestTemplate;

import java.util.*;

@Service
public class AgentService {

    @Value("${deepseek.api-key}")
    private String apiKey;

    private final RestTemplate restTemplate;
    private final WeatherTool weatherTool;
    private final ObjectMapper objectMapper;

    public AgentService(RestTemplate restTemplate,
                        WeatherTool weatherTool,
                        ObjectMapper objectMapper) {
        this.restTemplate = restTemplate;
        this.weatherTool = weatherTool;
        this.objectMapper = objectMapper;
    }

    public String run(String userMessage) {
        // 1. 构建消息（带 Function Calling 定义）
        List<Map<String, Object>> messages = new ArrayList<>();
        messages.add(Map.of("role", "user", "content", userMessage));

        // 2. 定义可用的函数
        List<Map<String, Object>> tools = List.of(
            Map.of(
                "type", "function",
                "function", Map.of(
                    "name", "get_weather",
                    "description", "查询指定城市的实时天气",
                    "parameters", Map.of(
                        "type", "object",
                        "properties", Map.of(
                            "city", Map.of(
                                "type", "string",
                                "description", "城市名称，如北京、上海"
                            )
                        ),
                        "required", List.of("city")
                    )
                )
            )
        );

        // 3. 第一次调用：AI 决定是否调用函数
        Map<String, Object> requestBody = new HashMap<>();
        requestBody.put("model", "deepseek-chat");
        requestBody.put("messages", messages);
        requestBody.put("tools", tools);
        requestBody.put("temperature", 0.1);

        Map response = callLLM(requestBody);
        Map choice = (Map) ((List) response.get("choices")).get(0);
        Map message = (Map) choice.get("message");

        // 4. 如果 AI 决定调用函数
        if (message.containsKey("tool_calls")) {
            List<Map<String, Object>> toolCalls =
                    (List<Map<String, Object>>) message.get("tool_calls");

            // 把 AI 的回复加入历史
            messages.add(message);

            for (Map<String, Object> toolCall : toolCalls) {
                String functionName = (String) ((Map) toolCall.get("function")).get("name");
                String arguments = (String) ((Map) toolCall.get("function")).get("arguments");

                // 5. 执行实际的函数
                String functionResult = executeFunction(functionName, arguments);

                // 6. 把函数结果加入历史
                messages.add(Map.of(
                    "role", "tool",
                    "tool_call_id", toolCall.get("id"),
                    "content", functionResult
                ));
            }

            // 7. 第二次调用：AI 基于函数结果生成最终回复
            requestBody.put("messages", messages);
            requestBody.remove("tools"); // 不需要再传 tools
            Map finalResponse = callLLM(requestBody);
            Map finalChoice = (Map) ((List) finalResponse.get("choices")).get(0);
            Map finalMessage = (Map) finalChoice.get("message");
            return (String) finalMessage.get("content");
        }

        // 如果不需要调用函数，直接返回
        return (String) message.get("content");
    }

    private String executeFunction(String name, String arguments) {
        try {
            if ("get_weather".equals(name)) {
                Map<String, String> args = objectMapper.readValue(arguments, Map.class);
                return weatherTool.getWeather(args.get("city"));
            }
            return "未知函数：" + name;
        } catch (Exception e) {
            return "函数执行出错：" + e.getMessage();
        }
    }

    private Map callLLM(Map<String, Object> body) {
        // 和之前 ChatService 类似的 HTTP 调用逻辑
        // ...（省略，参考第 2 章）
        return Map.of(); // 占位
    }
}
```

---

### 5.3 Agent 模式入门

Agent = 大模型 + 工具 + 循环决策

```
┌──────────────────────────────────┐
│           Agent 循环              │
│                                   │
│  用户输入                          │
│     ↓                             │
│  思考：我需要做什么？               │
│     ↓                             │
│  决策：应该调用哪个工具？           │
│     ↓                             │
│  执行：调用工具                    │
│     ↓                             │
│  观察：工具返回了什么？             │
│     ↓                             │
│  判断：任务完成了吗？              │
│     ├── 是 → 生成最终回复           │
│     └── 否 → 回到"思考"继续循环    │
│                                   │
└──────────────────────────────────┘
```

**一个简单的 Agent 循环**：

```java
public String agentRun(String task, int maxSteps) {
    List<Map<String, Object>> messages = new ArrayList<>();
    messages.add(Map.of("role", "system", "content",
        "你是一个智能助手。你可以调用工具来完成任务。" +
        "请一步一步思考，每次只调用一个工具。"));
    messages.add(Map.of("role", "user", "content", task));

    for (int step = 0; step < maxSteps; step++) {
        Map response = callLLM(messages);  // 调用大模型
        Map message = getMessage(response);

        if (hasToolCalls(message)) {
            // 执行工具调用
            String toolResult = executeToolCall(message);
            messages.add(message);                              // AI 的决策
            messages.add(Map.of("role", "tool",                 // 工具结果
                "content", toolResult));
            // 继续循环
        } else {
            // 没有工具调用 = 任务完成
            return message.get("content");
        }
    }
    return "任务未在" + maxSteps + "步内完成";
}
```

---

### 5.4 实战项目：AI 个人助理

结合前面学的内容，做一个综合项目：

**功能**：
- 💬 聊天（第 2 章）
- 📄 文档问答（第 4 章）
- 🌤️ 查天气（第 5 章）
- 🔍 搜索网页（Function Calling 调用搜索 API）

**架构**：

```
用户 → ChatController
         ↓
     AgentService（路由器）
         ├── 普通聊天 → ChatService
         ├── 文档问答 → RagService
         ├── 查天气   → WeatherTool
         └── 搜索网页 → SearchTool
```

---

## 第 6 章：流式输出与生产化 —— 从 Demo 到上线

> ⏱ 预计时间：6 小时 | 🎯 目标：让应用体验更好、更省钱、更稳定

### 6.1 流式输出（SSE）

普通模式：等 AI 全部生成完，一次性返回（用户要等很久）

流式模式：AI 生成一个字就返回一个字（ChatGPT 那种打字机效果）

**后端实现**：

```java
// StreamingChatController.java
@RestController
@RequestMapping("/api")
public class StreamingChatController {

    private final RestTemplate restTemplate;

    @PostMapping(value = "/chat/stream", produces = MediaType.TEXT_EVENT_STREAM_VALUE)
    public Flux<String> chatStream(@RequestBody ChatRequest request) {
        return Flux.create(sink -> {
            // 构建请求（stream: true）
            // 逐行解析 SSE 响应
            // 每收到一个 chunk，就 sink.next(content)
            // 完成后 sink.complete()
        });
    }
}
```

**前端接收**：

```javascript
// 使用 EventSource 或 fetch + ReadableStream
const response = await fetch('/api/chat/stream', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ message: userInput })
});

const reader = response.body.getReader();
const decoder = new TextDecoder();

while (true) {
    const { done, value } = await reader.read();
    if (done) break;
    const text = decoder.decode(value);
    // 逐字追加到聊天界面
    appendToLastMessage(text);
}
```

---

### 6.2 语义缓存 —— 省钱利器

很多用户问题其实是重复的（或相似的）：

```
"怎么重置密码？"
"如何修改密码？"      ← 和上面意思一样，但文字不同
"密码忘了怎么办？"     ← 还是同一个问题！
```

**语义缓存**：把问题和答案的 Embedding 存下来，新问题来了先查有没有相似的。

```java
@Service
public class SemanticCache {

    private final EmbeddingModel embeddingModel;
    private final Map<String, CacheEntry> cache = new ConcurrentHashMap<>();

    public Optional<String> get(String question) {
        Embedding questionEmbedding = embeddingModel.embed(question).content();

        for (CacheEntry entry : cache.values()) {
            double similarity = cosineSimilarity(questionEmbedding, entry.embedding);
            if (similarity > 0.95) {  // 相似度 > 95% 命中缓存
                return Optional.of(entry.answer);
            }
        }
        return Optional.empty();
    }

    public void put(String question, String answer) {
        Embedding embedding = embeddingModel.embed(question).content();
        cache.put(question, new CacheEntry(embedding, answer));
    }
}
```

---

### 6.3 限流与费用控制

```java
// 简单的 Token 桶限流器
@Component
public class RateLimiter {
    private final ConcurrentHashMap<String, TokenBucket> buckets = new ConcurrentHashMap<>();

    public boolean tryAcquire(String userId) {
        TokenBucket bucket = buckets.computeIfAbsent(userId,
            k -> new TokenBucket(100, 10));  // 100 Token，每秒补充 10 个
        return bucket.tryConsume(1);
    }
}
```

**费用控制清单**：

| 措施 | 说明 |
|------|------|
| 限制单次最大 Token | max_tokens 设 2000-4000 |
| 用户级别限流 | 每人每天最多 100 次调用 |
| 语义缓存 | 重复问题不调 API |
| 短模型优先 | 简单任务用 gpt-4o-mini / deepseek-chat |
| 监控告警 | 日费用超过预算发通知 |

---

### 6.4 错误处理最佳实践

```java
public String chatWithRetry(String message) {
    int maxRetries = 3;
    for (int i = 0; i < maxRetries; i++) {
        try {
            return callLLM(message);
        } catch (RateLimitException e) {
            // 限流了，等一等再试
            Thread.sleep((long) Math.pow(2, i) * 1000);  // 指数退避
        } catch (TimeoutException e) {
            // 超时，重试
            if (i == maxRetries - 1) throw e;
        }
    }
    throw new RuntimeException("调用失败，已重试 " + maxRetries + " 次");
}
```

---

### 6.5 部署建议

| 环境 | 推荐方案 |
|------|---------|
| 开发测试 | 本地 Docker Compose（Spring Boot + PostgreSQL + Chroma） |
| 生产部署 | K8s / 云服务器，API Key 走配置中心或 K8s Secret |

**Docker Compose 示例**：

```yaml
version: '3.8'
services:
  app:
    build: .
    ports:
      - "8080:8080"
    environment:
      - DEEPSEEK_API_KEY=${DEEPSEEK_API_KEY}
      - SPRING_PROFILES_ACTIVE=prod
    depends_on:
      - postgres
      - chroma

  postgres:
    image: pgvector/pgvector:pg16  # 带向量扩展的 PostgreSQL
    environment:
      POSTGRES_DB: rag_db
      POSTGRES_PASSWORD: secure_password
    volumes:
      - pgdata:/var/lib/postgresql/data

  chroma:
    image: chromadb/chroma:latest
    volumes:
      - chroma_data:/chroma/chroma

volumes:
  pgdata:
  chroma_data:
```

---

## 第 7 章：GitHub 实战项目推荐 —— 向优秀开源项目学习

> ⏱ 预计时间：持续关注 | 🎯 目标：找到适合自己水平的开源项目，边看边学

学完前面 6 章后，你已经能独立搭建 AI 应用了。但自己闷头写代码进步有限——**阅读优秀的开源项目，是提升最快的途径之一**。

本章精选了 GitHub 上最适合 Java + 前端背景学习者的 AI 开源项目，按难度和用途分类。

---

### 7.1 项目总览

```
难度  ★☆☆          ★★☆              ★★★
      │              │                 │
  快速体验型      教程/学习型       生产级平台型
  (点点就能用)   (跟着代码学)      (阅读源码提升)
```

| 难度 | 适合人群 | 学习方式 |
|------|---------|----------|
| ★☆☆ | 刚入门，想先体验 AI 应用长什么样 | 部署运行，理解功能 |
| ★★☆ | 有一定基础，想跟着代码学习 | Clone + 运行 + 调试 + 修改 |
| ★★★ | 想深入理解架构设计 | 阅读源码，学习设计模式 |

---

### 7.2 Java 后端项目（与你的技术栈完美匹配）

#### 🌟 首推：llm-apps-java-spring-ai

| 项目信息 | 详情 |
|----------|------|
| **GitHub** | [ThomasVitale/llm-apps-java-spring-ai](https://github.com/ThomasVitale/llm-apps-java-spring-ai) |
| **难度** | ★★☆ |
| **技术栈** | Spring Boot 3 + Spring AI + Ollama + PGVector + OpenAI |
| **推荐理由** | **Java AI 学习最佳项目，没有之一！** 56 个可运行示例，覆盖手册第 0-6 章全部内容 |

**项目包含的示例（直接对应本手册各章）**：

| 分类 | 示例数量 | 对应手册章节 | 亮点示例 |
|------|---------|-------------|---------|
| 用例 (Use Cases) | 5 个 | 第 2、4 章 | Chatbot、RAG 问答、语义搜索、文本分类 |
| 模型集成 (Models) | 10 个 | 第 1、2 章 | OpenAI / Ollama / Mistral AI 三套方案 |
| Prompt 设计模式 | ~25 个 | 第 3 章 | 模板、结构化输出、多模态、消息角色 |
| Tool Calling | 3 个 | 第 5 章 | OpenAI / Ollama / Mistral 三种实现 |
| 记忆 (Memory) | 4 个 | 第 5 章 | 基础记忆、JDBC、向量存储、Spring Security |
| RAG 流程 | 4 个 | 第 4 章 | 朴素 RAG、高级 RAG、分支 RAG、条件 RAG |
| 数据摄取 | 7 个 | 第 4 章 | JSON/Markdown/PDF/Tika 文档读取与分块 |
| 护栏 (Guardrails) | 2 个 | 第 6 章 | 输入护栏、输出护栏 |
| 可观测性 | 4 个 | 第 6 章 | 模型调用监控、向量存储监控 |

> **学习建议**：每学完手册一章，就去这个项目找对应示例运行一遍。从 `use-cases/chatbot` 开始，逐步深入。

---

#### 🌟 推荐二：LangChat/ai-tutorials

| 项目信息 | 详情 |
|----------|------|
| **GitHub** | [LangChat/ai-tutorials](https://github.com/LangChat/ai-tutorials) |
| **在线文档** | [ai-tutorials.langchat.cn](https://ai-tutorials.langchat.cn/) |
| **难度** | ★★☆ |
| **技术栈** | Java 17 + Maven + LangChain4j 1.10 + JUnit 5 |
| **推荐理由** | **中文友好，0 基础上手，40 篇文档 + 完整测试代码** |

**教程目录（部分）**：

```
01 - LangChain4j 简介
02 - 第一个聊天应用
03 - ChatModel 深入（含流式聊天）
07 - Embedding 模型
08 - 向量存储
10 - RAG 检索增强生成
11 - AI Services 声明式服务
... (共 40 篇)
```

**项目特点**：
- 每个主题都有**独立的测试类**，可以直接运行
- 使用 `.env` 文件统一管理配置，安全规范
- 支持 DeepSeek、OpenAI、通义千问等多种模型
- 代码风格好，有 Lombok、JUnit DisplayName 等最佳实践

> **学习建议**：先看在线文档理解概念，再 clone 代码运行测试，最后自己改参数实验。非常适合配合本手册第 2-5 章同步学习。

---

#### 🌟 推荐三：yu-ai-agent（AI 超级智能体）

| 项目信息 | 详情 |
|----------|------|
| **GitHub** | [liyupi/yu-ai-agent](https://github.com/liyupi/yu-ai-agent) |
| **难度** | ★★★ |
| **技术栈** | Java 21 + Spring Boot 3 + Spring AI + LangChain4j + PgVector + MCP |
| **推荐理由** | **完整全栈 AI 项目，从 0 到 1 构建 Agent** |

**项目内容**：
- **AI 恋爱大师应用**：多轮对话 + RAG 知识库 + 工具调用 + MCP 服务
- **YuManus 自主智能体**：基于 ReAct 模式，能自主搜索、下载、生成 PDF
- 配套完整视频教程 + 文字教程

**学习大纲**（9 期）：
1. 项目总览与架构设计
2. AI 大模型接入（4 种方式）+ 本地部署
3. AI 应用开发：Prompt 工程 + 多轮对话 + 结构化输出
4. RAG 知识库基础：Spring AI + 本地/云知识库
5. RAG 知识库进阶：ETL + 向量数据库 + 检索策略调优
6. 工具调用：6 种工具开发（搜索、文件、抓取、终端、下载、PDF）
7. MCP 协议：3 种使用方式 + MCP Server 开发
8. AI 智能体构建：ReAct + OpenManus 原理 + 自主实现
9. AI 服务化：SSE 接口 + 前端 + Docker + Serverless 部署

> **学习建议**：完成本手册前 6 章后再来看这个项目。它相当于把你学的所有知识串成一个完整的全栈产品，是**简历项目的绝佳素材**。

---

#### 🌟 推荐四：langchain4j-examples（官方示例）

| 项目信息 | 详情 |
|----------|------|
| **GitHub** | [langchain4j/langchain4j-examples](https://github.com/langchain4j/langchain4j-examples) |
| **难度** | ★★☆ |
| **技术栈** | Java + LangChain4j + 多种模型 |
| **推荐理由** | LangChain4j 官方出品，示例最权威 |

包含：Chat Models、Embedding、RAG、Tools、Agents、Image Models、Audio Models 等全方位示例。

---

#### 🌟 推荐五：spring-ai-community/awesome-spring-ai

| 项目信息 | 详情 |
|----------|------|
| **GitHub** | [spring-ai-community/awesome-spring-ai](https://github.com/spring-ai-community/awesome-spring-ai) |
| **难度** | ★☆☆ |
| **推荐理由** | 不是项目，是**资源索引**——收集了 Spring AI 生态的所有教程、工具、项目 |

当你不知道用什么库、看什么教程时，来这里搜就对了。

---

### 7.3 前端项目（发挥你的前端优势）

#### 🌟 Lobe Chat —— 开源 ChatGPT 替代品

| 项目信息 | 详情 |
|----------|------|
| **GitHub** | [lobehub/lobe-chat](https://github.com/lobehub/lobe-chat) |
| **难度** | ★★☆ |
| **Star** | 63K+ |
| **技术栈** | React + TypeScript + Next.js + shadcn/ui |
| **推荐理由** | **最好的 AI 聊天前端开源项目，UI 精美，功能完整** |

**你可以学到**：
- AI 聊天界面的完整前端架构
- 多模型切换（OpenAI / Claude / Gemini / Ollama）
- 流式输出（SSE）的前端实现
- 插件系统和知识库的前端交互
- PWA 离线支持、国际化、主题切换

> **学习建议**：作为前端开发者，这个项目的 UI/UX 设计值得深入研究。你可以参考它的对话组件设计，用在自己的项目中。

---

#### 🌟 NextChat (ChatGPT-Next-Web)

| 项目信息 | 详情 |
|----------|------|
| **GitHub** | [ChatGPTNextWeb/NextChat](https://github.com/ChatGPTNextWeb/NextChat) |
| **难度** | ★★☆ |
| **Star** | 80K+ |
| **技术栈** | React + Next.js |
| **推荐理由** | 部署最简单，5 分钟就能用上自己的 ChatGPT 套壳**

特别适合快速搭建私有的 AI 聊天前端，支持一键 Vercel 部署。

---

#### 🌟 Shadcn Chatbot Kit

| 项目信息 | 详情 |
|----------|------|
| **GitHub** | [blazity/shadcn-chatbot-kit](https://github.com/blazity/shadcn-chatbot-kit) |
| **难度** | ★☆☆ |
| **技术栈** | React + Next.js + shadcn/ui + Vercel AI SDK |
| **推荐理由** | **拿来即用的聊天组件库**，基于 shadcn/ui 构建**

如果你已经在用 shadcn/ui 做前端，这个库能让你几分钟搭出一个 AI 聊天界面。

---

### 7.4 平台型项目（理解 AI 产品全貌）

这些项目比较大，不建议一上来就啃源码。可以先**部署使用**，理解功能和架构后再深入。

| 项目 | GitHub | Star | 一句话介绍 | 适合你吗？ |
|------|--------|------|-----------|-----------|
| **Dify** | [langgenius/dify](https://github.com/langgenius/dify) | 60K+ | 可视化的 LLM 应用开发平台，拖拽式构建 AI 工作流 | ⭐ 强烈推荐！用它快速验证想法，再用 Java 自己实现 |
| **FastGPT** | [labring/FastGPT](https://github.com/labring/FastGPT) | 20K+ | 专注知识库问答，开箱即用的 RAG 平台 | 如果你想快速搭建知识库，用这个比从零写快 10 倍 |
| **MaxKB** | [1Panel-dev/MaxKB](https://github.com/1Panel-dev/MaxKB) | 12K+ | 国产开源知识库问答系统，支持 DeepSeek | 中文场景首选，可直接对接企业微信/钉钉 |
| **Open WebUI** | [open-webui/open-webui](https://github.com/open-webui/open-webui) | 50K+ | 自托管 AI 聊天界面，功能全面 | 想部署私有的 ChatGPT 替代品就用它 |
| **LangChat** | [LangChat/LangChat](https://github.com/LangChat/LangChat) | - | Java 生态的 AI 开发平台，LangChain4j 最佳实践 | Java 开发者必看，完整的 Java AI 全栈方案 |

---

### 7.5 Python 生态精品项目（拓宽视野）

虽然你是 Java 开发者，但这些 Python 项目的**架构思想**值得学习。AI 领域很多创新先出现在 Python 生态。

| 项目 | GitHub | 难度 | 值得学什么 |
|------|--------|------|-----------|
| **awesome-llm-apps** | [Shubhamsaboo/awesome-llm-apps](https://github.com/Shubhamsaboo/awesome-llm-apps) | ★★☆ | 18K+ Star，RAG 和 Agent 应用合集，每个都是独立小项目 |
| **llama_index** | [run-llama/llama_index](https://github.com/run-llama/llama_index) | ★★★ | RAG 框架的架构设计，数据连接器的设计模式 |
| **LangChain** | [langchain-ai/langchain](https://github.com/langchain-ai/langchain) | ★★★ | 理解 LangChain4j 之前，先了解 Python 版的设计哲学 |
| **CrewAI** | [crewai/crewai](https://github.com/crewai/crewai) | ★★☆ | 多 Agent 协作的设计模式 |

---

### 7.6 学习路线图：这些项目怎么配合本手册学？

```
┌──────────────────────────────────────────────────────────┐
│ 阶段          本手册         配套 GitHub 项目               │
├──────────────────────────────────────────────────────────┤
│                                                           │
│ 概念入门      第 0-1 章      直接看手册即可                  │
│     ↓                                                      │
│ 第一个应用    第 2 章        llm-apps-java-spring-ai       │
│                              → use-cases/chatbot           │
│                              LangChat/ai-tutorials         │
│                              → 02-第一个聊天应用             │
│     ↓                                                      │
│ Prompt 工程   第 3 章        llm-apps-java-spring-ai       │
│                              → patterns/prompts-*          │
│                              → patterns/structured-output-*│
│     ↓                                                      │
│ RAG 知识库    第 4 章        llm-apps-java-spring-ai       │
│                              → rag-* (4 种 RAG 模式)       │
│                              LangChat/ai-tutorials         │
│                              → 07-Embedding + 08-向量存储   │
│                              → 10-RAG                      │
│     ↓                                                      │
│ Agent         第 5 章        yu-ai-agent (完整 Agent 项目)  │
│                              llm-apps-java-spring-ai       │
│                              → patterns/tool-calling-*     │
│     ↓                                                      │
│ 生产化        第 6 章        yu-ai-agent → Docker/SSE      │
│                              Dify/FastGPT → 部署体验        │
│     ↓                                                      │
│ 综合实战      第 7 章        yu-ai-agent (全栈完整项目)      │
│                              Lobe Chat (前端参考)           │
│                                                           │
└──────────────────────────────────────────────────────────┘
```

---

### 7.7 如何高效学习开源项目？

**三步法**：

1. **先跑起来**（30 分钟）
   ```bash
   git clone <项目地址>
   # 按照 README 配置环境
   # 跑起来，点点看有什么功能
   ```

2. **带着问题读代码**（2-4 小时）
   - "这个功能是怎么实现的？" → 从 Controller 一路追到 Service
   - "为什么这样设计？" → 看注释、看 Commit 记录、看 Issue 讨论
   - "如果是我会怎么写？" → 对比自己的实现

3. **动手改**（4+ 小时）
   - 换个模型试试（DeepSeek 换成 GPT-4o）
   - 加个新功能（比如加个导出对话的功能）
   - 修个小 Bug 并提 PR（这是简历上非常亮眼的经历）

**不要做的**：
- ❌ 把整个项目代码从头读到尾（效率极低）
- ❌ 只看不跑（不运行永远理解不了）
- ❌ 追求一次看懂 100%（先理解 60%，剩下在实践中补）

---

## 附录 A：推荐资源清单

### 免费课程

| 课程 | 链接 | 时长 |
|------|------|------|
| 吴恩达《ChatGPT Prompt Engineering for Developers》 | [DeepLearning.AI](https://www.deeplearning.ai/short-courses/chatgpt-prompt-engineering-for-developers/) | 1.5h |
| 吴恩达《Building Systems with ChatGPT API》 | [DeepLearning.AI](https://www.deeplearning.ai/short-courses/building-systems-with-chatgpt/) | 1h |
| 吴恩达《LangChain for LLM Application Development》 | [DeepLearning.AI](https://www.deeplearning.ai/short-courses/langchain-for-llm-application-development/) | 1h |
| 吴恩达《Building Agentic RAG with LlamaIndex》 | [DeepLearning.AI](https://www.deeplearning.ai/short-courses/building-agentic-rag-with-llamaindex/) | 1h |

### 必读文档

| 文档 | 链接 |
|------|------|
| DeepSeek API 文档 | [platform.deepseek.com/docs](https://platform.deepseek.com/docs) |
| OpenAI API 文档 | [platform.openai.com/docs](https://platform.openai.com/docs) |
| LangChain4j 文档 | [docs.langchain4j.dev](https://docs.langchain4j.dev/) |
| Spring AI 文档 | [docs.spring.io/spring-ai](https://docs.spring.io/spring-ai/reference/) |

### GitHub 项目

| 项目 | 说明 |
|------|------|
| [langchain4j/langchain4j](https://github.com/langchain4j/langchain4j) | Java 版 LangChain |
| [spring-projects/spring-ai](https://github.com/spring-projects/spring-ai) | Spring 官方 AI 框架 |
| [chroma-core/chroma](https://github.com/chroma-core/chroma) | 轻量向量数据库 |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | 生产级向量数据库 |

### 中文社区

- **即刻**：搜索「AI 产品经理」「AI 开发」相关圈子
- **掘金**：搜索「大模型」「RAG」「Agent」标签
- **知乎**：关注「大语言模型」话题
- **Twitter/X**：关注 @kaboroflow、@dotey 等 AI 开发者

---

## 附录 B：常见问题 FAQ

### Q1: Java 能做 AI 开发吗？是不是必须学 Python？

**完全可以！** 大部分 AI 应用就是 HTTP 调用 + 业务逻辑，Java 完全胜任。Python 在 AI 训练和数据处理方面更占优势，但对于应用开发，你用 Java 没有任何问题。LangChain4j 和 Spring AI 让 Java AI 开发越来越方便。

### Q2: 需要学机器学习和深度学习吗？

**做应用开发不需要。** 就像你不需要懂发动机原理就能开车一样。但如果未来想深入（如微调模型、训练 Embedding），则需要补充 ML 基础。

### Q3: 大模型会胡说八道怎么办？

这就是"幻觉"问题。降低它的方法：
- 用 RAG（让 AI 基于文档回答）
- 降低 Temperature（0.1-0.3）
- 在 Prompt 中明确说"不确定就说不知道"
- Function Calling（让 AI 调用工具获取事实，而不是凭空编造）

### Q4: 怎么选模型？DeepSeek vs GPT-4o vs Claude？

| 场景 | 推荐 |
|------|------|
| 预算有限 / 学习阶段 | **DeepSeek-V3** |
| 复杂推理 / 代码生成 | Claude 3.5 Sonnet |
| 多模态（图片理解） | GPT-4o |
| 私有化部署 | Qwen 2.5 / Llama 3 |

### Q5: API Key 泄露了怎么办？

**立即去平台删除该 Key 并重新生成。** 同时检查是否有异常调用记录和费用。

### 第 0 章自测题答案

1. Token 是大模型处理文本的最小单位，中文约 1 字 = 1-2 Token，1000 Token ≈ 1500 中文字。
2. Temperature 0.1 输出确定性高，适合代码/事实问答；1.0 创造性高，适合写作/头脑风暴。
3. Embedding 将文字转成向量，用于计算语义相似度，是 RAG 检索的基础。
4. RAG = Retrieval-Augmented Generation（检索增强生成），解决了大模型知识过时、不懂私有文档的问题。
5. 普通对话只输出文字，Function Calling 让 AI 输出"调用哪个函数"的结构化指令。

---

## 附录 C：Java AI 工具栈速查

```
┌─────────────────────────────────────────────────────┐
│                    Java AI 技术栈                      │
├─────────────────────────────────────────────────────┤
│                                                       │
│  应用层                                               │
│  ├── Spring Boot 3.x         后端框架                  │
│  ├── Spring AI                官方 AI 集成框架          │
│  └── LangChain4j             社区 AI 编排框架           │
│                                                       │
│  LLM 调用层                                           │
│  ├── OkHttp / WebClient       HTTP 客户端              │
│  ├── Retrofit + OpenAI spec  类型安全调用              │
│  └── LangChain4j Models      统一模型接口              │
│                                                       │
│  向量存储层                                           │
│  ├── PgVector                 PostgreSQL 向量扩展      │
│  ├── Milvus                   生产级向量数据库          │
│  ├── Chroma（Python）         学习用轻量数据库          │
│  └── Qdrant                   高性能向量数据库          │
│                                                       │
│  文档处理层                                           │
│  ├── Apache PDFBox            PDF 解析                 │
│  ├── Apache POI               Word/Excel 解析          │
│  └── Apache Tika              通用文档解析              │
│                                                       │
│  生产化层                                             │
│  ├── Spring WebFlux + SSE     流式输出                 │
│  ├── Redis                    语义缓存                  │
│  ├── Micrometer + Prometheus  监控                     │
│  └── Resilience4j             限流/熔断                 │
│                                                       │
└─────────────────────────────────────────────────────┘
```

---

## 附录 D：术语表

| 术语 | 英文 | 解释 |
|------|------|------|
| 大语言模型 | LLM (Large Language Model) | 用海量文本训练的超大 AI 模型 |
| 提示词 | Prompt | 发给 AI 的输入文本 |
| 提示词工程 | Prompt Engineering | 设计和优化 Prompt 的方法 |
| 令牌 | Token | 大模型处理文本的最小单位 |
| 上下文窗口 | Context Window | AI 一次能记住的最大文本量 |
| 温度 | Temperature | 控制输出随机性的参数 (0-2) |
| 嵌入 | Embedding | 将文字转成数字向量 |
| 向量数据库 | Vector Database | 存储和搜索向量的数据库 |
| 检索增强生成 | RAG | 先查资料再回答的模式 |
| 函数调用 | Function Calling | 让 AI 调用外部函数 |
| 智能体 | Agent | 能自主使用工具完成任务 |
| 幻觉 | Hallucination | AI 编造虚假信息 |
| 少样本提示 | Few-Shot | 给 AI 示例来引导输出 |
| 思维链 | Chain of Thought (CoT) | 让 AI 一步步推理 |
| 流式输出 | Streaming / SSE | 逐字返回，打字机效果 |
| 微调 | Fine-tuning | 在特定数据上继续训练模型 |
| 语义缓存 | Semantic Cache | 用语义相似度做缓存 |

---

## 📋 学习检查清单

打印或复制这份清单，每完成一项就打勾 ✅

### 第 0 章：概念扫盲
- [ ] 能解释 AI → ML → DL → LLM 的关系
- [ ] 理解 Token、Prompt、Temperature、Embedding 是什么
- [ ] 能说出 RAG 和 Function Calling 的区别

### 第 1 章：环境准备
- [ ] 注册了 DeepSeek / OpenAI 账号
- [ ] 拿到了 API Key 并安全保存
- [ ] 用 curl 成功调用了一次 API

### 第 2 章：第一个 AI 应用
- [ ] 创建了 Spring Boot 项目
- [ ] 跑通了 ChatController → ChatService → DeepSeek API
- [ ] （可选）搭了前端聊天页面

### 第 3 章：Prompt 工程
- [ ] 理解了 Prompt 四大要素（角色、任务、格式、约束）
- [ ] 用 Few-Shot 成功引导了 AI 输出
- [ ] 用思维链让 AI 推理了复杂问题
- [ ] 管理了 Prompt 模板（不硬编码）

### 第 4 章：RAG 知识库
- [ ] 理解了 RAG 的完整流程
- [ ] 用 Python 或 Java 搭建了 RAG 原型
- [ ] 成功导入文档并基于文档问答
- [ ] 调过 chunk_size、top_k 等参数

### 第 5 章：Function Calling 与 Agent
- [ ] 实现了至少一个 Function Calling（如查天气）
- [ ] 理解了 Agent 循环（思考→决策→执行→观察）
- [ ] 搭建了一个综合应用（聊天 + RAG + 工具）

### 第 6 章：生产化
- [ ] 实现了流式输出（SSE）
- [ ] 理解了语义缓存的原理
- [ ] 加了限流和错误重试
- [ ] 了解了 Docker 部署方式

### 第 7 章：GitHub 实战项目
- [ ] Clone 并运行了 llm-apps-java-spring-ai 的 chatbot 示例
- [ ] 跟着 LangChat/ai-tutorials 完成了至少 5 个教程
- [ ] 部署体验了 Dify 或 FastGPT
- [ ] 浏览了 Lobe Chat 的前端源码
- [ ] 完成了 yu-ai-agent 全栈项目（选做）

---

> 🎉 **恭喜你！** 完成全部检查清单后，你已经是一名合格的 AI 应用开发者了。
>
> 接下来，建议你选择一个真实场景（比如团队的知识库问答系统），用学到的知识从零搭建，这才是最好的巩固方式。

---

*本手册 v1.1 | 2025 年 7 月 | 如有问题或建议，请联系知识库维护人*
