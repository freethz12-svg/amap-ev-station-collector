# AMap EV Station Collector

用于复现“高德 Web API 建候选名单 → 筛选对外营业汽车充电站 → Android 高德 APP + ADB 截图取证 → 价格解析与复核 → Excel 汇总”的 Codex Skill。

默认业务范围：每个输入目标周边 **3 公里**。

## 安装

将本仓库克隆或下载到 Codex skills 目录：

```powershell
git clone https://github.com/freethz12-svg/amap-ev-station-collector.git "$env:USERPROFILE\.codex\skills\amap-ev-station-collector"
```

重启或刷新 Codex 后调用：

```text
使用 $amap-ev-station-collector，读取目标 Excel，采集每个目标3公里内的对外营业汽车充电场站，并生成经过截图复核的汇总 Excel。
```

## 内容

- `SKILL.md`：Skill 入口、适用范围和不可违反的原则。
- `references/runbook.md`：完整操作流程、过滤规则、ADB 状态机、截图规范、价格转换、漏项复核和 Excel 验收标准。
- `agents/openai.yaml`：Codex UI 元数据。

## 使用要求

- 自备高德 Web 服务 Key，不要把 Key 写入仓库。
- 手机已安装高德地图并开启无线 ADB 调试。
- 严禁上传真实 API Key、ADB 设备信息、原始截图、目标名单或经营数据。
- 高德 API 与 APP 的使用须遵守相应服务条款和适用法律。
