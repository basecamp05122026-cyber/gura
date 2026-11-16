---
type: letter_to_future_self
actor: Myth
written_at: 2026-11-16T07:34:27.126Z
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

## 午休信 —— TASK-1291 第五輪做完、合進 main（2026-11-16 下午）

### 施工中
- 沒有。施工場 coding-20261116T071146Z-gura 已收（force，理由寫了讀數）；worktree bs1291s、bk1291s 都 remove 了（junction 先 rmdir、共用 _cache 16 項、townmesh 458 項都還在）；預覽伺服器停了；launch.json 自己的 gura-seacanal、gura-seacanal-ctrl 都拿掉了。

### 已落地
- Blockside dev 推到 **bb9cb3b**（遠端讀回一致）：2d4ef47 海面遮罩（堤後不畫海 r、石堤旁不碎浪 b、石堤旁 4 m 認水 a、堤身盡頭平頭＝TASK-1304）、fede11a 拱照兩道河堤撐開、bb9cb3b 合 dev（0e5eddf 威尼斯小船）。
- Blocksail 共用 main ff 到 **1a4ba074**（⛔ 沒推，等 Tim）：df7acfea 運河全當海（chunks.js）、34a19477 第五輪路橋河口、1a4ba074 合 main（b24a8956）＋ Blockside 指標＋ battle.html。
  - ⚠ 推之前還是要先把 origin/main 多的那筆（55d25865）用 --no-commit 合進來。
- 規劃 50 份已抄回共用樹 world/townplans；共用樹 town_bake --check ✓、check_core 四條 ✓、城市報表 ✓、town_check 互疊 0。
- TASK-1304 認領了、留言「球在 Tim：進遊戲看那一道堤」，狀態 in_progress（commit 用 Refs，沒 Fixes）。

### 等 Tim
- 問了「要先進遊戲看過再決定推 Blocksail main 嗎？」還沒答。
- 之前欠的推送：Blocksail a41d42b2/f8534ba2（現在都在 main 裡）、Sculpture c01f68d3/72933090、Senate d77cb3c。

### 已拍板（醒來不要重問）
- Tim 這一輪五件：①其他運河都照大運河套海面、堤後不穿透 ②河堤旁的路取消（河堤本身是路）③路穿運河、橋交叉、橋太密合併 ④橋沒有橋洞 ⑤不跨河的橋 ⇒ 都做了。TASK-1304 照他說的「河堤往外 clip 水面」修。
- 兩個 server 只留一個（他問過），對照組 server 用完就關。

### 查回來很貴的
- 窄運河鋸齒的真兇：中畫質「淺水變透明」（01_gl.js dep → a 最透 0.4）和岸邊亮線都照 8 m 高度貼圖算水深 ⇒ 6 m rio 被當淺灘。不是地形網格、也不是 discard。用 seaDbg({edge:0}) 對照才分出來。
- 藏著的窗格：手動 docked 進城時船停在離城 6 km 的錨地，地形／遮罩窗跟著船 ⇒ 改 __game.ships()[0].px/pz 搬到目標附近等 30 s（已寫進記憶 blocksail-town-view-unhide）。
- Worker 裡的遮罩：攔 w.Worker.prototype.postMessage 讀送進去的資料與回傳的 T（bundle 是一個閉包，拿不到全域變數）。
- 刪路要照「刪完重烘之後」的規劃再挑一次；河口切開（town_sample.js 改了）之後 v-corte-del-sabion 斷了 ⇒ 拿回 v-raccordo-42（第 4 份）、v-salizada-del-forno（第 5 份）。town_roads_check 判接上比城市報表鬆，最後以報表為準。
- 讀數：路 2,607→2,331；橋 439→363（交叉 0、太密 0、不跨河 5、跨水沒橋 3，剩的都是割點）；河堤封河口 29→10（剩的多是同一運河兩段的接頭）；住宅 7,379 棟容量 130,001；49 份規劃跟 main 逐字相同。

### 未做
- 一年模擬沒跑；撐開的拱沒從側面看過；Tim 截圖那一道破洞的堤沒找到是哪一道；chunk_bake 沒烘（打包產物）。
- 預設模式的刪細巷現在把河堤算進路網，會多挑 444 條 —— 沒做，沒人要求。
- 伐木場一年多蓋 ~830 座還沒查。

### 心境
這一輪 Tim 一邊看一邊丟了五件，本鯊魚每件都先開對照組再動手。最得意的是鋸齒那一題：三次猜錯（discard、4 m 通道、拱），最後用 edge:0 一刀切開才知道是「透明」不是「沒有」。量具全綠但人看到的是沙，一樣算沒做完。

