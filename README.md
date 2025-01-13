# Django Project Auto Setup with Aider

這個專案提供了一套使用 Aider 自動化部署 Django 專案的解決方案，通過定義好的規格文件（specs）和配置文件，快速建立一個具有完整結構的 Django 專案。

## 前置需求

- Python 3.12 或更高版本
- [uv](https://docs.astral.sh/uv/) - 快速的 Python 包管理工具
- [Aider CLI](https://aider.chat/) - AI 輔助代碼編輯工具
- [PostgreSQL](https://www.postgresql.org/) - 開源關係型數據庫系統

## 專案結構
```bash
.
├── project_config.yaml
├── pyproject.toml
├── README.md
└── specs/
    ├── spec-create-app.md
    ├── spec-create-project.md
    ├── spec-update-app.md
    └── spec-update-settings.md
```
## 快速開始

### 1. 設置環境

1. 克隆專案：
```bash
git clone https://github.com/allenshie/AIDER-Auto-setup-django-project.git
cd AIDER-Auto-setup-django-project
```

2. 使用 uv 創建和同步虛擬環境：
```bash
uv sync
```

### 2. 設置環境變量
複製 .env.sample 檔產生 .env 並設置你的 OPENAI_API_KEY | ANTHROPIC_API_KEY , DJANGO_SECRET_KEY, DB_PASSWORD
```bash
cp .env.sample .env
```
創建並設置必要的環境變量：

```bash
# Linux/MacOS
export OPENAI_API_KEY="your-openai-api-key"
export DJANGO_SECRET_KEY="your-django-secret-key"
export DB_PASSWORD="your-database-password"

# Windows PowerShell
$env:OPENAI_API_KEY="your-openai-api-key"
$env:DJANGO_SECRET_KEY="your-django-secret-key"
$env:DB_PASSWORD="your-database-password"
```

### 3. 配置專案
檢查並按需修改 project_config.yaml：
專案名稱
應用名稱
數據庫配置
模型定義
### 4. 使用 Aider 自動化部署
需按照以下順序執行自動化部署步驟：

啟動 aider
```bash
aider
```
1. 創建 Django 專案:
    ```bash
    # 在 aider shell 中執行：
    /add pyproject.toml
    /add project_config.yaml
    # 複製 specs/spec-create-project.md 的內容貼上到 aider 
    ```
2. 創建 Django 應用:
    ```bash
    # 在 aider shell 中執行：
    /add pyproject.toml
    /add project_config.yaml
    # 複製 specs/spec-create-app.md 的內容貼上到 aider shell
    ```
3. 更新專案設置:
    ```bash
    # 在 aider shell 中執行：
    /add pyproject.toml
    /add project_config.yaml
    /add {PROJECT_NAME}/{PROJECT_NAME}/settings.py
    #  複製 specs/spec-update-settings.md 的內容貼上到 aider shell
    ```
4. 創建數據模型:
    ```bash
    # 在 aider shell 中執行：
    /add pyproject.toml
    /add project_config.yaml
    /add {PROJECT_NAME}/{APP_NAME}/models.py
    # 複製 specs/spec-update-app.md 的內容貼上到 aider shell
    ```
## Aider 編譯器操作指南
Aider 編譯器提供了多個指令來管理文件和操作狀態

### 基本指令

| 指令 | 說明 |
|------|------|
| `/add <file>` | 添加檔案到 aider chat，允許 aider 讀取和修改該檔案 |
| `/read-only <file>` | 以唯讀模式添加檔案到 aider chat，僅供 aider 參考 |
| `/drop <file>` | 從 aider chat 中移除檔案 |
| `/clear` | 清除當前 aider chat 中的對話內容（執行新任務前建議先清除） |
| `/undo` | 回退最近的 git commit（當 aider 的修改需要撤銷時使用） |
| `/exit` | 退出 Aider 編譯器 |

### 使用注意事項

1. 執行新任務前的準備：
  - 使用 `/clear` 清除之前的對話
  - 使用 `/drop` 移除不需要的檔案
  - 使用 `/add` 或 `/read-only` 添加新任務需要的檔案

2. 文件權限管理：
  - 需要修改的檔案使用 `/add`
  - 僅供參考的配置文件使用 `/read-only`
  - 不再需要的檔案記得用 `/drop` 移除

3. 版本控制：
  - Aider 成功完成任務後會詢問是否提交到 git
  - 如果需要撤銷修改，可以使用 `/undo` 回退

## 自定義配置
### 修改專案配置
#### 編輯 project_config.yaml 文件以自定義：
- 專案和應用名稱
- 數據庫連接信息
- 模型定義
- 其他 Django 設置
### 修改依賴
如需添加或修改 Python 包依賴，編輯 pyproject.toml 文件。

### 注意事項
1. 確保 PostgreSQL 服務已啟動且可訪問
2. 環境變量必須在執行 Aider 命令前設置
3. 按照指定順序執行 spec 文件
4. 確保已正確配置 Aider（包括 API key）
### 排錯指南
如果遇到問題
1. 確認所有環境變量已正確設置
2. 確認 PostgreSQL 服務正在運行
3. 檢查 project_config.yaml 的語法是否正確
4. 確保按正確順序執行 spec 文件