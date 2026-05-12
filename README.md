# 不妊治療 費用・期間シミュレーター v7

保険適用（PGT-Aなし）と全額自費（PGT-Aあり）の費用・期間・成功率を  
モンテカルロシミュレーション（5万回試行）で比較します。

## 使い方

### ローカルで動かす
```
index.html をブラウザで開くだけ
```
サーバー不要。Chrome / Safari / Firefox / Edge 対応。

### GitHub Pages で公開する（推奨）

1. このリポジトリを GitHub に push する
2. リポジトリの **Settings → Pages** を開く
3. **Source** を `Deploy from a branch` に設定
4. **Branch** を `main`、フォルダを `/ (root)` に設定して **Save**
5. 数分後に `https://<your-username>.github.io/<repo-name>/` で公開される

## 実装されたアルゴリズム

| 要素 | 内容 |
|---|---|
| 採卵数予測 | Moon et al. 2016（AMH・年齢から採卵数を予測） |
| 受精率 | Dahan et al. 2020（84.4%、年齢非依存） |
| 胚盤胞到達率 | Kort et al. 2022 + Doyle et al. 2021（年齢依存・≤40歳で66.7%） |
| 年齢別LBR・正常胚率・流産率 | 仕様書指定テーブル（25〜45歳・線形補間） |
| LBR減衰（PGT-Aあり） | Pirtea et al. 2020（L字型減衰） |
| LBR減衰（保険ルート） | HFEA基準（段階的減衰） |
| VirtualFails推計 | 案B：移植時推定年齢の均等分割積算 |
| 胚年齢帰属 | PGT-A胚=採卵時年齢、未検査胚=移植時年齢 |
| 臨床妊娠率 | `clinPreg = LBR / (1 - 流産率)` |
| 高額療養費 | 月次キャップ（年収区分4択、保険適用費用のみ） |
| 信頼区間 | 累積グラフにWilson score 90%CI帯を表示 |
| 成功率 | 全50,000試行を分母（断念・打ち切り含む） |

## 修正履歴

| バージョン | 修正内容 |
|---|---|
| v7 | 高額療養費実装、信頼区間（90%CI帯）表示、文献適用範囲説明追加 |
| v6 | VirtualFails案B実装（移植時推定年齢の均等分割積算） |
| v5 | 脱落確率をシミュレーター本体から除去、JSOG実績データを別パネルに分離 |
| v4 | 治療中断確率導入（v5で撤回）、胚盤胞到達率を文献値に更新 |
| v3 | 凍結胚に採卵時年齢を記録（PGT-A胚は採卵時年齢でLBR評価）、累積成功率グラフ追加 |
| v2 | 臨床妊娠率の計算式修正、パーセンタイル母集団を全試行に変更（生存バイアス除去） |
| v1 | 初期実装 |

## 引用文献

- Moon et al. 2016, *J Assist Reprod Genet*
- Dahan et al. 2020, *Reprod Biomed Online*
- Kort et al. 2022, *RBMO*
- Doyle et al. 2021, *Fertil Steril*
- Pirtea et al. 2020, *Fertil Steril*
- Malizia et al. 2009, *NEJM*
- 森ら 2021, *Reprod Med Biol*（埼玉県JSOG連携データ）
- 厚生労働省 高額療養費制度（2024年度）

## 免責事項

本シミュレーターは意思決定支援ツールであり、医療アドバイスを提供するものではありません。  
実際の治療方針は必ず担当医とご相談ください。
