## IoT Location Anti-Loss Example

機器人防走失定位回報：

Request:
ez://h2plus-001.nug8.com/location?lat=22.6273&lon=120.3014&bat=87

Response:
ez://h2plus-001.nug8.com/status?lat=22.6273&lon=120.3014&bat=87&ts=2026-04-16T09:38:00Z

說明：
- lat/lon: WGS84座標
- bat: 電量百分比 0-100  
- ts: UTC時間戳，防重放攻擊
- 整個URI < 200字元，適合機器人低頻寬
