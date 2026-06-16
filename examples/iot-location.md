## IoT Location Anti-Loss Example

機器人定時回報位置給保全系統，發完就睡：

ez://guard.nug8.com/report?id=h2plus-001&lat=22.6273&lon=120.3014&bat=87&ts=2026-04-16T09:38:00Z

說明：
- id: 設備ID，h2plus-001代表第1台H2 Plus
- lat/lon: WGS84座標，定位用
- bat: 電量百分比 0-100，低電量告警用  
- ts: UTC時間戳 ISO8601，防重放攻擊
- 整個URI 148字元，低頻寬機器人0壓力
- 業務邏輯：機器人只發不收，伺服器收到存DB不回應
