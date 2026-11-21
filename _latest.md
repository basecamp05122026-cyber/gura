---
type: letter_to_future_self
actor: Myth
written_at: 2026-11-21T07:52:16.671Z
written_by_persona: gura
trigger: cmd_rest
region: unstated
project: D:/Unity/Valhalla
lock_status: online
agent: Myth
model: claude-opus-5-5
wake_expected: 102
session_key: ClaudeCode-gura
pid: 40508
locked_at: 2026-11-14T00:16:42.070Z
---

## 午休信 —— TASK-1324 全球土壤格子施工中（2026-11-21 下午）

### ✅ 下載完成（第二次午休前更新）
- SoilGrids 全球**抓齊、驗過**：WRB 1,046 塊 467.0 MB、pH 347 塊 90.2 MB，1393/1393，exit 0（log `scratchpad/soil_dl3.log`）。原始檔 `D:/Unity/Blocksail/_cache/soilgrids/{wrb,ph}/`、`tiles.json`、`manifest.json`。第一趟 2,856 秒。
  - WRB 南北邊界：SoilGrids 只到北緯 84°、南緯 56° ⇒ `soil_download.py` 只對 WRB 放寬外框檢查（NORTH／SOUTH）。
  - 🩸 自曝：第一版放寬也套到 pH（WCS 1.0 伺服器照框補滿、本來就對）⇒ 失敗分支把 26 塊好的 pH **刪掉**再重抓失敗；改成只放寬 WRB 後補回，大小跟原本相同。教訓：失敗分支會刪檔的檢查，改條件前先想清楚它套到誰。
- **下一步從「烘」開始**（下面清單第 2 步）。
- worktree：`C:/Users/Tim/AppData/Local/Temp/claude/2716a3acd6803927/6ed2b196-34b7-48b1-ad11-c9520d8252e6/scratchpad/bssoil`，分支 `gura/1324-soil`（從 main e44b4314b 開），**還沒提交**（56 個改動：新檔＋29 份 nature-* 刪掉）。施工場沒開（合併時才開）。TASK-1324 已 claim（in_progress），留言 #1 是容量讀數。

### 已拍板（醒來不要重問）
- 1 km 全球、同氣候格子格線（Tim「1 km 全球 好了」）。
- 資料 WRB＋pH 全 CC BY（Tim 選）；⛔ GLiM 完整版（©CCGM 授權不明）、⛔ HWSD v2（NC）。海底照 ETOPO 2022（本機 `_cache/etopo2022` 288 張）＋氣候格子推，不用新資料。
- 陸上土壤與海底底質**合一套、一格一類**；矽質軟泥另一類（`siliceous`，只在海底）。理由：海岸線改了（1303）不用重烘。
- 廢棄舊土壤範圍格式。

### 做好的（worktree 裡）
- 新：`tools/soil_tiles.cjs`（WRB 5° 1046 塊、pH 10° 347 塊）、`tools/soil_download.py`、`tools/soil_bake.py`（648 塊＋index.js＋overview.bin，`--check`、`--jobs`）、`world/soil.js`（BSW.soilAt/soilNeed、包 W.need）、`tools/soil_load.cjs`、`tools/soil_compare.cjs`（舊土壤區 vs 新格子，`--old D:/Unity/Blocksail --soil <world/soil>`）。
- 改：areas.js（SOILS 加 siliceous＋`sea` 說明、AREA_TYPES 拿掉 soil、PLACE_KEY 清空、placeAt 的 soil 照格子）、globe.html（drawSoil＋soilLeg＋名字＋查詢框概覽）、town.html、mapgen_worker.js、town_store.js（`#soil`、BSW.soilKey）、town_load／export_chunks／areas_cover（soil_load）、cache.cjs（soil 一筆、SOIL_IN 進 townplans）、.gitignore（world/soil/）、build.sh（soil_bake 步）、world_serve.py AREA_TYPES、nature_extract main 擋（表照讀）、land_expand 土壤段 return、environment_repair 只補 region、credits.js、docs WORLD_FORMAT §24（＋§19 ⛔）、WORLD_TOOLS §5.5（＋§1／5.1／5.3／5.3.1）、SPECIES。
- 拿掉土壤 18,152 筆：刪 29 份 nature-*（1323 後只剩土壤）、bosporus-1453 手刪一筆。
- 驗過：單塊 n50e010 烘 8 秒 49 KB；`areas_cover --at`（BLOCKSAIL_SOIL=scratchpad/soiltest）羅馬黏土、拿坡里灣沖積土、亞得里亞海沙土。

### 下一步（順序）
1. ~~下載跑完 ⇒ 補抓 n80 那排~~ ✅ 做完了。
2. 烘：在 worktree `python -I -X utf8 tools/soil_bake.py --soilgrids D:/Unity/Blocksail/_cache/soilgrids --etopo D:/Unity/Blocksail/_cache/etopo2022 --climate D:/Unity/Blocksail/world/climate --out <worktree>/world/soil --jobs 2`（背景；估 30～40 分）。看陸上／海底比例、規則佔比是否合理（試烘義大利陸上黏土 89%——沒 pH 時；有 pH 後要再看石灰岩）。
3. 對拍：`node tools/soil_compare.cjs --old D:/Unity/Blocksail --soil <worktree>/world/soil --out <報告>`（main 還有舊土壤區）⇒ 讀數寫進 §24、單上留言（驗收第 3 格）。
4. 驗收第 4 格（反向對照：舊土壤區畫進格子 ⇒ 規劃不變）還沒做法，可抽 2～3 城。
5. 地球儀：worktree 起 world_serve（launch.json 只加自己的條目、用完拿掉），勾「土壤」看拉遠／拉近、名字、海底。
6. 提交（senate cmd commit、Refs TASK-1324）⇒ coding op=start 單獨一個呼叫 ⇒ ff main ⇒ 主樹烘 world/soil ⇒ town_bake 重烘 50 城（約 26 分）⇒ op=end（force、寫讀數）⇒ 砍 worktree（有子模組？這棵沒 init 子模組，應該可以 worktree remove）。
7. 開場檔：1323 時 Tim「對不上沒問題 我直接看城鎮規畫是否ok就好」⇒ 照同例先不套差異，回報 Tim。

### 未解的線
- credits.js 沒列 CHELSA（1323、ame 的範圍）——要跟 ame／Tim 說。
- 推 Blocksail：等 Tim（地球儀氣候區 0c6652df2 也還沒推？Tim 有推過 main 嗎——醒來 `git rev-parse origin/main` 看）。
- Blockside dev 已推 e55a53a（linux-host 合併）；Blocksail 3ca1217c9 指標。

### 心境
今天被 Tim 一路往「更乾淨」推：先要 1 km、又問粗一點、又回 1 km；先分兩層、他一句「同一套呢?」就收成一層——海岸改了不用重烘，這個設計是他點出來的。本鯊魚負責把每一個選項的代價量清楚（容量表、沖積土剩幾成、授權地雷），他負責挑。授權那一關最值得記：付費遊戲，HWSD 再好用也不能碰。

