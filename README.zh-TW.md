# Awesome Harness Engineering [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> 精選的文章、實戰手冊、基準測試、規格與開源專案清單，主題聚焦於 harness engineering：形塑 AI agent 周邊環境的實踐，讓 agent 能穩定可靠地工作。

*[English](./README.md) | 繁體中文*

Harness engineering 位於 context engineering、評估（evaluation）、可觀測性（observability）、編排（orchestration）、安全自主（safe autonomy）與軟體架構的交會處。本清單專注於能讓 agent 在真實工作流程中更可靠的資源，尤其是長時間執行的程式撰寫與研究任務。

通用的 agent 工具不在收錄範圍內，除非該頁面直接談到 harness 設計、context 管理、評估、執行期控制，或其他攸關可靠性的 harness 基礎元件。

## 目錄 (Contents)

- [課程與學習資源 (Courses & Learning Resources)](#課程與學習資源-courses--learning-resources)
- [基礎 (Foundations)](#基礎-foundations)
- [Context、記憶與工作狀態 (Context, Memory & Working State)](#context記憶與工作狀態-context-memory--working-state)
- [約束、護欄與安全自主 (Constraints, Guardrails & Safe Autonomy)](#約束護欄與安全自主-constraints-guardrails--safe-autonomy)
- [規格、Agent 檔案與工作流程設計 (Specs, Agent Files & Workflow Design)](#規格agent-檔案與工作流程設計-specs-agent-files--workflow-design)
- [評估與可觀測性 (Evals & Observability)](#評估與可觀測性-evals--observability)
- [基準測試 (Benchmarks)](#基準測試-benchmarks)
- [執行環境、Harness 與參考實作 (Runtimes, Harnesses & Reference Implementations)](#執行環境harness-與參考實作-runtimes-harnesses--reference-implementations)
- [貢獻指南 (Contributing)](#貢獻指南-contributing)
- [授權 (License)](#授權-license)

## 課程與學習資源 (Courses & Learning Resources)

- [walkinglabs/learn-harness-engineering](https://github.com/walkinglabs/learn-harness-engineering) - 以專案為導向的課程儲存庫，教你如何讓 Codex 與 Claude Code 更可靠；以一個 Electron 個人知識庫應用為主軸，附有講義、範例產出物與實作型 harness 專案。

## 基礎 (Foundations)

- [Harness engineering: leveraging Codex in an agent-first world](https://openai.com/index/harness-engineering/) - OpenAI 的旗艦級實戰報告，說明如何運用架構約束、repo 內建指令、瀏覽器驗證與遙測，以 Codex 打造大型應用。
- [Effective harnesses for long-running agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents) - Anthropic 的核心文章，討論 initializer agent、功能清單、`init.sh`、自我驗證，以及跨多個 context window 的交接產出物。
- [Harness design for long-running application development](https://www.anthropic.com/engineering/harness-design-long-running-apps) - Anthropic 的後續文章，聚焦以更好的任務狀態與評估器設計來改善長時間執行的應用生成。
- [The Anatomy of an Agent Harness](https://blog.langchain.com/the-anatomy-of-an-agent-harness/) - LangChain 精要地把 agent 拆解為「模型 + harness」，涵蓋 prompt、工具、middleware、編排與執行期基礎設施。
- [Harness Engineering](https://martinfowler.com/articles/exploring-gen-ai/harness-engineering.html) - Thoughtworks 將 harness 工作拆成 context engineering、架構約束，以及對抗系統熵的「垃圾回收」。
- [Building effective agents](https://www.anthropic.com/engineering/building-effective-agents) - Anthropic 更廣泛的指南，談工作流程、agent、工具，以及何時結構化系統會勝過單純 prompting。
- [Skill Issue: Harness Engineering for Coding Agents](https://www.humanlayer.dev/blog/skill-issue-harness-engineering-for-coding-agents) - 務實地論證：coding agent 表現不佳，往往是 harness 問題而非模型問題。
- [Your Agent Needs a Harness, Not a Framework](https://www.inngest.com/blog/your-agent-needs-a-harness-not-a-framework) - Inngest 主張應把狀態、重試、追蹤與並行視為第一級基礎設施。
- [Greenfield AI, Brownfield AI, and the Vibecode You Just Inherited](https://sawinyh.com/blog/greenfield-vs-brownfield-ai-codebases) - 把 agent 會遇到的程式庫分成三類——agent 原生的全新專案、真正的老舊系統，以及剛被 vibecode 出來的繼承專案——並提供實戰手冊：分層 `CLAUDE.md` 規則、逐步收緊的 pre-commit hook、建立 lint 違規基準線、以功能資料夾重構，讓程式庫本身不再是 harness 的瓶頸。
- [Harness Engineering for Language Agents: The Harness Layer as Control, Agency, and Runtime](https://www.preprints.org/manuscript/202603.1756) - 一篇立場論文，將 harness 層視為第一級研究對象，提出 **control–agency–runtime (CAR)** 分解框架，並引入 **HarnessCard** 作為 harness 設計與評估的結構化報告格式。
- [Many Hands Engineering](https://github.com/mseeks/many-hands-engineering/blob/main/many-hands-engineering.pdf) - 一本探討「單一 agent harness 之上那一層」的手冊：多個受 harness 約束的 agent 如何共享公共資源、決策該落在「計畫性／自發性」光譜的何處，以及人類治理如何以不同於 agent 執行的節奏運作。它把 harness engineering 視為框架賴以立足的關鍵「地形」層。

## Context、記憶與工作狀態 (Context, Memory & Working State)

- [Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) - Anthropic 指出應把 context window 當成有預算的工作記憶來管理，而不是資料傾倒場。
- [Context Engineering for AI Agents: Lessons from Building Manus](https://manus.im/blog/Context-Engineering-for-AI-Agents-Lessons-from-Building-Manus) - Manus 的詳盡實戰手冊，談 KV-cache 區域性、工具遮罩、以檔案系統當記憶，以及把有價值的失敗留在 context 中。
- [Context Engineering for Coding Agents](https://martinfowler.com/articles/exploring-gen-ai/context-engineering-coding-agents.html) - Thoughtworks 指導如何形塑任務環境，讓 coding agent 保持有據可依且高產出。
- [Advanced Context Engineering for Coding Agents](https://www.humanlayer.dev/blog/advanced-context-engineering) - HumanLayer 的模式，用於降低 context 漂移並讓 coding session 更容易接續。
- [Context-Efficient Backpressure for Coding Agents](https://www.humanlayer.dev/blog/context-efficient-backpressure) - HumanLayer 的想法，防止 agent 把 context 燒在雜訊或低價值工作上。
- [OpenHands Context Condensensation for More Efficient AI Agents](https://openhands.dev/blog/openhands-context-condensensation-for-more-efficient-ai-agents) - OpenHands 設計的有界對話記憶，保留目標、進度、關鍵檔案與失敗測試，同時維持長時間 coding session 的效率。
- [Writing a good CLAUDE.md](https://www.humanlayer.dev/blog/writing-a-good-claude-md) - 務實指南，教你撰寫耐用、放在 repo 內、agent 能反覆遵循的指令。

## 約束、護欄與安全自主 (Constraints, Guardrails & Safe Autonomy)

- [Beyond permission prompts: making Claude Code more secure and autonomous](https://www.anthropic.com/engineering/claude-code-sandboxing) - Anthropic 談如何用更好的沙箱與政策設計，在不失去控制的前提下減少核准流程的摩擦。
- [Code execution with MCP: building more efficient agents](https://www.anthropic.com/engineering/code-execution-with-mcp) - Anthropic 的做法：透過明確、可檢視的工具邊界，賦予 agent 受控的執行能力。
- [Writing effective tools for agents](https://www.anthropic.com/engineering/writing-tools-for-agents) - Anthropic 指導如何設計讓模型更容易正確且安全呼叫的工具介面。
- [Mitigating Prompt Injection Attacks in Software Agents](https://openhands.dev/blog/mitigating-prompt-injection-attacks-in-software-agents) - OpenHands 的實務指南，用確認模式、分析器、沙箱與硬性政策降低自主 coding agent 的 prompt injection 風險。
- [Assessing internal quality while coding with an agent](https://martinfowler.com/articles/exploring-gen-ai/ccmenu-quality.html) - Thoughtworks 談如何把品質檢查移進迴圈內，而不是事後靠人工審查。
- [Anchoring AI to a reference application](https://martinfowler.com/articles/exploring-gen-ai/anchoring-to-reference.html) - Thoughtworks 談以具體範例來約束 agent，使其產出更一致。
- [Humans and Agents in Software Engineering Loops](https://martinfowler.com/articles/exploring-gen-ai/humans-and-agents.html) - 一套清晰的心智模型，說明人類該在何處強化 harness，而不是逐項微管理每個產出物。
- [Claude Code: Best practices for agentic coding](https://code.claude.com/docs) - Anthropic 對 repo 結構、檢查點、驗證與委派的實務建議，適用於 agentic coding 工作流程。
- [Lurkr](https://github.com/agentveil-protocol/lurkr) - 在部署前於 CI 執行的靜態掃描器，用來揭露 AI agent 的能力風險，包括影子能力、憑證流入 LLM context、`@tool` 中的 eval/subprocess、直接的 prompt 字串插值，以及未經驗證的 MCP 端點。

## 規格、Agent 檔案與工作流程設計 (Specs, Agent Files & Workflow Design)

- [AGENTS.md](https://github.com/agentsmd/agents.md) - 輕量的開放格式，用於撰寫 repo 內建指令，告訴 agent 該如何在該程式庫中工作。
- [agent.md](https://github.com/agentmd/agent.md) - 相關的標準化嘗試，目標是跨專案與工具的機器可讀 agent 指令。
- [GitHub Spec Kit](https://github.com/github/spec-kit) - GitHub 的規格驅動開發工具組，適合讓 agent 依明確的產品與工程規格執行。
- [Understanding Spec-Driven-Development: Kiro, spec-kit, and Tessl](https://martinfowler.com/articles/exploring-gen-ai/sdd-3-tools.html) - Thoughtworks 說明為何紮實的規格能讓 AI 輔助的軟體交付更可靠。
- [12 Factor Agents](https://www.humanlayer.dev/blog/12-factor-agents) - HumanLayer 的正式環境 agent 運作原則，包括明確的 prompt、狀態所有權，以及乾淨的暫停／恢復行為。
- [12-Factor AgentOps](https://www.12factoragentops.com/) - 偏維運視角的姊妹作，聚焦 context 紀律、驗證與可重現的 agent 工作流程。

## 評估與可觀測性 (Evals & Observability)

- [Testing Agent Skills Systematically with Evals](https://developers.openai.com/blog/eval-skills/) - OpenAI 的具體指南，教你用 JSONL 日誌與確定性檢查把 agent trace 轉成可重複的評估。
- [How to Evaluate Agent Skills (And Why You Should)](https://openhands.dev/blog/evaluating-agent-skills) - OpenHands 的動手實戰手冊，以有界任務、確定性驗證器、無 skill 基準線與 trace 審查，衡量某個 skill 是否真的有幫助。
- [Agent evals](https://platform.openai.com/docs/guides/agent-evals) - OpenAI 的產品指南，以可重現的任務層級與工作流程層級評估來衡量 agent 品質。
- [Evaluation best practices](https://platform.openai.com/docs/guides/evaluation-best-practices) - OpenAI 的通用指南，教你建立貼近真實分布並能及早捕捉退步的評估套件。
- [Trace grading](https://platform.openai.com/docs/guides/trace-grading) - OpenAI 說明如何直接為 agent trace 評分，對長篇多步驟任務特別有用。
- [Inspect AI](https://inspect.aisi.org.uk/) - 英國 AISI 的開源評估框架，提供 solver、scorer、沙箱、工具使用、MCP 與日誌檢視器等基礎元件，可用來打造可重現的 agent 評估 harness。
- [OpenTelemetry Semantic Conventions for Generative AI Systems](https://opentelemetry.io/docs/specs/semconv/gen-ai/) - 為 LLM 與 agent 工作流程建立埋點的標準 span、metric、event 與屬性慣例，讓 harness trace 能在各種可觀測性後端之間保持可攜。
- [AgentOps](https://github.com/AgentOps-AI/agentops) - 開源 Python SDK，支援 agent 監控、session 重播、成本追蹤、基準測試與追蹤，涵蓋常見的 LLM 與 agent 框架。
- [agenttrace](https://github.com/luoyuctl/agenttrace) - 本地優先的 TUI/CLI，用於稽核 AI coding agent 的 session trace、健康門檻、成本尖峰、工具失敗、延遲缺口，以及各次嘗試之間的差異。
- [Learning to Verify AI-Generated Code](https://openhands.dev/blog/20260305-learning-to-verify-ai-generated-code) - OpenHands 概述一套分層驗證堆疊，以正式環境 trace 訓練的軌跡評審器進行重排序、提早停止與審查時的品質控管。
- [Demystifying Evals for AI Agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents) - Anthropic 指導：當 agent 通往成功或失敗的軌跡有很多種時，究竟該衡量什麼。
- [Quantifying infrastructure noise in agentic coding evals](https://www.anthropic.com/engineering/infrastructure-noise) - Anthropic 說明執行期設定造成的分數變動，可能比排行榜上多數的名次差距還大。
- [Evaluating Deep Agents: Our Learnings](https://blog.langchain.com/evaluating-deep-agents-our-learnings/) - LangChain 務實拆解有狀態 agent 的單步、整段執行與多輪評估設計。
- [Improving Deep Agents with harness engineering](https://blog.langchain.com/improving-deep-agents-with-harness-engineering/) - LangChain 提出證據：光是調整 harness 就能顯著提升基準測試表現。

## 基準測試 (Benchmarks)

當你想比較的是 harness 品質而非僅僅模型品質時，這些基準測試特別有用。它們會對 context 處理、工具呼叫、環境控制、驗證邏輯，以及模型周邊的執行期骨架施加壓力。

- [Agent Arena](https://www.agent-arena.com/leaderboard) - 以 ELO 式評分與兩兩對戰結果排名 AI agent、模型、工具與框架的排行榜，提供跨類別比較 harness 層級選擇的結構化方式。
- [AgentBench](https://github.com/THUDM/AgentBench) - 跨環境基準測試，涵蓋作業系統、資料庫、知識圖譜、網頁瀏覽等，可用來檢視 harness 是否能推廣到單一狹窄任務迴圈之外。
- [AgentBoard](https://github.com/HKUST-NLP/AgentBoard) - 針對多輪 LLM agent 的基準測試，並搭配分析型評估面板，讓評估超越最終成功率，使部分進度與軌跡品質可見。
- [AgentStudio](https://github.com/SkyworkAI/agent-studio) - 整合式基準套件，提供貼近真實的環境與完整工具組，用於在真實電腦軟體上評估虛擬 agent，適合衡量 harness 在廣泛任務面上的深度。
- [AppWorld](https://appworld.dev/) - 由應用程式與人物構成、可控制的世界，用於對互動式 coding agent 做基準測試；具備基於狀態與基於執行的單元測試，能凸顯 harness 在規劃、程式生成與附帶損害控制上的品質。
- [AssistantBench](https://github.com/oriyor/AssistantBench) - 以貼近真實、耗時的研究任務評估網頁 agent，需要多步驟工具使用與資訊綜合，是長期任務網頁情境中 harness 品質的良好代理指標。
- [BrowseComp](https://www.kaggle.com/benchmarks/openai/browsecomp) - 評估 AI agent 找出難以尋得資訊的能力，在困難條件下對搜尋策略、context 管理與檢索 harness 設計施加壓力。
- [BrowserGym Leaderboard](https://huggingface.co/spaces/ServiceNow/browsergym-leaderboard) - 用於評估 LLM、VLM 與 agent 網頁導航任務的 gym 環境與排行榜，提供可重現的框架，在單一處比較多個網頁基準測試上的 harness 表現。
- [CharacterEval](https://github.com/morecry/CharacterEval) - 以多輪對話與角色設定評估角色扮演對話 agent 的基準測試，指標涵蓋四個面向，包括角色忠實度與對話連貫性。
- [ClawBench](https://clawbench.net) - 在搜尋、推理、程式撰寫、安全性與多輪對話任務上評估 AI agent 的基準測試，以單一套件涵蓋 harness 面對的各種需求。
- [ClawBench: Can AI Agents Complete Everyday Online Tasks?](https://huggingface.co/papers/2604.08523) - 瀏覽器 agent 基準測試，涵蓋 15 個類別、144 個線上正式網站上的 153 項日常網頁任務；使用輕量攔截層，只捕捉並阻擋最終送出的請求，讓 agent 能在真實網站上完成端到端評分而不產生真實世界的副作用。
- [ClawWork](https://github.com/HKUDS/ClawWork) - 真實世界的經濟型基準測試，AI agent 需完成橫跨 44 種職業的專業任務、賺取收入，同時管理 token 成本與經濟償付能力，可直接檢驗資源約束下的 harness 效率。
- [Computer Agent Arena](https://github.com/xlang-ai/computer-agent-arena) - 開放評估平台，讓使用者在真實電腦任務上比較基於 LLM/VLM 的 agent，任務從一般電腦操作到程式撰寫、資料分析與影片剪輯，能在廣泛任務面上凸顯 harness 差異。
- [EvoClaw: Evaluating AI Agents on Continuous Software Evolution](https://openhands.dev/blog/evoclaw-benchmark) - 一篇基準測試說明文，以真實 repo 歷史中彼此相依的里程碑序列評估 agent，凸顯退步累積與長期任務中的精確度流失。
- [GAIA](https://huggingface.co/datasets/gaia-benchmark/GAIA) - 通用 AI 助理的基準測試，常用來比較在工具、規劃、驗證與長期自主性上的 harness 層級選擇。
- [Galileo Agent Leaderboard](https://huggingface.co/spaces/galileo-ai/agent-leaderboard) - 開放評估平台，追蹤 LLM agent 在各商業領域的任務完成度與工具呼叫表現，適合比較企業級 agentic 情境下的 harness 品質。
- [GTA](https://github.com/open-compass/GTA) - 以人工撰寫的查詢、真實部署的工具與真正的多模態輸入評估 LLM agent 的工具使用能力，揭露孤立測試與真實部署之間的 harness 落差。
- [HAL: Holistic Agent Leaderboard](https://hal.cs.princeton.edu/) - 針對 agent 系統的基準測試與排行榜，重視可靠性、成本與廣泛任務覆蓋，適合比較端到端的 harness 行為。
- [Introducing Terminal-Bench 2.0 and Harbor](https://www.tbench.ai/news/announcement-2-0) - Terminal-Bench 2.0 的發布公告，有助於理解更困難的任務，以及 Harbor 背後的通用化評估 harness。
- [LeetCode-Hard Gym](https://github.com/GammaTauAI/leetcode-hard-gym) - 對接 LeetCode 提交伺服器的 RL 環境介面，用於評估程式生成 agent，讓 harness 能直接取得困難演算法題目上基於執行的回饋。
- [LLM Colosseum Leaderboard](https://github.com/OpenGenerativeAI/llm-colosseum) - 讓 LLM 在《快打旋風 III》中互相對戰的評估平台，測試速度、適應性與即時決策，作為緊湊延遲約束下 harness 反應能力的代理指標。
- [MAgIC](https://zhiyuanhubj.github.io/MAgIC/) - 衡量 LLM 在多 agent 系統中的認知、適應性、理性與協作能力的基準測試，適合評估 harness 如何協調 agent 互動與共享狀態。
- [MCP Bench](https://github.com/modelscope/MCPBench) - 評估 AI 模型與 MCP 伺服器互動的基準測試，衡量各類伺服器上的工具準確度、延遲與 token 使用量，直接反映 harness 在 MCP 整合上的設計選擇。
- [MCP Universe](https://mcp-universe.github.io/) - 比較 AI 模型在 MCP 任務上表現的排行榜，追蹤不同模型與 harness 設定如何處理工具增強型 agent 工作流程。
- [MCPMark](https://github.com/eval-sys/mcpmark) - 壓力測試型基準測試，針對 Notion、GitHub、Postgres 等工具上的真實 MCP 任務檢驗模型與 agent 能力，讓 harness 的 MCP 整合品質可被直接量測。
- [Olas Predict Benchmark](https://github.com/valory-xyz/olas-predict-benchmark) - 以歷史預測市場資料評估 agent 的基準測試，檢驗長期推理任務中研究、檢索與預測的 harness 設計。
- [OSWorld](https://os-world.github.io/) - 真實電腦操作基準測試，橫跨 Ubuntu、Windows 與 macOS 共 369 項任務，含初始狀態設定與基於執行的評估器，非常適合測試桌面與多模態 harness。
- [OSWorld-MCP](https://osworld-mcp.github.io) - OSWorld 的延伸版本，以 Model Context Protocol 評估 AI agent 在真實電腦任務上的表現，適合在貼近真實的桌面任務套件上比較支援 MCP 的 harness。
- [SEC-bench](https://github.com/SEC-bench/SEC-bench) - 評估 LLM agent 處理真實軟體安全任務（含漏洞重現與修補）的基準測試，對程式執行、容器化環境與安全導向工具的 harness 設計施加壓力。
- [SWE-bench Verified](https://www.swebench.com/) - 強力的軟體工程 agent 基準測試，任務取自真實 GitHub issue 與測試，讓 harness 在檢索、修補與驗證上的選擇高度可見。
- [τ-Bench](https://github.com/sierra-research/tau-bench) - 模擬使用者與具備領域專屬 API 工具及政策準則的語言 agent 之間的動態對話，適合評估圍繞結構化工具使用與政策執行所建立的 harness。
- [tau2-bench](https://github.com/sierra-research/tau2-bench) - 針對貼近真實的多步驟 agent 任務的基準測試，成敗取決於工具使用與執行品質，而非單次作答。
- [Terminal-Bench](https://www.tbench.ai/) - 針對終端機原生 agent 的基準套件，環境涵蓋 shell、檔案系統與大量驗證需求，特別適合比較 coding agent 的 harness。
- [TravelPlanner](https://github.com/OSU-NLP-Group/TravelPlanner) - 評估 LLM agent 在多重約束下進行工具使用與複雜規劃的基準測試，揭示 harness 設計如何處理多約束滿足與長期規劃。
- [VAB](https://github.com/THUDM/VisualAgentBench) - VisualAgentBench 將大型多模態模型當作視覺基礎 agent 評估，任務涵蓋具身、GUI 與視覺設計，適合比較 harness 在視覺為本的多步驟 agent 工作流程上的表現。
- [VisualWebArena](https://jykoh.com/vwa) - 針對多模態網頁 agent、貼近真實且以視覺為基礎的任務基準測試，在 WebArena 之上加入圖片與截圖輸入，考驗 harness 對瀏覽器環境中視覺 context 的支援。
- [WebArena](https://webarena.dev/) - 獨立、可自架的網頁環境，用於評估自主 agent 執行貼近真實的任務，是比較面向網頁的 harness 設計時可重現的基準線。
- [WebArena-Verified](https://github.com/ServiceNow/webarena-verified) - 經過驗證的網頁 agent 基準測試，具備精選任務以及針對 agent 回應與擷取到的網路 trace 的確定性評估器，非常適合量測面向網頁的 harness。
- [WildClawBench](https://github.com/InternLM/WildClawBench) - 在真實環境中執行的基準測試，於實際運行的 OpenClaw 環境內對 agent 執行 60 項原創任務，含多模態、長期任務與安全關鍵情境，讓 harness 在真實條件下的韌性直接可見。
- [WorkArena](https://github.com/ServiceNow/WorkArena) - 針對瀏覽器 agent 執行常見知識工作任務的基準測試，適合在貼近真實的企業型網頁工作流程（而非玩具型瀏覽器任務）上比較 harness。

## 執行環境、Harness 與參考實作 (Runtimes, Harnesses & Reference Implementations)

- [HEAAL](https://github.com/hyun06000/AIL) - 透過 AIL（AI-Intent Language）為 AI agent 提供以文法強制執行的安全約束。

- [Agent Frameworks, Runtimes, and Harnesses, Oh My!](https://blog.langchain.com/agent-frameworks-runtimes-and-harnesses-oh-my/) - LangChain 拆解哪些東西該屬於框架、執行環境與 harness。
- [Building agents with the Claude Agent SDK](https://claude.com/blog/building-agents-with-the-claude-agent-sdk) - Anthropic 介紹面向正式環境的 agent SDK，支援 session、工具與編排。
- [How we built our multi-agent research system](https://www.anthropic.com/engineering/multi-agent-research-system) - Anthropic 的架構說明文，描述一套角色分離、協調結構化的多 agent 系統。
- [deepagents](https://github.com/langchain-ai/deepagents) - LangChain 的開源專案，用 middleware 與 harness 模式打造更深層、能長時間執行的 agent。
- [SWE-agent](https://github.com/SWE-agent/SWE-agent) - 成熟的研究型 coding agent，讓 harness、prompt、工具與環境設計都可直接檢視。
- [SWE-ReX](https://github.com/SWE-agent/SWE-ReX) - 為 AI agent 打造的沙箱化程式執行基礎設施，適合當 harness 工作開始與執行期環境設計交融時使用。
- [AgentKit](https://github.com/inngest/agent-kit) - Inngest 的 TypeScript 工具組，在事件驅動基礎設施之上打造耐久、具工作流程意識的 agent。
- [browser-use/browser-harness](https://github.com/browser-use/browser-harness) - 基於 CDP 的輕薄瀏覽器 harness，讓 agent 能在執行期擴充輔助函式，適合檢視具自我修復能力的網頁任務工作流程。
- [Citadel](https://github.com/SethGammon/Citadel) - 針對 Claude Code 與 OpenAI Codex 的 harness，提供隔離的 worktree、多 agent 協調，以及持久化的記憶與戰役狀態。
- [Bring Your AI MCP](https://github.com/unitedideas/bringyour-mcp) - 公開的 harness 遷移參考，涵蓋 Claude Code 遷往 Codex 的流程，附可安裝的稽核產出物，以及對 hook、MCP 設定與指令檔差異的明確驗證說明。
- [Harbor](https://github.com/harbor-framework/harbor) - 通用化的 harness，用於大規模評估與改進 agent，與 Terminal-Bench 2.0 一同發布。
- [Harness Evolver](https://github.com/raphaelchristi/harness-evolver) - Claude Code 外掛，以多 agent 提案者、LangSmith 支援的評估與 git worktree 隔離，自主演化 LLM agent harness。基於 Meta-Harness（Lee et al., 2026）。
- [Ralph Wiggum as a Software Engineer](https://ghuntley.com/ralph/) - Geoffrey Huntley 記錄的「Ralph」：一種極簡的 `while :; do cat PROMPT.md | claude-code; done` harness 模式，以單一任務迴圈、確定性的 prompt 堆疊與有界的 subagent 並行度，驅動長時間的自主程式撰寫。
- [skills.sh](https://skills.sh) - 社群市集，用於發掘、分享與安裝可重複使用的 AI agent skill，橫跨 Claude Code 與 OpenClaw 等執行環境，讓 harness 能力可攜且可組合。
- [Uni-CLI](https://github.com/olo-dot-io/Uni-CLI) - 通用 CLI 樞紐，透過 711 條宣告式 YAML pipeline 將 agent 連接到 134 個網站與桌面應用。內建 8 階段 Karpathy 式自我修復迴圈、附起始目錄的評估 harness、每次呼叫的成本帳本、寫死的敏感路徑拒絕清單，以及可為每個 adapter 自動註冊一個 MCP 工具的 `unicli mcp serve`。每次呼叫約 80 個 token。

## 貢獻指南 (Contributing)

歡迎貢獻。請優先提供符合以下條件的資源：

- 明確說明 agent 如何被約束、評估、恢復、觀測或編排
- 原創實作、第一手來源文章，或高訊號量的技術說明文
- 對實際打造 harness 的實務工作者有用，而非泛泛的 AI 評論

若兩個連結講的是同一件事，請優先選擇更第一手、更務實、更偏向實作導向的那一個。

貢獻準則與建議的條目格式，請見 [CONTRIBUTING.md](./CONTRIBUTING.md)。

## 授權 (License)

[CC0 1.0](./LICENSE)
