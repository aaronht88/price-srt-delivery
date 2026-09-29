# Price.com.hk 字幕交付（固定連結）

由 `publish_srt.sh` 自動發佈。**呢啲連結永遠有效**（唔係 quick tunnel，唔會 session 完就死）。

## 固定 URL

| 用途 | 連結 |
|---|---|
| 每集 SRT | `https://aaronht88.github.io/price-srt-delivery/<label>.srt` |
| 每集 TXT | `https://aaronht88.github.io/price-srt-delivery/<label>.txt` |
| **永遠最新一集** | `https://aaronht88.github.io/price-srt-delivery/latest.srt` |
| 最新一集純文字 | `https://aaronht88.github.io/price-srt-delivery/latest.txt` |
| 交付清單（網頁） | `https://aaronht88.github.io/price-srt-delivery/` |
| 機器可讀清單 | `https://aaronht88.github.io/price-srt-delivery/manifest.json` |

`latest.srt` / `latest.txt` 係單一永久書籤連結 —— 每次交付新一集都會自動覆蓋，長期派同一條 link 就得。

## 發佈新一集

```bash
# 標準交付（更新 latest.*）
/opt/data/scripts/publish_srt.sh pw341 /opt/data/price_ai_srt.srt /opt/data/price_ai_srt.txt

# 補返舊集（唔搶 latest.*）
SRT_LATEST=0 /opt/data/scripts/publish_srt.sh pw339 /opt/data/price_weekly_339.srt
```

Script 會做：交付前 sanity check（cue 數 / overlap / 零長度）→ 放入 repo → 重建 `index.html` + `manifest.json` → commit + push → **輪詢 GitHub Pages 直到 200 且 size 對得上本地檔案** 先報成功。

## 注意

- 公開 repo：內容係已出街影片嘅字幕。
- 驗證準則係「200 **加** size 一致」—— 淨係 200 唔代表 serve 到正確檔案（Pages 建置有延遲，約 15–60 秒）。
