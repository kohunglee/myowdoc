
好的，我给你一个完整方案，**把你 Node.js 的 DeepSeek 温暖度检测代码部署到 Cloudflare Workers**，并开放一个 REST API：

`POST https://api.openworld.zone/WarmthScore/`，返回 JSON `{ "score": 8.70 }`。

---

## 1️⃣ 准备 Cloudflare Worker 环境

1. 安装 **Wrangler CLI**（Cloudflare Workers 官方工具）：
    

`npm install -g wrangler`

2. 登录 Cloudflare：
    

`wrangler login`

3. 创建新项目：
    

`wrangler generate warmth-api cd warmth-api`

---

## 2️⃣ 配置 API Key

在 **Cloudflare Worker 环境变量**里存储 DeepSeek API Key：

`wrangler secret put DEEPSEEK_API_KEY`

输入你在 DeepSeek 的 API Key。Cloudflare Worker 内通过 `env.DEEPSEEK_API_KEY` 访问。

---

## 3️⃣ 编写 Worker 代码

打开 `src/index.js`（如果是新 Worker，可能叫 `index.js` 或 `worker.js`），改成下面内容：

``export default {   async fetch(request, env) {     try {       if (request.method !== "POST") {         return new Response(JSON.stringify({ error: "POST only" }), { status: 405, headers: { "Content-Type": "application/json" } });       }        const { text } = await request.json();       if (!text || typeof text !== "string") {         return new Response(JSON.stringify({ score: 0.00 }), { headers: { "Content-Type": "application/json" } });       }        const payload = {         model: "deepseek-chat",         messages: [           {             role: "system",             content: ` 你是一个严格的温暖度评分分类器： - 输出数字范围 0.00 - 10.00，两位小数 - 严格零容忍阴阳怪气、暗示、灌水、无逻辑、不推荐内容 → 返回 0.00 - 正常内容输出温暖度 - 输出格式：只有数字，两位小数             `           },           { role: "user", content: text }         ],         stream: false       };        const resp = await fetch("https://api.deepseek.com/chat/completions", {         method: "POST",         headers: {           "Content-Type": "application/json",           "Authorization": `Bearer ${env.DEEPSEEK_API_KEY}`         },         body: JSON.stringify(payload)       });        const data = await resp.json();       const scoreRaw = data?.choices?.[0]?.message?.content?.trim() || "0.00";       // 保证是数字格式，两位小数       const score = parseFloat(scoreRaw).toFixed(2);        return new Response(JSON.stringify({ score: parseFloat(score) }), { headers: { "Content-Type": "application/json" } });      } catch (err) {       return new Response(JSON.stringify({ score: 0.00, error: err.message }), { headers: { "Content-Type": "application/json" } });     }   } }``

---

## 4️⃣ 配置路由

1. 打开 `wrangler.toml`，加入你的自定义域名路由：
    

`name = "warmth-api" main = "src/index.js" compatibility_date = "2025-11-23"  [[routes]] pattern = "api.openworld.zone/WarmthScore/*"`

> 注意 `pattern` 这里指定了路径 `/WarmthScore/*`，Cloudflare 会匹配所有请求。

---

## 5️⃣ 部署

`wrangler publish`

部署成功后，你的接口就可以访问了：

`curl -X POST "https://api.openworld.zone/WarmthScore/" \ -H "Content-Type: application/json" \ -d '{"text":"你写的真好，看了心情很舒服！"}'`

返回示例：

`{   "score": 8.70 }`

---

## 6️⃣ 优化建议

- **超严格安全**：可以在 `fetch` 前加一层正则检查，如果含有非法字符或极端敏感词，直接返回 `0.00`，避免调用 DeepSeek API 浪费 token。
    
- **缓存**：对重复评论可以缓存 score，提高效率，降低调用成本。
    
- **多语言支持**：中文 + 英文 prompt 已经可以覆盖大部分情况。
    

---

我可以帮你写一个 **增强版 Worker**，内置：

1. 零容忍阴阳怪气/暗示
    
2. 无逻辑/灌水直接 0
    
3. 自动两位小数
    
4. 可同时兼顾中文和英文输入
    

然后直接接入你的评论区。