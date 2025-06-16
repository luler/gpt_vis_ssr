# gpt_vis_ssr

服务化部署 gpt-vis-ssr，可以作为MCP工具 mcp-server-chart 私有制图服务后端

> 参考1：https://github.com/antvis/GPT-Vis/tree/main/bindings/gpt-vis-ssr

> 参考2：https://github.com/antvis/mcp-server-chart

# 安装

docker-compose.yml

```
version: '3.8'

services:
  gpt-vis-ssr:
    image: ghcr.io/luler/gpt_vis_ssr:latest
    ports:
      - 3000:3000
    volumes:
      - ./images:/app/public/images
    environment:
      - NODE_ENV=production
      - TZ=Asia/Shanghai
    restart: unless-stopped
```

运行

```
docker-compose up -d
```

# 使用
- 提供接口：`POST` http://127.0.0.1:3000/render
- 请求参数：
```json
{
    "type": "column",
    "data": [
        {
            "category": "交通",
            "value": 2000
        },
        {
            "category": "住宿",
            "value": 1200
        },
        {
            "category": "吃喝",
            "value": 1000
        },
        {
            "category": "门票",
            "value": 800
        },
        {
            "category": "其他",
            "value": 300
        }
    ],
    "title": "旅行计划费用统计",
    "axisXTitle": "费用类别",
    "axisYTitle": "金额 (元)"
}
```
- 返回数据
```json
{
    "success": true,
    "resultObj": "http://127.0.0.1:3000/images/c1e17b0f-513d-46de-ae74-e0d20ae52bd7.png"
}
```

- 结果图示例
![](./example.png)