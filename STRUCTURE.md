# 專案結構說明

本文件詳細說明專案的目錄結構和各檔案的用途。

## 📁 目錄結構

```
aortic-valve-detection/
│
├── README.md                                    # 專案主要說明文件
├── SETUP.md                                     # 環境設定指南
├── CONTRIBUTING.md                              # 貢獻指南
├── RESULTS.md                                   # 訓練與結果說明
├── STRUCTURE.md                                 # 專案結構說明（本文件）
├── LICENSE                                      # MIT 授權條款
├── .gitignore                                   # Git 忽略檔案設定
├── requirements.txt                             # Python 依賴套件清單
│
├── train_aortic_valve_object_detection.ipynb   # 訓練筆記本
├── test_aortic_valve_object_detection.ipynb    # 測試與預測筆記本
│
├── best.pt                                      # 訓練完成的最佳模型權重
└── predict_label.csv                            # 測試集預測結果
```

## 📄 檔案說明

### 文件檔案

#### README.md
- **用途**: 專案的主要說明文件
- **內容**:
  - 專案概述和目標
  - 快速開始指南
  - 使用方法
  - 模型資訊
  - 結果格式說明
- **對象**: 所有使用者（初學者到進階）

#### SETUP.md
- **用途**: 詳細的環境設定指南
- **內容**:
  - 系統需求
  - Google Colab 設定步驟
  - 本地環境設定（Windows/Linux/macOS）
  - 資料集下載和準備
  - 常見問題解答
- **對象**: 需要設定環境的使用者

#### CONTRIBUTING.md
- **用途**: 貢獻者指南
- **內容**:
  - 行為準則
  - 貢獻流程
  - 程式碼規範
  - Pull Request 流程
  - 最佳實踐
- **對象**: 想要貢獻程式碼或改進的開發者

#### RESULTS.md
- **用途**: 訓練過程和結果說明
- **內容**:
  - 訓練環境和配置
  - 模型架構說明
  - 評估指標解釋
  - 預測結果分析
  - 改進方向建議
- **對象**: 想了解模型細節的研究者和開發者

#### STRUCTURE.md
- **用途**: 專案結構說明（本文件）
- **內容**:
  - 目錄樹狀結構
  - 各檔案的用途和說明
  - 檔案之間的關係
- **對象**: 想快速了解專案組織的使用者

#### LICENSE
- **用途**: 開源授權條款
- **內容**: MIT License 全文
- **說明**: 允許自由使用、修改和分發，但需保留版權聲明

### 配置檔案

#### requirements.txt
- **用途**: Python 套件依賴清單
- **格式**: 每行一個套件及其版本
- **使用**: `pip install -r requirements.txt`
- **包含套件**:
  - ultralytics: YOLO 框架
  - torch: PyTorch 深度學習框架
  - opencv-python: 影像處理
  - pandas: 資料處理
  - matplotlib: 視覺化
  - 其他輔助套件

#### .gitignore
- **用途**: 告訴 Git 忽略哪些檔案
- **包含項目**:
  - Python 快取檔案 (`__pycache__/`, `*.pyc`)
  - 虛擬環境 (`venv/`, `env/`)
  - Jupyter 檢查點 (`.ipynb_checkpoints/`)
  - 大型資料檔案 (資料集、訓練輸出)
  - IDE 設定檔案 (`.vscode/`, `.idea/`)
  - 系統檔案 (`.DS_Store`, `Thumbs.db`)

### 程式碼檔案

#### train_aortic_valve_object_detection.ipynb
- **類型**: Jupyter Notebook
- **用途**: 模型訓練流程
- **主要內容**:
  1. 環境設定和檢查
  2. 資料集載入和預處理
  3. 模型配置和初始化
  4. 訓練循環
  5. 模型評估
  6. 保存最佳模型
- **輸出**: `best.pt` 模型檔案
- **執行環境**: Google Colab 或本地 Jupyter
- **預計執行時間**: 根據資料集大小和訓練輪數而定

#### test_aortic_valve_object_detection.ipynb
- **類型**: Jupyter Notebook
- **用途**: 模型測試和預測
- **主要內容**:
  1. 環境設定
  2. 載入訓練好的模型 (`best.pt`)
  3. 載入測試資料集
  4. 執行批次預測
  5. 結果後處理
  6. 生成提交檔案
- **輸出**: `predict_label.csv` 預測結果
- **執行環境**: Google Colab 或本地 Jupyter
- **預計執行時間**: 根據測試集大小而定

### 資料檔案

#### best.pt
- **類型**: PyTorch 模型權重檔案
- **大小**: ~5.3 MB
- **用途**: 保存訓練完成的最佳模型權重
- **內容**:
  - 模型架構參數
  - 訓練權重
  - 優化器狀態（如果保存）
  - 訓練配置資訊
- **使用方法**:
  ```python
  from ultralytics import YOLO
  model = YOLO('best.pt')
  ```

#### predict_label.csv
- **類型**: CSV 檔案
- **大小**: ~60 KB
- **用途**: 測試集的預測結果
- **格式**:
  ```csv
  id,image_name,class,confidence,top-left x-coordinate,top-left y-coordinate,bottom-right x-coordinate,bottom-right y-coordinate
  ```
- **欄位說明**:
  - `id`: 預測編號（整數）
  - `image_name`: 影像檔名（字串）
  - `class`: 類別標籤（0 = 主動脈瓣膜）
  - `confidence`: 信心分數（0-1 浮點數）
  - 座標欄位: 邊界框的左上和右下角座標（整數）
- **總筆數**: 1166 筆預測結果
- **用途**: 提交到 Kaggle 競賽或進行結果分析

## 🔄 檔案關係與工作流程

### 1. 訓練流程

```
requirements.txt → 安裝依賴
        ↓
train_aortic_valve_object_detection.ipynb → 訓練模型
        ↓
    best.pt → 保存最佳模型
```

### 2. 測試流程

```
best.pt → 載入模型
        ↓
test_aortic_valve_object_detection.ipynb → 執行預測
        ↓
predict_label.csv → 保存預測結果
```

### 3. 文件閱讀順序

對於新使用者，建議的閱讀順序：

1. **README.md** - 了解專案概況
2. **SETUP.md** - 設定開發環境
3. **train_aortic_valve_object_detection.ipynb** - 學習訓練流程
4. **test_aortic_valve_object_detection.ipynb** - 學習預測流程
5. **RESULTS.md** - 深入了解模型和結果
6. **CONTRIBUTING.md** - 如果想要貢獻

## 📦 可選的擴展結構

如果專案持續發展，可能會增加以下結構：

```
aortic-valve-detection/
│
├── docs/                           # 更詳細的文件
│   ├── api_reference.md           # API 參考文件
│   ├── tutorials/                 # 教學文件
│   └── research_notes.md          # 研究筆記
│
├── src/                           # 源代碼模組
│   ├── __init__.py
│   ├── data/                      # 資料處理模組
│   ├── models/                    # 模型定義
│   ├── utils/                     # 工具函數
│   └── visualization/             # 視覺化工具
│
├── tests/                         # 單元測試
│   ├── test_data.py
│   ├── test_model.py
│   └── test_utils.py
│
├── scripts/                       # 輔助腳本
│   ├── download_data.sh          # 資料下載腳本
│   ├── train.py                  # 命令列訓練腳本
│   └── predict.py                # 命令列預測腳本
│
├── configs/                       # 配置檔案
│   ├── train_config.yaml         # 訓練配置
│   └── model_config.yaml         # 模型配置
│
├── data/                          # 資料目錄（不提交到 Git）
│   ├── raw/                      # 原始資料
│   ├── processed/                # 處理後的資料
│   └── external/                 # 外部資料
│
├── models/                        # 模型檔案目錄
│   ├── best.pt
│   ├── last.pt
│   └── checkpoints/              # 訓練檢查點
│
├── results/                       # 結果輸出目錄
│   ├── predictions/              # 預測結果
│   ├── visualizations/           # 視覺化圖表
│   └── metrics/                  # 評估指標
│
└── notebooks/                     # Jupyter Notebooks
    ├── 01_data_exploration.ipynb # 資料探索
    ├── 02_model_training.ipynb   # 模型訓練
    ├── 03_model_evaluation.ipynb # 模型評估
    └── 04_prediction.ipynb       # 預測
```

## 🔧 Git 管理策略

### 應該提交的檔案

✅ 所有文件（.md 檔案）
✅ 程式碼檔案（.py, .ipynb）
✅ 配置檔案（requirements.txt, .gitignore）
✅ 小型資料檔案（< 10 MB）

### 不應該提交的檔案

❌ 大型模型檔案（> 100 MB，考慮使用 Git LFS）
❌ 資料集（通常很大，提供下載連結即可）
❌ 虛擬環境
❌ 快取檔案
❌ IDE 設定檔案
❌ 臨時檔案和日誌

### Git LFS (Large File Storage)

對於大型檔案（如 `best.pt`），如果必須提交到 Git，建議使用 Git LFS：

```bash
# 安裝 Git LFS
git lfs install

# 追蹤大型檔案
git lfs track "*.pt"
git lfs track "*.pth"
git lfs track "*.h5"

# 提交 .gitattributes
git add .gitattributes
git commit -m "Add Git LFS tracking"

# 正常提交大型檔案
git add best.pt
git commit -m "Add trained model"
git push
```

## 📊 檔案大小統計

```
總大小: ~6.8 MB

檔案大小分布:
├── best.pt                  5.3 MB  (78%)
├── predict_label.csv       60 KB   (1%)
├── notebooks               ~1.4 MB (20%)
└── 文件和配置              ~50 KB  (1%)
```

## 🎯 維護建議

1. **定期更新文件**: 當專案有重大變更時更新相關文件
2. **保持結構清晰**: 避免在根目錄堆積過多檔案
3. **使用有意義的命名**: 檔案和目錄名稱應該清楚表達其用途
4. **適當的模組化**: 當專案變大時，考慮將功能拆分成模組
5. **版本控制**: 對重要變更使用 Git tags 標記版本

## 📝 檢查清單

在提交到 GitHub 前，確保：

- [ ] 所有文件都是最新的
- [ ] README 包含清晰的使用說明
- [ ] requirements.txt 包含所有依賴
- [ ] .gitignore 正確配置
- [ ] 移除敏感資訊（API keys, 密碼等）
- [ ] 大型檔案使用 Git LFS 或提供下載連結
- [ ] 所有程式碼都經過測試
- [ ] LICENSE 檔案包含正確的年份和作者資訊

---

最後更新：2025年2月6日
