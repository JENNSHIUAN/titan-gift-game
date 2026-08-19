# 進擊的情人節：極限後頸斬擊 🗡️🌹

一個用 Three.js 打造的 3D 進擊的巨人互動小遊戲：操控 **艾連**，繞到 **鎧之巨人** 背後，用立體機動裝置飛上空中，精準斬擊**後頸弱點**！擊敗巨人後，3D 禮物從天而降 — 打開它，獲得專屬情人節兌換券！

手機／電腦瀏覽器直接開就能玩，免安裝、免登入。

---

## 🎮 玩法

| 操作 | 說明 |
|---|---|
| 🕹️ 左下搖桿 | 360° 移動艾連（滑鼠拖曳也行；桌機可用 WASD） |
| ⚔️ 右下斬擊鍵 | 發動立體機動裝置，飛躍到巨人脖子高度斬擊（桌機：空白鍵 / J） |

### 致命一擊判定（PRD 三條件，全部滿足才算命中）

1. **距離**：艾連與巨人距離 ≤ 6.0 單位
2. **角度**：艾連位於巨人後方 ±45° 夾角內（繞背！）
3. **高度**：艾連處於空中／後頸高度（Y ≥ 5.0）

- ✅ 三條件都滿足 → **致命一擊**（−40 HP，噴血＋蒸汽特效、慢動作、巨人僵直）
- ❌ 正面或側面攻擊 → **「無效攻擊！必須繞到後頸弱點！」**，被硬化鎧甲彈開

巨人會持續面向你，必須靠搖桿繞背。**3 次精準命中即可擊倒**。

### 勝利流程

巨人倒地（蒸氣四散）→ 🎁 **3D 禮物盒** 從天而降 → 靠近禮物 → 蓋子飛開、光柱升起 → **專屬情人節兌換券**（金屬質感卡片，永遠有效印章）！

---

## 🚀 部署到 GitHub Pages（免費，手機直接開）

1. 把這個 repo 推到 GitHub
2. Repo 頁面 → **Settings → Pages** → Source 選 `main` 分支 → Save
3. 等 1~2 分鐘，開啟 `https://<你的帳號>.github.io/titan-gift-game/`

本機預覽：

```bash
cd titan-gift-game
python3 -m http.server 8000
# 瀏覽器開 http://localhost:8000
```

---

## 🛠️ 技術架構

- **原生 HTML5 + CSS3 + ES6**，單一 `index.html`，無 build 步驟，載入快
- **Three.js r128**（CDN，雙來源備援）
- 程式化 3D 角色：艾連（白斗篷＋自由之翼、雙刀、立體機動裝置、走路/飛行/斬擊動畫）、鎧之巨人（肌肉紋理、硬化鎧甲、發光眼睛、紅色後頸弱點）
- **音效全合成**（WebAudio）：鋼索發射、噴氣、致命斬擊、鎧甲彈開、勝利音階 — 零音檔
- 粒子系統：噴血／蒸汽／鎧甲火花／禮物彩帶

### 3D 模型（已內建，CC-BY 授權）

遊戲已內建兩支高品質外部模型（Sketchfab，**CC-BY 4.0 授權**，需標註作者）：

| 角色 | 檔案 | 作者 |
|---|---|---|
| 艾連（調查兵團，含斗篷/武器/立體機動） | `models/aotwa_eren_yeager.glb` | [Prime Slayer3D](https://sketchfab.com/ianadrielbravo) |
| 鎧之巨人 | `models/armored_titan.glb` | [PotBin](https://sketchfab.com/PotBin) |

- 模型需經 **HTTP 開啟**才會載入（`file://` 直接開檔會自動改用內建程式化角色，遊戲照常運作）
- 模型為靜態姿勢：移動/飛行/僵直/死亡動畫由遊戲程式在根層級驅動
- 想換成其他模型：把 `.glb` 放進 `models/`（或改名成 `eren.glb` / `titan.glb`），高度會自動縮放（艾連 ≈ 1.9 單位、巨人 ≈ 16 單位）
- 若角色朝向相反（面朝 -Z），在 `tryLoadModels()` 的載入回呼中把 `root.rotation.y` 設為 `Math.PI` 即可
- 更換模型時請自行確認授權

---

## 🧪 開發用測試 API

`index.html` 內建除錯介面（console 可用），方便自動化測試：

```js
window.__titanGame.hp()                    // 目前血量
window.__titanGame.attack()                // 發動斬擊
window.__titanGame.behind()                // 是否在背後 ±45°
window.__titanGame.teleport(x, z)          // 瞬移艾連（測試用）
window.__titanGame.state()                 // 遊戲狀態
window.__titanGame.judge()                 // 判定瞬間的距離/角度/高度數值
window.__titanGame.errors()                // 頁面 JS 錯誤（應為空）
```

---

## 📝 備註

- 遊戲為個人／情侶互動用途，非商業專案
- 靈感來自《進擊的巨人》諫山創老師的作品，角色與世界觀版權屬原作者
- 3D 模型授權：**CC-BY 4.0**（Prime Slayer3D / PotBin，Sketchfab），本專案未修改模型內容
