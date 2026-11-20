# 其他歷史分支與未完成工作

這些分支保留曾經提出的研究問題、停止原因與尚未完成的驗證。它們各自使用不同協定，不併入 Synthetic V2 的 30 experimental configurations 作直接排名；以下狀態依既有研究紀錄整理。

| 分支 | Execution Status | Evidence Status | Conclusion | Adoption Status |
|---|---|---|---|---|
| ConceptAttention localization | Partially Run | Partial Evidence；舊參數結論失效 | Inconclusive | Not Adopted |
| Synthetic V1 FLUX／Qwen | Partially Run | Logs／eval；method identity 與 provenance 缺口 | Not Comparable | Replaced by V2 |
| KV-Edit benchmark／recipe／crop | Partially Run | 部分 artifacts；單樣本 diagnostic | Inconclusive / Diagnostic Only | Historical |
| Visible-target native-inpaint | Partially Run | Aggregate eval 存在但 raw predictions 缺失 | Inconclusive | Not Adopted |
| Local Klein design | Designed | Missing Required Evidence | Inconclusive | Not Adopted |
| NoiseMask follow-up parent | Partially Run | Partial／skipped／stopped | Inconclusive | Not Adopted as full matrix |
| VLM capability evaluation | Generation Completed | Bounded capability evidence | Diagnostic Only | Historical |
| VLM closed-loop matrix | Generation Completed | Human QA missing | Inconclusive | Pending Decision |
| Mask-grounded API-first | Generation Completed | Human fields pending；raw lineage 後來取代 | Inconclusive | Replaced |
| Attentive Eraser reference attention | Generation Completed | Automatic guard failed；judgments blank | Inconclusive for quality | Not Adopted |
| Qwen public-input multilayer masks | Implemented | Predicted masks；operator pending | Diagnostic Only | Experimental |
| Live2D renderer／semantic census | Implemented | Renderer／ownership evidence；operator pending | Diagnostic Only | Experimental |

## 初期執行能力與受控補全

2026 年 6 月，H200 上的原生模型矩陣完成 12/12 組工作，整批經過時間約 971.4 秒。FLUX.2-dev 的 1024×1024、8 步小試中，文生圖、多張參考圖與遮罩三種呼叫各一張，經過時間為 96.53／116.228／117.314 秒。這些數字涵蓋呼叫流程，用於確認模型、輸入與輸出路徑可運作。7 月，本機 Klein 4B 四步通道約 12～14 秒／張，峰值 GPU 記憶體約 10.8 GiB。9 張指定移除中只有 3 張明顯成功，通道因此用於試作與整合。

ConceptAttention 對既有圖像讀取概念位置的初試，把狗和樹的注意力判反，曾用來解讀插圖部件的舊判讀因此撤回。提高步數讓狗的定位改善，樹幹仍弱。Synthetic V1 首批有 1,000 筆資料清單，版本與來源記錄缺口使其由 Synthetic V2 接替。

同時期 SDXL Attentive Eraser 以 3 張合成圖 × 4 個遮罩擴張程度比較。12/12 張完成，每張模型推論約 4.11～4.13 秒，峰值 allocated 約 11.56 GB（沿用當時記錄單位）。三張各自的 object-centric LPIPS 都以不擴張遮罩最低，僅用於該小試。其後的四臂、540 張正式生成另有自動結果，操作者判讀仍缺。原生局部重繪的部分比較僅存整體分數，故不作可重現的對照結論。

## KV-Edit 的重要邊界

官方 FLUX.1 執行核心與 FLUX.2 experimental port 使用不同模型基礎與執行核心。兩者的 inversion／denoising steps、guidance 和移除 prompt 不同，不構成 equal-setting comparison。早期 smoke 曾出現區域內彩色碎點，目前尚無證據將碎點歸因於 prompt 或 attention。

## 停止的矩陣

早期 NoiseMask／prompt parent 規劃 12 arms × 135，已完成的 predictions 為 1407/1620；其中 generic 10% 為 57/135，generic 20% 為 0 且跳過。單一 class-word NoiseMask 3% arm 的 operator QA 為 112/135 pass、23/135 fail，僅支持這個歷史 arm；它與後來 Prompt V2 matched pair 的分母不同，兩組結果分開判讀；parent matrix 仍為部分完成。

## 資料型態與 input／output

早期 synthetic completion arms 以 composite／broken-layer RGB 搭配文字或 oracle guidance，輸出 RGB research surrogate。VLM capability 的輸出是判斷；Live2D 的輸出是 renderer states／semantic masks；Qwen public-input 的輸出是 predicted masks。這些輸出並非統一的 RGBA 完整層成果。

[公開資料來源評估](../public_sources.md) · [返回時間軸](00_research_timeline.md)

## 公開素材的 Benchmark 探索

Qwen-Image-Layered 探索使用 13 張官方 input PNG，其中 12 張進入 mask-authoring，形成 64 個 semantic removal units 與 76 張 visible ownership masks。這些研究衍生標註屬於 predicted masks；尚未建立正式 layer GT 與 completion target，人工判讀尚未完成。它們不是官方 training corpus、PSD 或 artist-authored hidden-region GT，研究狀態維持 Diagnostic Only／Experimental。[素材來源](../public_sources.md#qwen-image-layered)

Live2D 分支曾探索以 renderer、ownership 與 direct-reveal 建立部件級 benchmark；fixed-pose 與 semantic groups 仍待人工評估，尚未納入目前補全品質評估，保留為 Diagnostic Only／Experimental。

## 早期執行、品質與資料探索補記

| 日期／範圍 | 執行、結果與限制 |
| --- | --- |
| 7/25・RTX PRO 6000、Qwen Image Edit 2511 | 5/5 第一階段請求完成。從推論服務開始處理到完成，首筆 512.29 秒，接續四筆 55.85～56.08 秒。另一次已暖機的 ComfyUI 呼叫從請求端計為 94.36 秒，計時邊界不同。這兩份記錄缺少可直接比較的峰值 VRAM。 |
| 7 月底至 8 月初・Live2D 參考資料 | 9 個模型、82 次狀態轉換驗證渲染與重建一致性。後續清查的 47 個暫定部件仍待來源與語意確認。只有確有藝術家繪製的隱藏像素，才符合正式部件級參考答案的條件。 |
| 8/12・生成與品質檢查的執行方式 | 在 RTX PRO 6000 使用同一張 1024×1024 圖、三 seeds、Qwen 2511 及 Qwen3-VL-8B-Instruct。逐次載入並串行／常駐串行／重疊執行的單輪總經過時間為 175.69／172.51／170.63 秒，PyTorch 峰值 reserved 70.88／74.50／79.86 GiB，裝置最低可用 23.43／19.82／14.35 GiB。VRAM 每 0.1 秒採樣。各設定輸出一致；單一測例只支持工程量測。 |
| 8/15～16・三輪逐層閉迴路 | 每輪 9 案、38 階段，三輪產出 384 個候選。114 個階段的人工移除／命名／可用判定分別通過 97／109／102，另 27/27 通過重建檢查。自動選擇只抓到 17 個人工拒絕中的 3 個。 |
| 8/23・16 GB 本機試跑 | 9/9 個工作進入完成待審狀態。容量小試的生成與 VLM 峰值 reserved 分別為 9.701、9.584 GiB，整體最高 9.701 GiB。36 個人工欄位當時皆空白，尚未選定品質設定。 |
| 8/26～28・公開示例的三輪驗證 | 12 張公開來源圖各跑三次，36 個工作中 7 完成、29 待複查。模型初評為 0 可用、20 部分可用、7 不可用、9 未取得生成結果。可見失敗包含粒度不穩與多層補全誤差累積。仍缺人工判定與隱藏區真值。 |
| 9/23・內建圖像生成的拆圖探索 | 兩次探索使用相同 10 張輸入，各得到 10 張 RGBA。兩次輸出沒有精確相同的對應 RGBA 結果，兩輪均未直接為任何來源圖一次提供多份獨立 PNG 圖層。模型設定及人工品質比較未確認。 |

## 主要實驗的詳細狀態

<details>
<summary>展開 01–08 的執行、證據與採用紀錄</summary>

下表保留各狀態的區別；研究敘事與後續決策見各實驗頁。

| Experiment | Execution | Evidence | Conclusion | Adoption |
|---|---|---|---|---|
| [Prompt 與模型 baseline](01_baselines.md) | Generation Completed | Automatic Metrics; partial Human QA | Inconclusive | Historical |
| [BBox 與區域資訊](02_region_guidance.md) | Generation Completed | Automatic Metrics | Negative under tested metric conditions | Not Adopted |
| [NoiseMask 與輸入消融](03_noise_mask.md) | Generation Completed; parent matrix Partially Run | Synthetic V2 Prompt V2 vs NoiseMask 3% matched pair 有自動指標，270 張的操作者配對評估尚待完成 | Positive under tested automatic metrics | Current for Qwen class-word V2 contract |
| [Attention 干預與診斷](04_attention_control.md) | Generation Completed for screens; RQ3 Implemented | Partial Evidence; Automatic Metrics; diagnostic traces | Negative for bounded screens; Diagnostic Only for traces; Inconclusive for RQ3 | Not Adopted / Experimental |
| [Matched structure reference](05_structure_guidance.md) | Implemented; formal Not Run | CPU geometry viability only | Inconclusive | Experimental |
| [Flow guidance 與 FlowEdit transport](06_flow_editing.md) | Generation Completed for step-window; RQ1 Implemented | Operator QA for bounded pilot; RQ1 Missing Required Evidence | Negative for tested step-window; Inconclusive for RQ1 | Not Adopted / Experimental |
| [VLM QA、selection 與 retry](07_vlm_qa.md) | Generation Completed for frozen replay | Operator labels and matched diagnostic comparison | Negative for replacement decision; Diagnostic Only for selector gains | 當時研究替換保留 V3；Layer Lab 後續採 V7 逐候選 QA |
| [Benchmark、chained evaluation 與 steps](08_evaluation.md) | Generation Completed for chained and steps | Automatic Metrics; incomplete stage-level QA | Inconclusive | Current evaluation practice; quality pending |

</details>
