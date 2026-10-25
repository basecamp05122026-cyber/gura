---
type: letter_to_future_self
actor: Myth
written_at: 2026-10-25T11:10:02.350Z
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

# 🫖 午休信（第十次）—— wake #94（2026-10-25 傍晚）

## 這一段做完的
- **TASK-0929 結單**（Tim「929 ok」）。
- **TASK-0911 第二段**（Tim「繼續優化船隊系統吧 讓玩家所在海域會真實模擬船隊運行」）：驗收 14／16 勾。
  - Blocksail main **2d333ac**（本機，**沒推**；中間 f06ca6d）：
    - 營運路線 `fleetRoute`：環＝母港 → 沿途 → 本區集散地 →（長途：別區集散地）→ 母港；沿途港一座一座插；到期（3 輪且 30 天、或 90 天）回母港照貿易報表重看（多 10% 或在虧才換；在虧又排不出 ⇒ idle 7 天）；rlog。
    - 精細海區 `FINE.zones`（加勒比、馬爾馬拉方框〔佔位〕）、`fineFocus` 照玩家船、出去多走 0.5°；照小時出港（5～9 點）到港、港裡 12～36 h。
    - 凍結 `coarseDay`：環上位置 ph、虛擬貿易額度（每段排的那份 × 24 ÷ 一輪小時）、海盜每天照「真的穿過一次」擲、劫那天的份（期望一樣）。
    - 交接 fleetToFine／fleetToCoarse；**townDay 一開頭先跑完今天的小時**（出入港買賣要在換日生產之前；fineRunTo 先 fineSync）。
    - 船隊規模：sloop 40／brig 150／fluyt 300（hull falcon／phoenix／cosecha）、船況、回母港修船（錢給船匠）、每 30 天造／賣。
    - 地球儀 `trafficFor`：回 Blockside 8 km 內在海上的＋附近停港的（泊位 hdg）。
    - fleet_check ⑥⑦⑧③ 全過；TRADE_SIM §2.8。
  - Blockside dev **8dcdca2 已推**：`58_traffic.js` 往來的船（每 2 秒 trafficNeed、6 km 內才生、背景預算分段建、上限 MAX_SHIPS 扣我艦、sh.npc 照航點開不開火、清單沒了就 splice 出 SHIPS 並放網格）；順手修 54_helm 讓友船那列 c.od 沒有就爆。
- 噗浪：回 summit ×2、crest ×3、erina ×1；新噗 359171909639442（https://www.plurk.com/p/3jbdapge8i）。

## 已拍板（醒來不要重問）
- 航線：一律從母港出發、一定經過本區集散地、可長途到別區集散地（Tim 兩張圖：環）；航線一開始排好，幾個月或幾輪才照報表調整。
- 非精細區凍結：虛擬貿易額度、照樣造船修船、海盜照機率。
- 航海模式用**真的船**（不開火、照航點開、停用回收），之後 0940 直接接；半無縫載入、上限參考海戰設定、不卡主執行緒。

## 未解的線
- 0911 剩 2 格：城鎮模式看停港的船（只在航海模式泊位旁實測過）、地球儀每格幀數（背景窗格量的 6 支 13.6～16.7 vs 0 支 3.2 ms 只當參考）⇒ Tim 有畫面時看一眼。
- 沒推：Blocksail main（2d333ac 以前一長串，含別人的）、Sculpture、Senate、SCP_Core。
- 0911 之外還在等：0914。
- 沒有施工中的 worktree、施工場、伺服器；launch.json 只刪了我自己那筆（gura-fleet2、gura-traffic）。

## 這一段撞到的坑
- 照小時跑 vs 整天跳對不上兩次：出入港在市場買賣 ⇒ 必須在換日生產之前；fineRunTo 前要先 fineSync。
- 兩層的尺：凍結海盜一開始打了兩次折（0.09% vs 0.93%）；修船次數也一樣（被劫扣船況要乘 24÷一輪小時）。
- 背景窗格 `G.live(0.5)` 在 SIMT 不走時一次跑 200 格，迴圈掛住分頁幾分鐘 ⇒ 用 live(0.05)＋牆鐘上限（記憶已補）。
- iframe 裡加 capture listener 攔不住地球儀回覆 ⇒ 暫時 cine.site = null。
- Blockside build --code 要求成品照 HEAD 建 ⇒ 先 git checkout -- index.html。
- 測試船擺到淺水邊被「避開淺水」接管 —— 是正確行為，不是 bug。

## 心境
今天從 Tim 一句「真實模擬」一路接到他畫的那兩個紅圈，最後看到第一艘電腦的船在金斯敦港外自己張帆開走 —— 船頭跟航點差 0°。最刺的是兩把尺打了兩次折，最爽的是兩層三年對上。船在海上了，下一步是讓海盜盯上玩家。

