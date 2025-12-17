阻止 Ahrefs、Semrush、Moz 等 SEO 工具抓取你的网站，通常是为了**保护商业机密**（不让竞争对手轻易分析你的反向链接、关键词策略）或者**节省服务器资源**。

这是一场“猫鼠游戏”。最有效的方法是**分层防御**。

鉴于你之前提到使用了 **Cloudflare**，这是最强、最简单的防线。

以下是由于浅入深的三种方案：

---

### 第一层：君子协定 (robots.txt)

这是最基础的。正规的 SEO 工具（Ahrefs, Semrush, Majestic）都会遵守 robots.txt 协议。虽然这防不住流氓爬虫，但能防住 90% 的主流 SEO 工具。

在你的网站根目录 static/robots.txt (Hugo) 中添加：

codeText

```
User-agent: AhrefsBot
Disallow: /

User-agent: SemrushBot
Disallow: /

User-agent: SemrushBot-SA
Disallow: /

User-agent: DotBot
Disallow: /

User-agent: MJ12bot
Disallow: /

User-agent: PetalBot
Disallow: /

User-agent: BLEXBot
Disallow: /

User-agent: AhrefsSiteAudit
Disallow: /

User-agent: DataForSeoBot
Disallow: /

# 允许 Google 和 Bing
User-agent: *
Allow: /
```

- **AhrefsBot**: Ahrefs 的爬虫。
    
- **SemrushBot**: Semrush 的爬虫。
    
- **DotBot**: Moz 的爬虫。
    
- **MJ12bot**: Majestic 的爬虫（查外链很厉害）。
    
- **PetalBot**: 华为的，有时候很暴力，不想做国内SEO可以封。
    

---

### 第二层：Cloudflare WAF 防火墙（核武器，强烈推荐）

robots.txt 只是个“请勿打扰”的牌子，Cloudflare 则是门口带枪的保安。它能在请求到达你服务器之前直接拦截，**节省流量和服务器算力**。

**操作步骤：**

1. 登录 Cloudflare -> 进入你的域名。
    
2. 左侧菜单选择 **Security (安全性)** -> **WAF (Web 应用程序防火墙)**。
    
3. 点击 **Create rule (创建规则)**。
    
4. **规则名称**：Block SEO Bots
    
5. **Field (字段)** 选择 User Agent。
    
6. **Operator (运算符)** 选择 contains (包含)。
    
7. **Value (值)** 填入 AhrefsBot。
    
8. 点击 OR (或者)，重复步骤 5-7，填入 SemrushBot，DotBot，MJ12bot 等等。
    
9. **Choose action (选择行动)**：选择 **Block (阻止)**。
    
10. **Deploy (部署)**。
    

**更高级的 Cloudflare 技巧 (Expression)：**  
你可以直接点击 "Edit expression" 粘贴这个逻辑：

codeText

```
(http.user_agent contains "AhrefsBot") or 
(http.user_agent contains "SemrushBot") or 
(http.user_agent contains "DotBot") or 
(http.user_agent contains "MJ12bot") or 
(http.user_agent contains "DataForSeoBot") or 
(http.user_agent contains "BLEXBot") or 
(http.user_agent contains "SeekportBot")
```

---

### 第三层：Web 服务器配置 (Nginx)

如果你不想用 Cloudflare，或者想做双重保险，可以在 Nginx 配置里直接拦截。

在你的 nginx.conf 或站点配置文件 server 块中添加：

codeNginx

```
if ($http_user_agent ~* (AhrefsBot|SemrushBot|DotBot|MJ12bot|DataForSeoBot|BLEXBot|SeekportBot)) {
    return 403;
}
```

- ~* 表示不区分大小写的正则匹配。
    
- return 403 表示直接返回“禁止访问”，对方什么也拿不到。
    

---

### 这样做有什么后果？

1. **竞争对手变瞎**：他们在 Ahrefs 里搜你的域名，会显示“无法抓取”或者数据长期不更新。他们看不到你的新页面、看不到你新做的内链结构。
    
2. **外链数据消失**：如果别的网站连了你，但 MJ12bot 爬不到你的站，Majestic 的外链报告里可能就不会收录这个链接的“目标页面信息”（虽然他们爬发链接的那个站还是能发现链接指向你，但无法分析你的页面内容）。
    
3. **不影响 Google收录**：只要你不封 Googlebot，你的 SEO 排名不会受负面影响。实际上，减少了垃圾爬虫，你的服务器响应速度变快，可能反而利好 SEO。
    

**建议**：最少要做 **Cloudflare WAF** 这一步，最省心且极其有效。