# 主動脈瓣膜物件偵測 - YOLOv12

這是 CE6102 課程的 YOLO 作業專案，使用 YOLOv12 模型對 CT 掃描影像中的主動脈瓣膜進行物件偵測。

## 📋 專案概述

本專案使用深度學習技術，特別是 YOLOv12（You Only Look Once）物件偵測模型，來識別和定位 CT 掃描影像中的主動脈瓣膜。這對於醫學影像分析和輔助診斷具有重要意義。

**Kaggle 競賽連結**: [CE6102 YOLO HW 2025](https://www.kaggle.com/competitions/ce6102-yolo-hw-2025/overview)

## 🎯 專案目標

- 訓練 YOLOv12 模型來偵測 CT 影像中的主動脈瓣膜
- 實現高準確度的物件偵測和定位
- 生成符合競賽格式的預測結果

## 📁 檔案結構

```
.
├── README.md                                    # 專案說明文件（繁體中文）
├── train_aortic_valve_object_detection.ipynb  # 模型訓練筆記本
├── test_aortic_valve_object_detection.ipynb   # 模型測試與預測筆記本
├── best.pt                                      # 訓練完成的最佳模型權重
├── predict_label.csv                            # 預測結果檔案
├── requirements.txt                             # Python 套件依賴
├── LICENSE                                      # 授權文件
└── .gitignore                                   # Git 忽略檔案設定
```

## 🚀 快速開始

### 環境需求

- Python 3.12+
- CUDA 12.4+ (建議使用 GPU 進行訓練)
- 至少 16GB RAM
- Google Colab (推薦) 或本地 GPU 環境

### 安裝步驟

1. **複製專案**
```bash
git clone https://github.com/你的用戶名/aortic-valve-detection.git
cd aortic-valve-detection
```

2. **安裝依賴套件**
```bash
pip install -r requirements.txt
```

3. **下載資料集**
   - 從 [Kaggle 競賽頁面](https://www.kaggle.com/competitions/ce6102-yolo-hw-2025/data) 下載資料集
   - 解壓縮並放置於適當目錄

### 使用方法

#### 訓練模型

使用 `train_aortic_valve_object_detection.ipynb` 筆記本進行模型訓練：

1. 開啟 Google Colab 或 Jupyter Notebook
2. 上傳訓練筆記本
3. 確認已設定 GPU 運行環境
4. 依序執行所有儲存格
5. 訓練完成後會產生 `best.pt` 模型檔案

#### 執行預測

使用 `test_aortic_valve_object_detection.ipynb` 筆記本進行預測：

1. 上傳測試筆記本和訓練好的 `best.pt` 模型
2. 載入測試資料集
3. 執行預測流程
4. 生成 `predict_label.csv` 結果檔案

## 📊 模型資訊

- **模型架構**: YOLOv12
- **框架**: Ultralytics 8.3.239
- **深度學習框架**: PyTorch 2.9.0+cu126
- **訓練硬體**: Tesla T4 GPU (15GB VRAM)
- **檢測類別**: 主動脈瓣膜 (單一類別)

## 📈 結果格式

預測結果以 CSV 格式輸出，包含以下欄位：

- `id`: 預測序號
- `image_name`: 影像檔名
- `class`: 類別（0 代表主動脈瓣膜）
- `confidence`: 信心分數
- `top-left x-coordinate`: 邊界框左上角 X 座標
- `top-left y-coordinate`: 邊界框左上角 Y 座標
- `bottom-right x-coordinate`: 邊界框右下角 X 座標
- `bottom-right y-coordinate`: 邊界框右下角 Y 座標

範例：
```csv
id,image_name,class,confidence,top-left x-coordinate,top-left y-coordinate,bottom-right x-coordinate,bottom-right y-coordinate
0,test_patient0001_0003,0,0.3590,111,283,146,306
```

## 🔧 技術細節

### 訓練配置

- **優化器**: 自動選擇（Ultralytics 預設）
- **資料增強**: 包含翻轉、縮放、旋轉等
- **批次大小**: 根據 GPU 記憶體自動調整
- **訓練輪數**: 可在筆記本中自訂

### 推論配置

- **信心閾值**: 可調整（預設值請參考測試筆記本）
- **NMS 閾值**: 非極大值抑制閾值
- **輸入尺寸**: 根據模型訓練時的設定

## 📝 注意事項

1. **GPU 記憶體**: 訓練過程需要充足的 GPU 記憶體，建議使用至少 12GB VRAM 的顯示卡
2. **資料預處理**: 確保影像格式和標註格式符合 YOLO 要求
3. **編碼設定**: 程式碼中包含 UTF-8 編碼設定，避免中文字元錯誤
4. **模型儲存**: 訓練過程會自動儲存最佳模型權重

## 🤝 貢獻

歡迎提出問題和建議！如果你想為專案做出貢獻：

1. Fork 此專案
2. 建立你的功能分支 (`git checkout -b feature/AmazingFeature`)
3. 提交你的修改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 開啟 Pull Request

## 📄 授權

本專案採用 MIT 授權條款 - 詳見 [LICENSE](LICENSE) 檔案

## 👨‍🏫 課程資訊

- **課程**: CE6102
- **作業**: YOLO Object Detection
- **指導教授**: Prof. Chia-Yu Lin
- **年度**: 2025

## 🙏 致謝

- [Ultralytics YOLOv12](https://github.com/ultralytics/ultralytics) - 提供優秀的 YOLO 實作框架
- [Kaggle](https://www.kaggle.com/) - 提供競賽平台和資料集
- Prof. Chia-Yu Lin - 課程指導與支持

## 📧 聯絡方式

如有任何問題或建議，請透過以下方式聯絡：

- 開啟 GitHub Issue
- 電子郵件：[你的信箱]

---

⭐ 如果這個專案對你有幫助，請給予星標支持！
