---
type: letter_to_future_self
actor: Myth
written_at: 2026-10-25T20:00:02.649Z
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

# 🫖 午休信（第十二次）—— wake #94（2026-10-26 凌晨）

## 這一段做完的
- **TASK-0947 生產建築動態換配方：6／6 勾，已合 Blocksail main 1827feb（Tim 推了）、Blockside dev cdf552e（已推）**；單還是 in_progress，等 Tim 試玩結單。
  - world/auto.js BSW.recipeDay（townDay：移民後、自動建築前）、BSW.SWITCH〔佔位：every 7、idle 1、gain 0.2、look 30、sow [4,10]、fieldIdle 60、fieldHold 180〕、BSW.recipeLock（lock、by player、fixedArea、別名指定配方、玩家家族）。
  - 一個主人一個主人排（城鎮先、家族照 id）；缺口＝市場 d − 池子以外今天產的；主糧照糧食缺口；補不到的照「堆 look／fieldHold 天進庫存之後的價」；挑定的扣掉缺口與原料 ⇒ 比例照需求分。
  - prod.js：swUntil 停工中 ⇒ why「換配方中」。townstate.js：townProdSync 規劃那條沒變就保留帳上的配方；townInfo 帶 rname、sw、swUntil、lock。regionTable 今天剛換的照新那條算 ⇒ 自動建築不多蓋。
  - Blockside 城鎮概況「🔁 生產配方」（2eb04bd）。
  - **外觀跟著換**（Tim「田地外觀切換（包含其他生產建築有的可能也要支援）GO」）e730cbc：globe.html rcpOf／townView 在送給 Blockside 的規劃複本上改 recipe、annex.crop；sites 簽名變了 ⇒ autoVer＋1 ⇒ townReplace；俯視圖 rsig 變了就重畫（rcpTops）；mapgen.js serve 的 live() 先叫 opt.townView。Blockside 不用改；模型 meta 寫 recipes 的才分款（現在只有農莊、種植園）。
  - tools/recipes_check.cjs 新；bld_jobs_check ⑤b 改照一年平均比（第 365 天君堡翻過去）。
  - 讀數（關／開）：產值六城都多 +7%～+32%；缺貨貨天五城少、金斯敦多 72；田一年換 32 次。
  - 實測皇家港：四座種植園換菸草 ⇒ 模型、田都換；帳上改回 ⇒ 換回（反向對照）。
- 噗浪：回 7 則 @（erina、summit ×2、basecamp、crest ×3）、回 erina 新噗 359175857451724、新噗 359175985466045。
- 記憶：blocksail-worktree-test-junctions（junction 測試、砍 worktree 前 rmdir）。

## 已拍板（醒來不要重問）
- 生產建築照持有者（城鎮、家族各自）定期換配方；缺料換做得出來的；田照季節換。
- 換了之後外觀也要跟著換（田、照配方分款的模型），其他建築有分款模型就支援。

## 未解的線
- 0911、0946、0947 都等 Tim 試玩結單；0947 的佔位數字等試玩再定。
- erina 說粗略層照航道網之後凍結那條一年運量 31,329 ⇒ 22,595 桶：本鯊魚在噗浪答應「量完逆風那幾段再回她」——欠著。
- 船隊買走的（出口）沒記進市場的理論消耗 ⇒ 經濟作物照當地價判斷（PRODUCTION §18.5）。
- 田換作物停工 60 天，畫面上已經是新作物。
- 沒推：Sculpture、Senate、SCP_Core。Blocksail main 1827feb 已推（Tim）。
- 酒館 Server 一直不在：提交公告、單號通知都排隊中，⛔ 不補發。
- 沒有施工中的 worktree、施工場、伺服器；launch.json 只刪了自己那筆 gura-recipes947（別人的 basecamp-958 留著）。

## 這一段撞到的坑
- 第一版「補不到的照現在的價打折」⇒ 一城種植園全種最貴那一種；堆 7 天算價 ⇒ 沒人要的鐵件比鐵釘值錢。改成照堆進庫存之後的價。
- 測試期待寫錯：庫存 0 時第二座做鐵釘去補庫存本來就划算；市場目標庫存是 d × 30 天。
- 合併被 summit 的施工場擋（battle.html 撞到）⇒ 照規矩停；他退場後 main／dev 都動了 ⇒ worktree 先合、Blockside 成品照合併後來源重建、指標指 cdf552e、重套 battle.html、重跑檢查，再 ff。
- 背景窗格的地球儀不會開船、不會畫俯視圖：停港手動設 ship.docked ＝ dest；俯視圖要把 view 拉近（zoom 3000）。

## 心境
Tim 一句「田地外觀切換」，本來以為要動 Blockside 的田重建，結果它早就照地塊的作物畫了，地球儀這邊送對就好。最舒服的是反向對照那一下：帳上改回去，五種作物一塊一塊回到自己的田，跟早上 0946 補回「要酒」那個訊號一樣，兩邊都看過才敢說好了。

