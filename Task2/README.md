# 600683.SH 历史行情数据与技术指标诊断看板

本项目为 **北京大学量化交易课 Task 1** 的归档项目。项目完成了对股票 **京投发展 (600683.SH)** 自 2025 年 1 月 2 日至 2026 年 7 月 3 日共计 **362 个交易日** 历史行情数据的多源校验对齐、描述性统计学诊断、四大核心技术指标（RSI, MACD, Bollinger Bands, DMI/ADX）的精确递推计算，并提供了一个交互式的 GitHub Pages 展示面板。

---

## 📂 项目结构

*   `600683_SH_daily.csv`：清洗并格式化后的原始日线数据（包含前复权价与未复权价）。
*   `600683_SH_indicators_computed.csv`：计算了四大技术指标（DIF, DEA, HIST, MB, UP, DN, RSI, DI+, DI-, ADX）后的宽表数据。
*   `600683_SH_indicators_chart.png`：由 Matplotlib 绘制的 300 DPI 四面板行情技术看板。
*   `verification_results.txt`：Tushare 经典版接口与 Yahoo Finance 的双源对齐核对报告。
*   `600683_SH_Technical_Diagnostic_Report.pdf`：排版严谨、包含 LaTeX 级公式框及参数披露的学术级 PDF 报告。
*   `index.html`：本项目专用的极客风 GitHub 面板主页（基于 Tailwind CSS 响应式设计）。

---

## 🚀 部署您的 GitHub Pages 分享面板

要将本项目作为类似 [xuema.github.io/ai_quant](https://xuema.github.io/ai_quant/) 的在线看板分享给他人，只需以下 3 步：

### 第一步：新建 GitHub 仓库
1. 登录您的 GitHub 账号，点击右上角 `New` 新建仓库；
2. 命名您的仓库（如 `600683_technical_diagnostic`），设为 **Public (公开)**，勾选 `Add a README file`，然后点击创建。

### 第二步：上传项目文件
1. 在新建的仓库页面中，点击 `Add file` -> `Upload files`；
2. 将本地 `/Users/demerzel/Desktop/北大量化交易课/Task 1/` 目录下的所有文件（**特别是 `index.html` 和 `600683_SH_indicators_chart.png`**）拖入浏览器中并提交 commit。

### 第三步：激活 GitHub Pages
1. 进入该 GitHub 仓库的 `Settings` (设置) 页面；
2. 在左侧菜单栏中点击 `Pages`；
3. 在 **Build and deployment** 下的 Build source 选择 `Deploy from a branch`；
4. 在 **Branch** 下选择 `main` (或 `master`) 分支，目录选择 `/ (root)`，点击 `Save`；
5. 等待 1~2 分钟，页面上方将会出现您的 live 专属在线分享链接（如 `https://<您的用户名>.github.io/600683_technical_diagnostic/`）！

---

## 📈 核心指标参数设置规范

为了保证量化回测的重现性，本看板图表严格执行了以下技术指标参数设置：

1.  **相对强弱指标 (RSI)**：
    *   时间周期 = `14 日`，超买阈值 = `70`，超卖阈值 = `30`，强弱临界点 = `50`。
2.  **平滑异同移动平均线 (MACD)**：
    *   快速 EMA 周期 = `12 日`，慢速 EMA 周期 = `26 日`，信号线 DEA EMA 周期 = `9 日`（直方图计算采用中国市场标准两倍差值法）。
3.  **布林带 (Bollinger Bands)**：
    *   中轨简单均线周期 = `20 日`，包络宽度滚动标准差倍数 K = `2.0`（95.44% 双侧置信度）。
4.  **趋向指标 (DMI & ADX)**：
    *   趋向平滑周期 = `14 日`，ADX 趋势强弱临界线 = `20`，单边高能量动能触发线 = `26`。

---

## 💡 深度量化分析结论

*   **右偏震荡格局**：该股均值（6.15元）远高于中位数（4.26元），表明有超过 60% 的时间在 5 元以下磨底积聚筹码。针对此特征，应在策略中配置 **自适应动态止损** 或 **唐奇安通道突破** 过滤器。
*   **高波动与封板倾向**：日波动率标准差达 3.55%，存在极端封板行为。在交易执行端，回测时必须加入 **硬滑点限制** 以预防流动性枯竭带来的滑点失真。
*   **流动性爆发现象**：成交量爆发时是清淡期的 8.9 倍，属于典型资金/情绪驱动型标的。应用 **DMI & ADX 指标** 能够极为完美地在 ADX < 20 时屏蔽横盘无序磨损，在 ADX > 26 时精准捕捉单边拉升大主升浪。
