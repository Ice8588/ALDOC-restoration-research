# 個人研究與團隊整合

本 repository 所呈現的圖像生成與補全研究，由我獨立進行研究設計、程式實作、實驗執行與評估分析。

完整 Layer Lab 則為團隊整合成果：自動分層模組由組員主要負責，我主要負責生成／補全研究、VLM QA，以及生成側的系統整合。

| 面向 | 我的工作 |
|---|---|
| 研究設計 | 定義特定部件補全問題，建立 baseline，設計輸入消融、區域控制與配對比較 |
| 程式實作 | 實作生成／補全研究功能、VLM QA、mask processing 與 evaluation utilities |
| 實驗執行 | 建立實驗矩陣，執行生成與重試，整理各分支結果與停止決策 |
| 評估分析 | 結合量化指標與人工判讀，分析失敗案例，整理正結果、負結果與未定論 |
| 系統整合 | 將生成、補全與 QA 工作接入 Layer Lab 的圖層操作流程，參與生成側整合 |

[研究時間軸](experiments/00_research_timeline.md)保留生成方法的比較與決策。ALDOC 的公開架構也涵蓋團隊整合的預設分層流程與測試中的場景、物件、部件三層模式。[Layer Lab 系統架構與操作展示](system_evolution.md)

第三方模型、論文方法與美術素材均依來源標註。本 repository 的 [精選實作](selected_implementation.md)為通用 mask 與 evaluation 工具；來源及重用條件見 [NOTICE](../NOTICE.md)。
