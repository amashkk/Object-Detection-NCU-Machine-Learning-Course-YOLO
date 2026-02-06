# 貢獻指南

感謝你有興趣為本專案做出貢獻！這份文件提供了貢獻的指引和最佳實踐。

## 目錄

- [行為準則](#行為準則)
- [如何貢獻](#如何貢獻)
- [開發流程](#開發流程)
- [程式碼規範](#程式碼規範)
- [提交訊息規範](#提交訊息規範)
- [Pull Request 流程](#pull-request-流程)

## 行為準則

### 我們的承諾

為了營造一個開放且友善的環境，我們承諾讓每個人都能無騷擾地參與此專案，無論年齡、體型、殘疾、種族、性別認同、經驗水平、國籍、外表、種族、宗教或性取向。

### 我們的標準

正面行為包括：

- 使用友善和包容的語言
- 尊重不同的觀點和經驗
- 優雅地接受建設性批評
- 關注對社群最有利的事情
- 對其他社群成員表示同理心

不可接受的行為包括：

- 使用帶有性意味的語言或圖像
- 挑釁、侮辱或貶損的評論，以及人身或政治攻擊
- 公開或私下騷擾
- 未經許可發布他人的私人資訊
- 其他在專業環境中可合理視為不適當的行為

## 如何貢獻

### 回報 Bug

如果你發現 Bug，請開啟一個 Issue，並包含以下資訊：

- **清晰的標題**：簡潔描述問題
- **詳細描述**：說明問題的詳細情況
- **重現步驟**：列出重現 Bug 的步驟
- **預期行為**：說明你預期應該發生什麼
- **實際行為**：說明實際發生了什麼
- **環境資訊**：
  - 作業系統（Windows/Linux/macOS）
  - Python 版本
  - CUDA 版本（如適用）
  - GPU 型號（如適用）
  - 相關套件版本
- **截圖或日誌**：如果有的話，附上相關截圖或錯誤訊息

### 建議新功能

如果你有新功能的想法：

1. **檢查現有 Issues**：確認是否已有類似建議
2. **開啟新 Issue**：清楚描述你的提案
3. **說明理由**：解釋為什麼這個功能有用
4. **提供範例**：如果可能，提供使用情境或範例

### 改進文件

文件改進永遠受歡迎！包括：

- 修正拼寫或文法錯誤
- 改善說明的清晰度
- 新增缺少的資訊
- 翻譯文件
- 新增使用範例

## 開發流程

### 1. Fork 專案

點擊 GitHub 頁面右上角的 "Fork" 按鈕。

### 2. Clone 到本地

```bash
git clone https://github.com/你的用戶名/aortic-valve-detection.git
cd aortic-valve-detection
```

### 3. 建立分支

```bash
# 從 main 分支建立新分支
git checkout -b feature/你的功能名稱

# 或針對 Bug 修復
git checkout -b fix/Bug描述
```

分支命名規範：
- `feature/` - 新功能
- `fix/` - Bug 修復
- `docs/` - 文件更新
- `refactor/` - 程式碼重構
- `test/` - 測試相關

### 4. 設定開發環境

```bash
# 建立虛擬環境
python -m venv venv

# 啟動虛擬環境
# Windows
venv\Scripts\activate
# Linux/Mac
source venv/bin/activate

# 安裝依賴
pip install -r requirements.txt

# 安裝開發依賴（如果有）
pip install pytest black flake8
```

### 5. 進行修改

進行你的程式碼修改，確保：

- 程式碼符合專案風格
- 新增適當的註解
- 更新相關文件
- 新增或更新測試（如適用）

### 6. 測試你的修改

```bash
# 執行測試（如果有測試套件）
pytest

# 檢查程式碼風格
flake8 .

# 格式化程式碼
black .
```

### 7. 提交修改

```bash
git add .
git commit -m "feat: 新增某某功能"
```

### 8. 推送到 GitHub

```bash
git push origin feature/你的功能名稱
```

### 9. 建立 Pull Request

1. 前往你的 Fork 在 GitHub 上的頁面
2. 點擊 "New Pull Request"
3. 選擇你的分支
4. 填寫 PR 描述（見下方範本）
5. 提交 Pull Request

## 程式碼規範

### Python 風格指南

遵循 [PEP 8](https://www.python.org/dev/peps/pep-0008/) 風格指南：

```python
# 良好的範例
def detect_aortic_valve(image_path: str, confidence_threshold: float = 0.5) -> list:
    """
    偵測影像中的主動脈瓣膜。
    
    Args:
        image_path: 影像檔案路徑
        confidence_threshold: 信心分數閾值
        
    Returns:
        包含偵測結果的列表
    """
    # 載入模型
    model = load_model()
    
    # 執行預測
    results = model.predict(image_path, conf=confidence_threshold)
    
    return results
```

### 命名慣例

- **變數和函數**：使用 `snake_case`
  ```python
  image_path = "test.jpg"
  def calculate_accuracy():
      pass
  ```

- **類別**：使用 `PascalCase`
  ```python
  class AorticValveDetector:
      pass
  ```

- **常數**：使用 `UPPER_CASE`
  ```python
  MAX_BATCH_SIZE = 32
  DEFAULT_CONFIDENCE = 0.5
  ```

### 註解規範

```python
# 單行註解使用 #

"""
多行註解或 docstring 使用三引號。
說明函數、類別或模組的用途。
"""

def function_name(param1, param2):
    """
    函數的簡短描述。
    
    更詳細的說明（如果需要）。
    
    Args:
        param1 (type): 參數 1 的描述
        param2 (type): 參數 2 的描述
        
    Returns:
        type: 回傳值的描述
        
    Raises:
        ExceptionType: 何時會拋出此例外
    """
    pass
```

### Jupyter Notebook 規範

- 每個 cell 應有清楚的目的
- 使用 Markdown cell 說明步驟
- 保持程式碼 cell 簡潔
- 執行前清除所有輸出（除非展示結果）

## 提交訊息規範

使用 [Conventional Commits](https://www.conventionalcommits.org/) 格式：

```
<類型>(<範圍>): <簡短描述>

<詳細描述>（可選）

<footer>（可選）
```

### 類型

- `feat`: 新功能
- `fix`: Bug 修復
- `docs`: 文件變更
- `style`: 程式碼格式（不影響功能）
- `refactor`: 重構（既非新功能也非修復）
- `test`: 新增或修改測試
- `chore`: 建置過程或輔助工具的變動

### 範例

```bash
# 新功能
git commit -m "feat: 新增批次預測功能"

# Bug 修復
git commit -m "fix: 修復信心分數計算錯誤"

# 文件更新
git commit -m "docs: 更新 README 安裝說明"

# 重構
git commit -m "refactor: 重構資料載入邏輯以提升效能"
```

## Pull Request 流程

### PR 標題

使用與 commit 訊息相同的格式：

```
feat: 新增某某功能
fix: 修復某某問題
docs: 更新某某文件
```

### PR 描述範本

```markdown
## 描述
簡要說明此 PR 的目的和修改內容。

## 動機和背景
解釋為什麼需要這個變更。

## 修改類型
- [ ] Bug 修復
- [ ] 新功能
- [ ] 重構
- [ ] 文件更新
- [ ] 其他（請說明）

## 測試
說明你如何測試這些變更：
- [ ] 單元測試
- [ ] 整合測試
- [ ] 手動測試

## 檢查清單
- [ ] 程式碼符合專案風格指南
- [ ] 已自我審查程式碼
- [ ] 程式碼已加上適當註解
- [ ] 已更新相關文件
- [ ] 變更不會產生新的警告
- [ ] 已新增測試證明修復有效或功能正常運作
- [ ] 所有測試都通過

## 截圖（如適用）
如果是 UI 相關變更，請附上截圖。

## 相關 Issue
關閉 #（issue 編號）
```

### Review 流程

1. **提交 PR** 後，維護者會進行審查
2. **回應評論**：認真對待 reviewer 的建議
3. **進行修改**：根據回饋更新程式碼
4. **保持更新**：確保你的分支與主分支同步

```bash
# 同步主分支
git checkout main
git pull upstream main
git checkout feature/你的功能名稱
git rebase main
```

5. **合併**：一旦獲得批准，維護者會合併你的 PR

## 建議與最佳實踐

### 提交頻率

- 經常提交小的、有意義的變更
- 每個 commit 應該是一個邏輯單元
- 避免混合不相關的修改

### 程式碼品質

- 撰寫清晰、可讀的程式碼
- 避免過度複雜的邏輯
- 使用有意義的變數和函數名稱
- 移除除錯用的 print 語句

### 測試

- 為新功能撰寫測試
- 確保現有測試仍然通過
- 測試邊界情況和錯誤情境

### 文件

- 更新或新增相關文件
- 確保範例程式碼可以執行
- 解釋複雜的邏輯或設計決策

## 問題與協助

如果你有任何問題或需要協助：

1. 查看現有的 Issues 和 Discussions
2. 閱讀專案文件
3. 在 GitHub 上開啟新 Issue
4. 參與社群討論

## 感謝

再次感謝你的貢獻！每一個貢獻都讓這個專案變得更好。

---

最後更新：2025年2月
