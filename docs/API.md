# API 文档 · GhostAI 知识库

> 团队版 / 企业版可用。Dify Service API 100% 兼容。

## 拿到 API Key

1. 登录控制台 → 选择应用 → "**访问 API**"
2. 点 "**API Key**" → "**新建 Secret Key**"
3. 复制密钥（格式：`app-xxx...`）

## 基础地址

```
https://www.ghostai.top/v1
```

## 对话接口

最常用的 endpoint：

### POST /v1/chat-messages

```bash
curl -X POST https://www.ghostai.top/v1/chat-messages \
  -H "Authorization: Bearer app-xxxxx" \
  -H "Content-Type: application/json" \
  -d '{
    "inputs": {},
    "query": "我们公司的退货政策是什么？",
    "response_mode": "blocking",
    "user": "user-uuid-001"
  }'
```

返回：
```json
{
  "answer": "根据《售后服务政策》：商品签收后 7 天内可申请无理由退货...",
  "conversation_id": "abc-123",
  "message_id": "msg-456",
  "metadata": {
    "retriever_resources": [{
      "document_name": "售后服务政策v3.pdf",
      "segment_position": 12,
      "content": "...",
      "score": 0.85
    }]
  }
}
```

### 流式返回（SSE）

```bash
curl -X POST https://www.ghostai.top/v1/chat-messages \
  -H "Authorization: Bearer app-xxxxx" \
  -H "Content-Type: application/json" \
  -d '{
    "query": "...",
    "response_mode": "streaming",
    "user": "user-001"
  }'
```

Stream 每个 chunk 是一个 JSON 行，前缀 `data: `（SSE 协议）。

## 知识库 API（管理用）

> 这是 Dataset API（独立 Key）。控制台 → 知识库 → "API 访问"。

### 上传文档（text）

```bash
curl -X POST https://www.ghostai.top/v1/datasets/{dataset_id}/document/create-by-text \
  -H "Authorization: Bearer dataset-xxxxx" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "公司新政策 2026-Q2",
    "text": "...全文...",
    "indexing_technique": "high_quality",
    "process_rule": {"mode": "automatic"}
  }'
```

### 检索（向量查询）

```bash
curl -X POST https://www.ghostai.top/v1/datasets/{dataset_id}/retrieve \
  -H "Authorization: Bearer dataset-xxxxx" \
  -H "Content-Type: application/json" \
  -d '{
    "query": "退货政策",
    "retrieval_model": {
      "search_method": "semantic_search",
      "reranking_enable": false,
      "score_threshold_enabled": false,
      "top_k": 5
    }
  }'
```

## 客户端集成示例

### Python

```python
import requests

r = requests.post(
    "https://www.ghostai.top/v1/chat-messages",
    headers={"Authorization": "Bearer app-xxxxx"},
    json={
        "query": "退货政策",
        "response_mode": "blocking",
        "user": "u-001",
    },
)
print(r.json()["answer"])
```

### Node.js

```javascript
const res = await fetch("https://www.ghostai.top/v1/chat-messages", {
  method: "POST",
  headers: {
    "Authorization": "Bearer app-xxxxx",
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    query: "退货政策",
    response_mode: "blocking",
    user: "u-001",
  }),
});
const { answer } = await res.json();
console.log(answer);
```

### Go

```go
import (
    "bytes"
    "encoding/json"
    "io"
    "net/http"
)

body, _ := json.Marshal(map[string]interface{}{
    "query": "退货政策",
    "response_mode": "blocking",
    "user": "u-001",
})
req, _ := http.NewRequest("POST", "https://www.ghostai.top/v1/chat-messages",
    bytes.NewBuffer(body))
req.Header.Set("Authorization", "Bearer app-xxxxx")
req.Header.Set("Content-Type", "application/json")

resp, _ := http.DefaultClient.Do(req)
defer resp.Body.Close()
result, _ := io.ReadAll(resp.Body)
```

## 常用接入场景

### 嵌入企业官网（最简）

```html
<iframe
  src="https://www.ghostai.top/chatbot/abc-share-token"
  style="width:100%; height:600px; border:none;">
</iframe>
```

控制台 → 应用 → "**网站嵌入**" 获取专属链接。

### 浮动客服按钮

```html
<script
  async
  src="https://www.ghostai.top/embed.min.js"
  data-token="abc-share-token">
</script>
```

### 接微信公众号 / 企业微信

直接用 [Dify 官方文档](https://docs.dify.ai/) 的接入指南，所有 endpoint 把 `dify.ai` 换成 `www.ghostai.top` 即可。

## Rate Limit

- **个人版**：30 req/min
- **团队版**：100 req/min
- **企业版**：1000 req/min（可议）

超出返 429 Too Many Requests。

## 完整 API 列表

100% 兼容 Dify v1 API。完整 endpoint 见 [Dify 官方 API 文档](https://docs.dify.ai/getting-started/readme/model-providers/openai-api-compatible)。所有 endpoint 把 `https://api.dify.ai` 替换为 `https://www.ghostai.top` 即可。

下一步 → [联盟分销](AFFILIATE.md)
