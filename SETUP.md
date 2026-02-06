# 環境設定指南

本文件提供詳細的環境設定步驟，幫助你順利執行此專案。

## 目錄

- [系統需求](#系統需求)
- [Google Colab 設定](#google-colab-設定)
- [本地環境設定](#本地環境設定)
- [資料集準備](#資料集準備)
- [常見問題](#常見問題)

## 系統需求

### 最低需求
- Python 3.12 或更新版本
- 16GB RAM
- 50GB 可用硬碟空間
- GPU: NVIDIA GPU with CUDA support (建議)
  - 最低 8GB VRAM
  - 建議 12GB+ VRAM (如 Tesla T4, RTX 3060 或更好)

### 建議配置
- Python 3.12
- 32GB RAM
- 100GB SSD 硬碟空間
- GPU: Tesla T4 / V100 / A100 或 RTX 3080+

## Google Colab 設定

推薦使用 Google Colab，它提供免費的 GPU 資源且環境設定簡單。

### 步驟 1: 啟用 GPU

1. 開啟 Google Colab: https://colab.research.google.com/
2. 點選 `Runtime` (執行階段) → `Change runtime type` (變更執行階段類型)
3. 在 `Hardware accelerator` (硬體加速器) 選擇 `GPU`
4. 點選 `Save` (儲存)

### 步驟 2: 驗證 GPU

執行以下程式碼確認 GPU 可用：

```python
!nvidia-smi
```

應該會看到類似以下輸出：
```
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 550.54.15    Driver Version: 550.54.15    CUDA Version: 12.4   |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
|   0  Tesla T4            Off  | 00000000:00:04.0 Off |                    0 |
+-------------------------------+----------------------+----------------------+
```

### 步驟 3: 安裝依賴套件

```python
!pip install ultralytics
```

### 步驟 4: 上傳檔案

使用 Colab 的檔案上傳功能：
1. 點選左側的資料夾圖示
2. 點選上傳圖示
3. 選擇訓練或測試筆記本、模型檔案等

## 本地環境設定

### Windows

#### 步驟 1: 安裝 Python

1. 下載 Python 3.12: https://www.python.org/downloads/
2. 安裝時勾選 `Add Python to PATH`
3. 驗證安裝：
```bash
python --version
```

#### 步驟 2: 安裝 CUDA (使用 GPU)

1. 檢查 GPU 驅動版本：
```bash
nvidia-smi
```

2. 下載並安裝 CUDA Toolkit 12.4: https://developer.nvidia.com/cuda-downloads

3. 下載並安裝 cuDNN: https://developer.nvidia.com/cudnn

#### 步驟 3: 建立虛擬環境

```bash
# 建立虛擬環境
python -m venv venv

# 啟動虛擬環境
venv\Scripts\activate

# 安裝依賴套件
pip install -r requirements.txt
```

### Linux / macOS

#### 步驟 1: 安裝 Python

```bash
# Ubuntu/Debian
sudo apt update
sudo apt install python3.12 python3-pip

# macOS (使用 Homebrew)
brew install python@3.12
```

#### 步驟 2: 安裝 CUDA (Linux, 使用 GPU)

```bash
# 檢查 GPU
nvidia-smi

# 安裝 CUDA (Ubuntu)
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/cuda-ubuntu2204.pin
sudo mv cuda-ubuntu2204.pin /etc/apt/preferences.d/cuda-repository-pin-600
wget https://developer.download.nvidia.com/compute/cuda/12.4.0/local_installers/cuda-repo-ubuntu2204-12-4-local_12.4.0-550.54.14-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu2204-12-4-local_12.4.0-550.54.14-1_amd64.deb
sudo apt-get update
sudo apt-get -y install cuda
```

#### 步驟 3: 建立虛擬環境

```bash
# 建立虛擬環境
python3 -m venv venv

# 啟動虛擬環境
source venv/bin/activate

# 安裝依賴套件
pip install -r requirements.txt
```

## 資料集準備

### 從 Kaggle 下載

#### 方法 1: 網頁下載

1. 造訪競賽頁面: https://www.kaggle.com/competitions/ce6102-yolo-hw-2025/data
2. 登入你的 Kaggle 帳號
3. 點選 `Download All` 下載所有檔案
4. 解壓縮檔案到專案目錄

#### 方法 2: 使用 Kaggle API

1. 安裝 Kaggle API:
```bash
pip install kaggle
```

2. 設定 API 金鑰:
   - 前往 https://www.kaggle.com/settings/account
   - 點選 `Create New API Token`
   - 下載 `kaggle.json`
   - 將檔案放置於:
     - Windows: `C:\Users\<你的用戶名>\.kaggle\kaggle.json`
     - Linux/Mac: `~/.kaggle/kaggle.json`

3. 下載資料集:
```bash
kaggle competitions download -c ce6102-yolo-hw-2025
```

### 資料集結構

下載後的資料集應該有以下結構：

```
dataset/
├── train/
│   ├── images/
│   │   ├── train_patient0001_0001.png
│   │   ├── train_patient0001_0002.png
│   │   └── ...
│   └── labels/
│       ├── train_patient0001_0001.txt
│       ├── train_patient0001_0002.txt
│       └── ...
├── val/
│   ├── images/
│   └── labels/
└── test/
    └── images/
```

## 啟動 Jupyter Notebook

### 本地環境

```bash
# 確保虛擬環境已啟動
# Windows: venv\Scripts\activate
# Linux/Mac: source venv/bin/activate

# 啟動 Jupyter Notebook
jupyter notebook
```

瀏覽器會自動開啟，選擇要執行的筆記本檔案。

## 常見問題

### Q1: CUDA out of memory 錯誤

**解決方法**:
- 減少批次大小 (batch size)
- 使用較小的輸入影像尺寸
- 關閉其他佔用 GPU 記憶體的程式
- 使用 Google Colab Pro 獲取更多 GPU 記憶體

### Q2: 找不到 CUDA

**解決方法**:
```python
import torch
print(torch.cuda.is_available())  # 應該顯示 True
print(torch.cuda.get_device_name(0))  # 顯示 GPU 名稱
```

如果顯示 False，請:
1. 確認已安裝正確版本的 CUDA
2. 確認已安裝 GPU 版本的 PyTorch
3. 重新安裝 PyTorch: `pip install torch torchvision --index-url https://download.pytorch.org/whl/cu124`

### Q3: ModuleNotFoundError

**解決方法**:
```bash
# 確保所有依賴都已安裝
pip install -r requirements.txt

# 或個別安裝缺少的套件
pip install ultralytics
```

### Q4: 訓練速度很慢

**可能原因**:
1. 未使用 GPU (使用 CPU 訓練)
2. 批次大小過小
3. 資料增強過於複雜

**解決方法**:
- 確認 GPU 已啟用並被正確使用
- 適當增加批次大小
- 調整資料增強參數

### Q5: 記憶體不足（RAM）

**解決方法**:
- 減少 DataLoader 的 workers 數量
- 減少批次大小
- 使用較小的模型
- 關閉不必要的程式

## 效能優化建議

### 訓練加速

1. **使用混合精度訓練**:
```python
# Ultralytics 會自動使用 AMP (Automatic Mixed Precision)
model.train(data='config.yaml', amp=True)
```

2. **調整批次大小**:
```python
# 盡可能使用最大批次大小而不超出記憶體
model.train(data='config.yaml', batch=16)  # 根據你的 GPU 調整
```

3. **使用多 GPU**:
```python
# 如果有多個 GPU
model.train(data='config.yaml', device='0,1')  # 使用 GPU 0 和 1
```

### 推論加速

1. **批次推論**:
```python
# 一次處理多張影像
results = model.predict(images, batch=32)
```

2. **降低影像尺寸**:
```python
# 使用較小的輸入尺寸
results = model.predict(images, imgsz=416)  # 預設是 640
```

## 下一步

設定完成後，請參考主要的 [README.md](README.md) 來了解如何使用此專案。

## 需要協助？

如遇到其他問題，請：
1. 查看 [Ultralytics 官方文件](https://docs.ultralytics.com/)
2. 在 GitHub 開啟 Issue
3. 參考 Stack Overflow 相關討論
