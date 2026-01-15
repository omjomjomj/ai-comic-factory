# AI Comic Factory 完整教學指南

## 📖 專案簡介

**AI Comic Factory** 是一個開源的 AI 漫畫生成工具，讓您只需輸入一段文字描述，就能自動生成多格漫畫。它結合了大型語言模型 (LLM) 來編寫故事，以及 Stable Diffusion XL (SDXL) 來繪製漫畫畫面。

### 核心功能
- 🎨 **一鍵生成漫畫**: 輸入故事描述，AI 自動生成完整漫畫
- 📝 **故事編排**: 使用 LLM 將您的想法轉化為漫畫分鏡
- 🖼️ **高品質圖像**: 使用 SDXL 生成精美的漫畫畫面
- 🔧 **多種風格**: 支援多種漫畫風格和佈局
- 📤 **導出功能**: 可導出為圖片格式

---

## 🚀 快速開始

### 系統需求

| 項目 | 最低要求 | 建議配置 |
|------|----------|----------|
| **Node.js** | 18.x | 20.x |
| **NPM** | 9.x | 10.x |
| **記憶體** | 4GB | 8GB |
| **網路** | 穩定連線 | 高速連線 |

### 安裝步驟

#### 步驟 1: 進入專案目錄

```powershell
cd c:\Users\omjom\Downloads\AI-comic\ai-comic-factory
```

#### 步驟 2: 安裝依賴

```powershell
npm install
```

#### 步驟 3: 配置環境變數

```powershell
# 複製範本文件
copy .env.example .env

# 或者創建 .env.local（推薦，用於覆蓋特定設定）
copy .env.example .env.local
```

#### 步驟 4: 編輯配置文件

使用任何文字編輯器打開 `.env` 或 `.env.local`，填入您的 API 金鑰。

#### 步驟 5: 啟動開發伺服器

```powershell
npm run dev
```

#### 步驟 6: 訪問應用

打開瀏覽器，訪問 **http://localhost:3000**

---

## 🔑 API 配置詳解

### LLM 引擎選項 (故事生成)

您需要選擇一個 LLM 引擎來生成漫畫故事腳本：

#### 選項 1: Hugging Face Inference API (免費入門)

```env
LLM_ENGINE="INFERENCE_API"
AUTH_HF_API_TOKEN=<YOUR_HUGGINGFACE_TOKEN>
LLM_HF_INFERENCE_API_MODEL="HuggingFaceH4/zephyr-7b-beta"
```

**獲取方式**: https://huggingface.co/settings/tokens

**優點**: 
- ✅ 免費（有配額限制）
- ✅ 無需信用卡

**缺點**:
- ⚠️ 速度較慢
- ⚠️ 有使用限制

---

#### 選項 2: OpenAI GPT (推薦，品質最佳)

```env
LLM_ENGINE="OPENAI"
AUTH_OPENAI_API_KEY=<YOUR_OPENAI_API_KEY>
LLM_OPENAI_API_MODEL="gpt-4-turbo"
```

**獲取方式**: https://platform.openai.com/api-keys

**優點**:
- ✅ 故事品質最佳
- ✅ 生成速度快
- ✅ 支援中文

**缺點**:
- ⚠️ 需要付費
- ⚠️ 需要信用卡

**費用估算**: 
- gpt-4-turbo: 約 $0.01-0.03 / 次漫畫生成

---

#### 選項 3: Groq (快速且便宜)

```env
LLM_ENGINE="GROQ"
AUTH_GROQ_API_KEY=<YOUR_GROQ_API_KEY>
LLM_GROQ_API_MODEL="mixtral-8x7b-32768"
```

**獲取方式**: https://console.groq.com/keys

**優點**:
- ✅ 速度極快
- ✅ 免費配額慷慨
- ✅ 無需信用卡

**缺點**:
- ⚠️ 中文支援較弱

---

#### 選項 4: Anthropic Claude (高品質)

```env
LLM_ENGINE="ANTHROPIC"
AUTH_ANTHROPIC_API_KEY=<YOUR_ANTHROPIC_API_KEY>
LLM_ANTHROPIC_API_MODEL="claude-3-opus-20240229"
```

**獲取方式**: https://console.anthropic.com/

**優點**:
- ✅ 故事品質優秀
- ✅ 安全性高

**缺點**:
- ⚠️ 需要付費

---

### 渲染引擎選項 (圖像生成)

您需要選擇一個渲染引擎來生成漫畫圖像：

#### 選項 1: Hugging Face Inference API (免費入門)

```env
RENDERING_ENGINE="INFERENCE_API"
AUTH_HF_API_TOKEN=<YOUR_HUGGINGFACE_TOKEN>
RENDERING_HF_INFERENCE_API_BASE_MODEL="stabilityai/stable-diffusion-xl-base-1.0"
```

**優點**:
- ✅ 免費
- ✅ 使用 SDXL 模型

**缺點**:
- ⚠️ 速度較慢
- ⚠️ 可能需要排隊

---

#### 選項 2: Replicate (推薦，穩定可靠)

```env
RENDERING_ENGINE="REPLICATE"
AUTH_REPLICATE_API_TOKEN=<YOUR_REPLICATE_TOKEN>
RENDERING_REPLICATE_API_MODEL="stabilityai/sdxl"
```

**獲取方式**: https://replicate.com/account/api-tokens

**優點**:
- ✅ 穩定可靠
- ✅ 多種模型可選
- ✅ 按使用付費

**費用估算**: 
- 約 $0.00115 / 張圖像

---

#### 選項 3: OpenAI DALL-E 3 (最佳品質)

```env
RENDERING_ENGINE="OPENAI"
AUTH_OPENAI_API_KEY=<YOUR_OPENAI_API_KEY>
RENDERING_OPENAI_API_MODEL="dall-e-3"
```

**優點**:
- ✅ 圖像品質最佳
- ✅ 風格一致性好

**缺點**:
- ⚠️ 費用較高（約 $0.04-0.08 / 張）
- ⚠️ 可能有內容限制

---

## 🎯 推薦配置方案

### 方案 A: 完全免費入門

```env
# .env.local
LLM_ENGINE="INFERENCE_API"
AUTH_HF_API_TOKEN=<YOUR_HF_TOKEN>
LLM_HF_INFERENCE_API_MODEL="HuggingFaceH4/zephyr-7b-beta"

RENDERING_ENGINE="INFERENCE_API"
RENDERING_HF_INFERENCE_API_BASE_MODEL="stabilityai/stable-diffusion-xl-base-1.0"
```

**總費用**: $0 / 月（有使用限制）

---

### 方案 B: 最佳性價比 ⭐

```env
# .env.local
LLM_ENGINE="GROQ"
AUTH_GROQ_API_KEY=<YOUR_GROQ_KEY>
LLM_GROQ_API_MODEL="mixtral-8x7b-32768"

RENDERING_ENGINE="REPLICATE"
AUTH_REPLICATE_API_TOKEN=<YOUR_REPLICATE_TOKEN>
RENDERING_REPLICATE_API_MODEL="stabilityai/sdxl"
```

**總費用**: 約 $0.01-0.05 / 次漫畫生成

---

### 方案 C: 最佳品質

```env
# .env.local
LLM_ENGINE="OPENAI"
AUTH_OPENAI_API_KEY=<YOUR_OPENAI_KEY>
LLM_OPENAI_API_MODEL="gpt-4-turbo"

RENDERING_ENGINE="OPENAI"
RENDERING_OPENAI_API_MODEL="dall-e-3"
```

**總費用**: 約 $0.20-0.50 / 次漫畫生成

---

## 📋 可用命令

```powershell
# 開發模式（熱重載）
npm run dev

# 構建生產版本
npm run build

# 運行生產版本
npm start

# 代碼檢查
npm run lint
```

---

## 🐳 Docker 部署

### 使用 Docker 構建

```powershell
# 構建 Docker 映像
docker build -t ai-comic-factory .

# 運行容器
docker run -p 3000:3000 --env-file .env ai-comic-factory
```

### Docker Compose

創建 `docker-compose.yml`:

```yaml
version: '3.8'
services:
  comic-factory:
    build: .
    ports:
      - "3000:3000"
    env_file:
      - .env
    restart: unless-stopped
```

運行:
```powershell
docker-compose up -d
```

---

## 🎨 適用場景

### 1. 🎓 教育與學習

**場景**: 為課程或教材創建視覺化教學內容

**範例用途**:
- 歷史故事視覺化
- 科學概念圖解
- 語言學習故事書
- 兒童繪本創作

**優勢**: 
- 快速生成教學素材
- 吸引學生注意力
- 低成本製作教材

---

### 2. 📱 社交媒體內容

**場景**: 為社交平台創建吸睛內容

**範例用途**:
- Instagram 故事連載
- Twitter 漫畫推文
- Facebook 趣味內容
- TikTok 配圖故事

**優勢**:
- 快速生成原創內容
- 獨特的視覺風格
- 提高互動率

---

### 3. 🎮 遊戲與娛樂

**場景**: 為遊戲或娛樂項目創建美術素材

**範例用途**:
- 遊戲故事板
- 角色設計概念
- 劇情預覽漫畫
- 粉絲作品創作

**優勢**:
- 快速原型設計
- 降低美術成本
- 風格統一

---

### 4. 📰 新聞與媒體

**場景**: 為新聞報導添加視覺元素

**範例用途**:
- 事件時間線視覺化
- 複雜概念圖解
- 社論插圖
- 專題報導配圖

**優勢**:
- 快速響應新聞事件
- 獨特的視覺敘事
- 提高讀者參與度

---

### 5. 💼 商業應用

**場景**: 為企業內容創建專業視覺素材

**範例用途**:
- 產品說明漫畫
- 員工培訓材料
- 品牌故事視覺化
- 客戶溝通素材

**優勢**:
- 專業視覺呈現
- 快速製作週期
- 成本效益高

---

### 6. 🎭 創意與藝術

**場景**: 個人創作和藝術探索

**範例用途**:
- 個人漫畫創作
- 故事概念驗證
- 風格實驗
- 藝術項目原型

**優勢**:
- 無限創意可能
- 快速視覺化想法
- 低門檻藝術創作

---

## ⚙️ 進階配置

### 調整頁數

```env
# 設定漫畫最大頁數（預設 6 頁）
MAX_NB_PAGES=8
```

### 啟用速率限制

```env
# 建議在生產環境啟用
NEXT_PUBLIC_ENABLE_RATE_LIMITER="true"
```

### 啟用內容審查

```env
# 過濾不當內容
ENABLE_CENSORSHIP="true"
```

---

## 🔧 故障排除

### 問題 1: npm install 失敗

```powershell
# 清除快取後重試
npm cache clean --force
rm -rf node_modules
npm install
```

### 問題 2: API 連接失敗

1. 檢查 API 金鑰是否正確
2. 確認網路連接正常
3. 檢查 API 配額是否用盡

### 問題 3: 圖像生成超時

```env
# 使用較快的渲染引擎
RENDERING_ENGINE="REPLICATE"
```

### 問題 4: 中文支援問題

```env
# 使用支援中文的 LLM
LLM_ENGINE="OPENAI"
LLM_OPENAI_API_MODEL="gpt-4-turbo"
```

---

## 📊 費用估算表

| 方案 | LLM | 渲染 | 每次漫畫費用 | 月費估算 (100次) |
|------|-----|------|-------------|-----------------|
| 免費 | HuggingFace | HuggingFace | $0 | $0 |
| 經濟 | Groq | Replicate | ~$0.02 | ~$2 |
| 標準 | OpenAI | Replicate | ~$0.05 | ~$5 |
| 專業 | OpenAI | DALL-E 3 | ~$0.30 | ~$30 |

---

## 🔗 相關資源

### 官方資源
- [官方網站](https://aicomicfactory.app)
- [Hugging Face Space](https://huggingface.co/spaces/jbilcke-hf/ai-comic-factory)
- [作者 Linktree](https://linktr.ee/FLNGR)

### API 文檔
- [Hugging Face Inference API](https://huggingface.co/docs/api-inference/index)
- [OpenAI API](https://platform.openai.com/docs)
- [Replicate API](https://replicate.com/docs)
- [Groq API](https://console.groq.com/docs)
- [Anthropic API](https://docs.anthropic.com/)

### 相關技術
- [Next.js 文檔](https://nextjs.org/docs)
- [Stable Diffusion XL](https://stability.ai/stable-diffusion)
- [TailwindCSS](https://tailwindcss.com/)

---

## 💡 使用技巧

### 1. 編寫有效的提示詞

**好的提示詞範例**:
```
一隻勇敢的小貓咪決定探索神秘的森林，
途中遇到了會說話的蘑菇和迷路的螢火蟲，
最終幫助螢火蟲找到回家的路。
```

**提示詞技巧**:
- ✅ 包含清晰的故事線
- ✅ 描述主要角色
- ✅ 說明場景和情節
- ❌ 避免過於抽象的描述
- ❌ 避免包含不適當內容

### 2. 選擇合適的佈局

- **4 格漫畫**: 適合簡短故事或笑話
- **6 格漫畫**: 適合中等長度故事
- **8 格漫畫**: 適合較複雜的敘事

### 3. 優化生成品質

```env
# 使用 Refiner 模型提升品質
RENDERING_HF_INFERENCE_API_REFINER_MODEL="stabilityai/stable-diffusion-xl-refiner-1.0"
```

---

## 🎉 開始創作

現在您已經了解了 AI Comic Factory 的所有配置和使用方法：

1. ✅ 選擇適合您的 API 方案
2. ✅ 配置環境變數
3. ✅ 運行 `npm run dev`
4. ✅ 訪問 http://localhost:3000
5. ✅ 輸入您的故事，開始創作！

**祝您創作愉快！** 🎨✨
