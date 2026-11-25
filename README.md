# 复刻实验室

三个小产品的 PWA 复刻，纯前端、无后端、数据只存本机。

- 刷手机刹车（对标 Curiosity Quench）：<https://asdffr12.github.io/clone-lab/brake/>
- 稳住（对标 Rootd）：<https://asdffr12.github.io/clone-lab/calm/>
- 文字变 PPT（对标 MagicSlides）：<https://asdffr12.github.io/clone-lab/slides/>

首页：<https://asdffr12.github.io/clone-lab/>

## 是什么

不是像素级克隆，复刻的是核心流程：

- **刹车**：想刷手机 → 随机兴趣微任务 → 90 秒倒计时 → 记录 → 连续天数。兴趣可自建，有 7 天柱状图、JSON 备份。
- **稳住**：呼吸（4-7-8 / 4-4-4 / 方箱）→ 5-4-3-2-1 感官锚定 → 前后打分 → 记录。有 7 天柱状图、JSON 备份。
- **变 PPT**：粘文章 → 规则切页与要点提炼（去口语词、长句切块、同页去重）→ 改字 / 加页 / 排序 → 全屏预览 → 导出 PPTX、网页或 Markdown。

## 技术上

- 每个应用是一个自包含的 HTML（CSS/JS 全内联），`slides` 内联了 PptxGenJS 3.12.0，所以接近 500KB。
- 每个目录有独立 `manifest.webmanifest`，可安装到桌面/主屏；`sw.js` 做网络优先 + 缓存兜底。
- 数据存在 `localStorage`：`cq.v1`、`rootd.v1`，PPT 不存内容。
- 部署在 GitHub Pages，相对路径，换到任意子目录也能用。

## 更新

改页面后把 `sw.js` 的 `CACHE` 版本号 +1，提交推送即可。详见 [DEPLOY.md](DEPLOY.md)。

## 边界

- 没有接模型：变 PPT 是规则提炼，不是 AI 语义理解。
- 没有账号与云同步：换设备要手动导出/导入 JSON。
- 不是原生安装包：要上 App Store / Google Play 还需要开发者账号、签名和 Capacitor 壳。
