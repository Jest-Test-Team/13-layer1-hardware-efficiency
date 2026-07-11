# Layer-1 Hardware Efficiency

**中文名稱：** 跨平台硬體效率與健康監測  
**建築學來源：** Building Physics and Envelope Performance（建築物理與外殼效能）

## 核心問題

> Windows、macOS、Linux 裝置的 CPU/GPU/記憶體/磁碟/電源與熱狀態是否有效率且可持續？

## Problem statement

endpoint telemetry 多以故障或安全為中心，缺乏 workload-to-energy、thermal throttling、battery wear 與 embodied lifecycle 的整體視角。

## Inputs

- OS performance counters
- RAPL/powermetrics/vendor telemetry
- battery SMART/NVMe data
- process/workload tags
- device inventory


## Outputs

- Workload Energy Profile
- thermal/throttle incidents
- battery and disk health
- right-sizing and replacement advice


## Primary metrics

| Metric ID | 初始用途 |
|---|---|
| `joules_per_work_unit` | 建立 baseline、趨勢與 review trigger；正式公式見後續 metric registry。 |
| `idle_waste_ratio` | 建立 baseline、趨勢與 review trigger；正式公式見後續 metric registry。 |
| `thermal_throttle_time` | 建立 baseline、趨勢與 review trigger；正式公式見後續 metric registry。 |
| `battery_health_delta` | 建立 baseline、趨勢與 review trigger；正式公式見後續 metric registry。 |
| `io_amplification` | 建立 baseline、趨勢與 review trigger；正式公式見後續 metric registry。 |
| `device_lifetime_score` | 建立 baseline、趨勢與 review trigger；正式公式見後續 metric registry。 |


## MVP scope

1. 跨平台 agent collectors
2. 本機隱私過濾
3. 時間序列 ingest
4. workload 效率與異常 dashboard


## Out of scope for MVP

- 自動執行高風險變更
- 以單一分數取代專業審查
- 未經授權蒐集個人、員工、病患或客戶敏感資料
- 宣稱已建立普遍適用的因果關係

## Repository contract

- `project.yaml`：machine-readable project manifest
- `api/openapi.yaml`：最小 ingestion / assessment API
- `schemas/event.schema.json`：事件資料契約
- `docs/architecture.md`：邊界、資料流與 implementation slices
- `docs/threat-model.md`：安全、隱私與濫用風險
- `examples/sample-event.json`：合成資料範例

## First implementation milestone

先完成 **single-tenant, synthetic-data, read-only analysis**。在證據追溯、權限、資料保留與人工覆核尚未建立前，不進入真實組織或個人資料環境。
