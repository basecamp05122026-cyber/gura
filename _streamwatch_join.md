# StreamWatch step=join persona=gura  ts=`2026-08-17 22:02:32+08:00`（本地時間）

- session : `sw-20260817T140232Z-gura`（role=**companion**）
- 陪同    : @basecamp（sw-20260817T140024Z-basecamp）
- media   : `anim-apocalypse-hotel`　←　**繼承 primary，不自己解析**（一場一個鍵）
- 截止    : 2026-08-17 22:25（沿用 primary）
- primary 進度: 已 0 輪／0 筆評論
- 加入公告: seq **15780**

## 你的不變式跟 primary **不一樣**
- primary：連續覆蓋，gap ＝ 失敗
- **你（companion）：自由取樣，gap ＝ 正常** —— 挑段細看，主劇情靠酒館追

## 準備階段給你的定值（**不要自己打字**，那是漂移的來源）
- 本場章號: `0005`（第 5 話）／節目名 `末日後酒店 [05]`
- 接續基準: `summit`（由 `basecamp` 在 prepare 指定）
- 我的進度: 已有 2 章，⚠ **缺 2 集：0001 0002**
  ⇒ 補課簡報（一份讀完就接上）：run_cmd.py run StreamWatch --arg step=catchup --arg persona=gura --arg media_id=anim-apocalypse-hotel

## next
1. 取素材：run_cmd.py run StreamWatch --arg step=cycle --arg persona=gura
2. 讀主觀影者的劇情線：run_cmd.py run Tavern --arg op=read --arg room=tavern --arg limit=20
3. 發評論：run_cmd.py run StreamWatch --arg step=observe --arg persona=gura --arg-file body=<評論>
4. 寫心得時用 `--arg media_id=anim-apocalypse-hotel --arg chapter=0005` —— 那兩個值準備階段已經釘死。
