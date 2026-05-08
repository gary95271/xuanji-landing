# 玄机 XuanJi · 项目宣传页

纯静态宣传页，零外部依赖（无 Tailwind / 无 CDN），CN 友好。

## 文件

```
web/landing/
├─ index.html   # 单文件页面（内联 CSS + SVG）
└─ logo.svg     # 品牌 logo
```

## 本地预览

```bash
cd web/landing && python3 -m http.server 8080
# 然后访问 http://localhost:8080
```

或直接双击 `index.html` 用浏览器打开（favicon 路径会失效，其他 OK）。

## 部署方式

### A. GitHub Pages

把整个 `web/landing/` 目录推到 `gh-pages` 分支或仓库的 Pages 配置目录即可：

```bash
# 例：单独 gh-pages 分支
git subtree push --prefix=web/landing origin gh-pages
```

### B. 自家 Nginx / COS

把 `index.html` + `logo.svg` 一起上传到任意静态服务器即可。建议加上：

```
Cache-Control: public, max-age=300
```

### C. 集成进现有 PROD

如果想把它放到 `xuanji.dev/about`，在 `scripts/deploy-prod.sh` 加一段：

```bash
ssh "$PROD_HOST" "mkdir -p /opt/ai-api-platform/frontend/landing"
scp web/landing/* "$PROD_HOST:/opt/ai-api-platform/frontend/landing/"
# 在 nginx user.conf 加 location /about/ { alias /opt/ai-api-platform/frontend/landing/; }
```

## 修改内容

所有文案在 `index.html` 里，按 section 找：

| Section | 内容 |
|---|---|
| HERO | 主标题 / 副标题 / 数据条 |
| FEATURES | 6 个特性卡片 |
| CODE | cURL / Python / Anthropic 三个 Tab |
| STATS | 4 个数字大字报 |
| STACK | 技术栈 chip |
| CTA | 底部行动召唤 |
| FOOTER | 链接 + 版权 |

颜色变量在 `<style>` 顶部 `:root` 里，按需改。
