# 龍蝦雲 Design System

> 記錄整個產品的 UI 設計架構、色彩、字體、組件規範。
> 修改 UI 前必讀此文件。

---

## 一、設計系統總覽

產品共有 **3 套 UI 系統**，各自對應不同受眾與情境：

| # | 系統名稱 | Base 模板 | 對象 | 頁面數 |
|---|----------|-----------|------|--------|
| **A** | Marketing 官網 | `dzx_index.html`（獨立） | 潛在客戶 | 1 頁 |
| **B** | 用戶流程系統 | `system_base.html` | 付費用戶 | 17 頁 |
| **C** | 後台管理系統 | `base.html` | 管理員 | 6 頁 |

---

## 二、系統 A — Marketing 官網

**檔案**：`templates/dzx_index.html`（完全獨立，不繼承任何 base）

### 色彩
| 角色 | Token | Hex |
|------|-------|-----|
| 頁面背景 | `--black` | `#0b0e14` 深藍黑 |
| 卡片背景 | `--dark` / `--card` | `#141820` |
| 邊框 | `--border` | `#1e2433` |
| 主色（CTA） | `--lime` | `#E85542` 橘紅 |
| 輔色 | `--orange` | `#FF6B35` 橙 |
| 輔助文字 | `--gray` | `#8899aa` |

### 字體
```
主字體：'Space Grotesk', 'Noto Sans SC', sans-serif
CDN：fonts.loli.net（國內可用）
字重：300 / 400 / 500 / 600 / 700 / 800 / 900
```

### 特效
- `body::before`：左上角紅色星雲光暈（radial-gradient，rgba(232,85,66,0.10)）
- 捲動行為：`scroll-behavior: smooth`
- Tailwind CSS via CDN（`cdn.tailwindcss.com`）

### 頁面結構
```
Navbar（固定） → Hero → Stats → Skills Ticker → About → Scenarios
→ Features（技能列表） → Pricing → Compare Table → CTA → Footer
```

---

## 三、系統 B — 用戶流程系統

**Base 模板**：`templates/system_base.html`
**樣式檔**：`static/system.css`（Design Token + 組件 Class）
**Tailwind**：CDN + `tailwind.config` 自訂 token

### 色彩 Token（CSS Variables）

```css
/* Backgrounds */
--bg:           #0a0a0a   /* 頁面底色，純黑 */
--surface:      #111111   /* 卡片底色 */
--elevated:     #1a1a1a   /* 懸浮層 */
--overlay:      #222222   /* overlay 層 */

/* Borders */
--border:       #222222
--border-strong:#333333

/* Text */
--text-1:       #fafafa   /* 主文字 */
--text-2:       #a1a1aa   /* 次要文字 */
--text-3:       #52525b   /* 輔助文字 */
--text-4:       #3f3f46   /* placeholder */

/* Accent — 主色 */
--accent:       #ef4444   /* 紅色 */
--accent-hover: #dc2626
--accent-dim:   rgba(239, 68, 68, 0.12)
--accent-ring:  rgba(239, 68, 68, 0.25)

/* Semantic */
--success:      #22c55e   /* 成功/active */
--warning:      #f59e0b   /* 警告 */
--info:         #3b82f6   /* 資訊 */
--danger:       #ef4444   /* 危險（同 accent） */
```

### Tailwind 擴展 Token

```js
colors: {
  'bg':       '#0a0a0a',
  'surface':  '#111111',
  'elevated': '#1a1a1a',
  'border':   '#222222',
  'accent':   '#ef4444',
  'accent-h': '#dc2626',
  't1':       '#fafafa',
  't2':       '#a1a1aa',
  't3':       '#52525b',
}
borderRadius: {
  'sys':    '8px',
  'sys-lg': '12px',
}
```

### 字體

```
主字體：Inter, Noto Sans SC, system-ui, sans-serif
等寬：Menlo, Monaco, Consolas, monospace
CDN：fonts.loli.net（國內可用）
字重：400 / 500 / 600 / 700
基礎字級：14px，行高 1.6
```

### Border Radius 規格

| Token | 值 | 用途 |
|-------|-----|------|
| `--r-sm` | `4px` | code、小型元素 |
| `--r-md` | `8px` | 按鈕、input |
| `--r-lg` | `12px` | 卡片（`s-card`） |
| `--r-xl` | `16px` | 大型 modal |

### Transition 規格

```css
--t-fast: 0.12s ease   /* hover 顏色切換 */
--t-base: 0.2s ease    /* 一般動畫 */
```

### 組件 Class 速查（前綴 `s-`）

#### 卡片
```css
.s-card           /* 標準卡片：surface 背景 + border + r-lg */
```

#### 按鈕
```css
.s-btn            /* 基礎按鈕，需搭配 variant */
.s-btn-primary    /* 紅色實心 CTA */
.s-btn-ghost      /* 透明 + border，次要操作 */
.s-btn-danger     /* 紅色 dim 底，危險操作 */
.s-btn-full       /* width: 100% */
.s-btn-lg         /* 大尺寸 CTA（padding 15px 24px，font 16px） */
```

#### 表單
```css
.s-label          /* 表單標籤（text-2，13px，500） */
.s-input          /* 文字輸入框 */
.s-select         /* 下拉選單 */
.s-textarea       /* 多行文字框 */
.s-hint           /* 輔助說明文字（text-3，12px） */
```

#### 通知 / Flash
```css
.s-flash              /* 基礎 flash 容器 */
.s-flash-error        /* 紅色：#fca5a5 */
.s-flash-success      /* 綠色：#86efac */
.s-flash-warning      /* 黃色：#fcd34d */
.s-flash-info         /* 藍色：#93c5fd */
```

#### Badge
```css
.s-badge          /* 基礎 badge，pill 形 */
.s-badge-green    /* #4ade80 */
.s-badge-red      /* #f87171 */
.s-badge-yellow   /* #fbbf24 */
.s-badge-blue     /* #60a5fa */
.s-badge-purple   /* #c084fc */
.s-badge-gray     /* text-2 色 */
```

#### 其他
```css
.s-back           /* ← 返回連結，text-3 色 */
.s-divider        /* 水平分隔線 */
.s-progress       /* 進度條容器，高 3px */
.s-progress-fill  /* 進度條填充，accent 色 */
.s-section-title  /* 區塊標題，uppercase + letter-spacing */
.mono             /* 等寬字體 + surface 背景 */
```

### 套用頁面清單

| 模板 | 說明 |
|------|------|
| `dzx_purchase.html` | 購買表單（自帶 API Key） |
| `dzx_purchase_proxy.html` | 購買表單（Proxy 代理模式） |
| `dzx_payment.html` | 付款（微信 / USDT IP 分流） |
| `dzx_status.html` | 部署進度 |
| `dzx_qrcode.html` | QR Code 綁定 |
| `dzx_chat.html` | 網頁聊天 |
| `dzx_recharge.html` | AI 餘額充值 |
| `dzx_topup.html` | 充值（Proxy 用戶） |
| `dzx_topup_lookup.html` | 充值查詢 |
| `dzx_bind.html` | 綁定 |
| `dzx_wechat_bind.html` | 微信綁定 |
| `dzx_guide.html` | 使用教程 |
| `dzx_install.html` | 安裝教程 |
| `dzx_faq.html` | 常見問題 |
| `dzx_advanced.html` | 進階功能 |
| `dzx_error.html` | 錯誤頁 |
| `login.html` | 後台登入 |

---

## 四、系統 C — 後台管理系統

**Base 模板**：`templates/base.html`
**樣式**：全部 inline `<style>` 寫在 base.html 內（不依賴外部 CSS 檔）
**Tailwind**：不使用

### 色彩

| 角色 | Hex |
|------|-----|
| 頁面背景 | `#f0f2f8` 淺灰 |
| 主文字 | `#1e293b` 深灰藍 |
| 側邊欄背景 | `#1a1f37` 深藍 |
| 側邊欄文字 | `#a0aec0` 灰 |
| 主色（active） | `#ef4444` 紅（via system.css override） |
| 連結色 | `#6366f1` 靛紫（base 預設） |
| 卡片背景 | `#ffffff` 白 |
| 邊框 | `#e2e8f0` 淺灰 |
| 成功 | `#22c55e` 綠 |
| 危險 | `#ef4444` 紅 |
| 警告 | `#f59e0b` 黃 |

> **注意**：`system.css` 中的 `body.admin-body` 區塊會覆蓋管理後台的主色為紅色 `#ef4444`，與用戶系統一致。

### 佈局結構

```
.app-layout (flex)
├── .sidebar (240px, fixed)
│   ├── .sidebar-brand (Logo + 品牌名)
│   ├── .sidebar-nav (導覽連結)
│   │   └── .sidebar-link [.active]
│   └── .sidebar-footer (版本 + 狀態)
└── .main-area (margin-left: 240px)
    ├── .top-header (64px, sticky)
    │   ├── .page-title
    │   ├── .header-search
    │   └── .header-avatar
    └── .container (max-width: 1320px, padding: 24px 32px)
```

### 字體

```
主字體：Inter, -apple-system, BlinkMacSystemFont, "Segoe UI", "PingFang SC", "Microsoft YaHei"
等寬：Menlo, monospace
基礎字級：14px，行高 1.6
```

### 套用頁面清單

| 模板 | 說明 |
|------|------|
| `orders.html` | 訂單列表 |
| `order_detail.html` | 訂單詳情 |
| `order_create.html` | 新建訂單 |
| `billing.html` | 今日帳單 |
| `quota.html` | AWS 配額監控 |
| `proxy_stats.html` | DeepSeek 餘額監控 |

---

## 五、三套系統差異對照

| 維度 | A Marketing | B 用戶流程 | C 後台管理 |
|------|-------------|------------|------------|
| **主題** | 暗色 | 暗色 | 淺色 |
| **背景色** | `#0b0e14` 深藍黑 | `#0a0a0a` 純黑 | `#f0f2f8` 淺灰 |
| **主色** | `#E85542` 橘紅 | `#ef4444` 正紅 | `#ef4444` 紅（override）|
| **主字體** | Space Grotesk | Inter | Inter |
| **卡片** | 自定義 inline | `.s-card` | `.card` inline |
| **CSS 方案** | Tailwind + inline | Tailwind + system.css | 全 inline |
| **按鈕 class** | Tailwind utility | `.s-btn-*` | `.btn-*` |

---

## 六、已知設計問題 & 修復記錄

| 問題 | 影響頁面 | 修復方式 | 狀態 |
|------|----------|----------|------|
| 「推荐」badge 佔用卡片內部空間，導致三張價格卡高度不一、金額不對齊 | `dzx_purchase_proxy.html`、`dzx_topup.html` | badge 改用 `position: absolute; top: -11px` 浮在框線上；card 加 `display: flex; min-height: 120px` 等高 | ✅ 已修（v1.4.2） |

---

## 七、新增 UI 規範

### 開發新頁面時

1. **用戶端頁面** → 繼承 `system_base.html`，優先用 `s-*` class + `system.css` token
2. **管理端頁面** → 繼承 `base.html`，跟隨現有 `.btn-*` / `.card` / `.table` 慣例
3. **Landing 擴充** → 修改 `dzx_index.html`，維持太空暗色主題

### 色彩使用原則

- 主要操作（CTA）→ `--accent` (`#ef4444`)
- 成功 / active → `--success` (`#22c55e`)
- 警告 / 即將到期 → `--warning` (`#f59e0b`)
- 錯誤 / 危險 → `--danger` (`#ef4444`)
- 次要文字 → `--text-2` / `--text-3`

### Floating Badge 規範（價格卡等）

需要在卡片邊框上方放 badge（如「推荐」「省」），統一使用：

```css
.your-card { position: relative; }
.your-badge {
  position: absolute;
  top: -11px;
  left: 50%;
  transform: translateX(-50%);
  white-space: nowrap;
  /* 色彩依情境 */
}
```

> 詳細規格見 SPEC.md。截圖見 `screenshots/`。

---

*最後更新：2026-03-19*
