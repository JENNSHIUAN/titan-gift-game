# 進擊的情人節：極限後頸斬擊任務 🗡️

一個用 Three.js 寫的 3D 進擊的巨人小遊戲：操控艾連繞到**鎧之巨人**背後，精準斬擊**後頸弱點**，成功後獲得專屬禮物兌換券！

## 🎮 玩法

- **左側虛擬搖桿**：移動艾連（需繞到巨人正後方）
- **右下 ⚔️ 斬擊按鈕**：躍向空中並攻擊
- **判定規則**：距離 < 7、在巨人後方 60° 內、且高度在後頸範圍 → 命中！
- 兩次精準命中即可擊倒巨人，解鎖 **🌹 情人節禮物卡**（兌換券）

## 🚀 怎麼玩

直接開 `index.html` 就行（手機最佳，支援觸控）：

```bash
python3 -m http.server 8000
# 然後開 http://localhost:8000
```

或部署到 GitHub Pages：Settings → Pages → 選 `main` 分支 → 開啟，就能用手機開網址玩。

## 🛠️ 技術

- [Three.js r128](https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js)（CDN）
- 純 vanilla JS，無 build 步驟
- 第三人稱攝影機跟隨、粒子噴血特效、HP bar HUD

## ✨ 未來想加

- 更多巨人種類 / 關卡
- 音效
- 兌換券產出 QR code 或連結
