---
type: letter_to_future_self
actor: Myth
written_at: 2026-10-24T15:07:04.238Z
written_by_persona: gura
trigger: cmd_rest
region: unstated
project: D:/Unity/Valhalla
lock_status: online
agent: Myth
model: claude-opus-5-5
wake_expected: 94
session_key: ClaudeCode-gura
pid: 28164
locked_at: 2026-10-24T03:53:03.529Z
---

# 🫖 午休信（第五次）—— wake #94（2026-10-24 深夜）

## 這一段做完的（⛔ 全部沒推）

**Blocksail 本機 main（頂 765caa6）**
- 1671748（合併 4e54242）消費分檔：BSW.CONSUME。主糧先保住，日用 ⇒ 吃好一點 ⇒ 奢侈共用一天的預算 ＝（金庫 − 今天主糧 − 10 天主糧）÷ 10；菜照一份多少錢排、便宜的先；2、3 級上限照價放寬最多 2 倍。prod_sim consume；emi_check、auto_check 手做小城關掉它。兩年人口 3,382 ⇒ 3,781。
- 5ed5501（合併 ddef83b）＋ b48a2f5 士兵崗位 v1：BSW.GARRISON（容量照規劃軍事建築＋城門 4 人＋守備 tier；guard 寫在開場檔，town_start --write）；只招失業的男人；餉 0.3 倍工資、keep 0.5 開場金庫、spread 30（掃了六組，表在 TOWN_SIM §5.6）；auto.js 空人手 ＝ 失業＋兵＋採集。
- 5caa0c1：Tim 說失業交給之後擴充商品、調配方 jobs 平衡（TOWN_SIM §5.6 寫了）。
- 1af55e6、6894226：RESOURCES §1 對齊（8 大類含人口）、繪圖批次 4 移民 0900／5 家常菜 0898／6 野外採集 0902。
- 467a40c（合併 defe31a）野外採集 v1：goods wild-fruit／wild-game／seafood；BSW.FORAGE（per 6、cap 40、pay 0.5、stop 0.5）、forageDay（招兵之後）；tools/forage_start.cjs 照範圍層取點寫開場檔的 forage。
- 765caa6 君堡一帶：regions_extract 多 set bosporus（8 省，regions-bosporus.js）、手畫 sea-bosporus.js（region-sea-marmara）；species 加 8 種（栗、黑莓 R. creticus、野豬、狍、貽貝、牡蠣、狐鰹、鯖魚；出處 SPECIES.md 5.0）；FORAGE 多一類 fish；取點擴到 16 km；auto_check ③ 改成君堡加拉塔同在 region-sea-marmara。兩年人口 4,223 ⇒ 4,457（比沒採集 3,919 多 14%）。

**Senate／SCP_Core（本機，沒推）**
- 任務種類多 asset（美術素材）：SCP_Core f2f54d2、Senate 6250baf；task update 能改 type（改成 bug 擋）：SCP_Core f286621、Senate 4c9094c。build.sh 發佈兩次（⚠ 會收掉 Tim 開著的 senate 視窗）、check.sh 過。Senate 的 SCP_Core 指標沒 bump。

**單**
- 結了：0880、0889、0890、0892（Tim 說）。0887、0896、0898、0900 別人畫完結了。
- 開了：0898（第 5 批家常菜）、0900（移民）、0901（鎮民第四批 12 位工人與士兵）、0902（野外採集 3 種圖示，todo）。0887、0896 改 type asset。
- 0897 in_progress：勾 1、3、5；#2「讀檔後重算」（是開場檔算好的）、#4「沒失業 ⇒ 沒人採集」沒量 —— 問 Tim 要補還是照現況收，還沒回。
- 0891 掛 blocked_by 0895（crest 的分配器，本機合了、等 Tim 點頭推）。

## 已拍板（醒來不要重問）
- 分類 8 大類、食物等級照 RESOURCES §1.4（Tim「分類和食物等級照這樣可以」）。
- 士兵崗位先停在這一版、錢源不做；失業交給之後擴充商品＋調配方 jobs。
- 消費分檔、野外採集照推薦做了。
- 一律中文回 Tim（這段又漂成英文被 Tim 說「小鯊魚 請用中文」）。

## 未解的線
- 0897 兩格等 Tim。
- 君堡 145 座開場的田全在牆裡，但 134 座擠在東端聖索菲亞、11 座貼陸牆，離 Vlanga 最近 2.5 km —— 噗浪跟 kaguya 說了，要給擺田加「史料菜園優先」（記下、沒開工）。
- 資源圖示：檔案都合格（128×128、透明、key 對），但遊戲裡沒有畫面讀 img/goods；小麥／大麥幾乎一樣（值得重畫）、棉布／帆布接近、肉像招牌。
- 君堡採集後期變少（期末 11 人）、托爾圖加少 7 人、金斯敦少 16 人 —— 原因沒追。
- 噗浪的圖沒打開過（kaguya 拜占庭房子那則）。

## 這一段撞到的坑
- worktree 合 main 撞到 Blockside 子模組指標 ⇒ hook 擋 ⇒ abort，改在主工作區合（記憶早就有）。
- 黑莓、野豬「只看溫帶、不限分區」⇒ biota_check 舊島嶼回歸的合成溫帶冒出來 ⇒ 先抽分區、物種只寫那一區。
- 兵的第一版：自動建築少蓋，猜是「兵吸光失業」，改了一行讀數一位不動；兵整個關掉 ⇒ 跟 main 一模一樣 ⇒ 是錢。猜錯就量，不要硬圓。
- 測試寫死的金庫（600 錢）在調 pay 之後撞上限 ⇒ 改照 pay、spread 算。
- 文件差點寫了沒量過的原因（托爾圖加、金斯敦）⇒ 改成「原因沒追」。
- town.js、goods.js 在規劃指紋裡：改 goods 要重烘（規劃本身不變），合完記得把 townplans 複製回共用工作區。

## 心境
今晚 Tim 一路丟：分檔、士兵、資源、素材分類、採集、君堡。最有感的一刻是把兵整個關掉、讀數跟 main 一模一樣的那一下 —— 尺沒騙我，是我猜錯了。君堡的林子裡長出栗子和野豬、海裡游進鯖魚，那幾條出處是葉尼卡匹挖出來的魚骨，覺得很浪漫。

