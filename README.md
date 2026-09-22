# 目的地行程攻略生成器

一个可复用的 AI 旅行规划 Skill，用小时级日历组织行程，配合地图定位、路线顺序和交通接驳卡。适合规划新目的地，也适合持续修改已有攻略。

## 包含什么

- 按地理位置、开放时间和体力安排每日路线，保留固定预约与休息时间。
- 修改景点时同时检查时间、内容、地图定位以及前后两段交通。
- 默认步行距离达到 1.5km 时补蓝色接驳卡，格式为「打车N分钟 Xkm」；这个阈值可按个人偏好调整。
- 蓝色表示交通，绿色表示餐饮和酒店休息，橙色表示游玩、课程、SPA、咖啡厅等活动。
- 附可编辑的 HTML 日历模板与本地校验脚本。

## 使用方法

点击本仓库的 **Code → Download ZIP** 并解压，将整个目录交给支持 Skill 的 AI 工具，要求它读取 `SKILL.md`，按照其中的流程制作攻略。也可以直接将本目录安装到工具支持的技能目录，命名为 `destination-trip-planner`。

示例请求：

> 使用 destination-trip-planner，为我规划大阪和京都 7 天行程。日期是……，酒店是……，已预约的活动有……。每天 9 点以后出门，喜欢咖啡、街区和美食，避免太累。请查证营业时间和交通，输出带地图的 HTML 日历。

后续可以继续要求：

> 把第三天下午换成这家店，同时更新地图和前后交通，达到接驳阈值就补卡。

## 目录

```text
SKILL.md                         核心指令
agents/openai.yaml               技能显示信息
references/planning-rules.md     规划与接驳规则
references/data-schema.md        模板数据格式
assets/itinerary-template.html   通用 HTML 模板
scripts/validate_itinerary_html.mjs  本地校验脚本
```

模板中的 Example 地点和日期仅用于展示结构，使用前必须替换为实际行程。地图需要联网；整日途经点的呈现取决于 Google Maps 的嵌入支持，不能保证所有点都在嵌入地图中显示，需实际检查并使用「大图」核对。

## 校验

安装 Node.js 后，在仓库目录运行：

```bash
node scripts/validate_itinerary_html.mjs assets/itinerary-template.html
```

脚本检查 JavaScript 语法、事件重叠、卡片类型和接驳卡分钟数的一致性。它不会联网核实车程、营业时间或真实步行距离，这些仍需 AI 查证。仅对自己生成或可信的 HTML 运行：脚本会求值其中的日程数据。

本仓库提供规划方法和示例，不含任何个人旅行安排、酒店预订或账户密钥。
