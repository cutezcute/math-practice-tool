# math-practice-tool
# ⛏️ Math with Ore · Supplementary Practice Tool

==============================================

A purely local HTML supplementary practice tool. Simply **double-click `index.html`**​ to use — **no internet required, no data uploaded anywhere**.

Current Question Banks (in `data/` directory)

---------------------------------------------

**① 5·3 Daily Practice Autumn 2026 · Grade 5 Semester 1 · Math · Beijing Normal Univ. Edition (BSD)**, total **70 papers**:

| Group                | Count | Source                                                |
| -------------------- | ----- | ----------------------------------------------------- |
| Lesson Exercises     | 51    | `53天练5年级上2026版.pdf` p6–p107 (2 pages per lesson)      |
| Comprehensive Review | 1     | Main book p108–p113, end-of-term comprehensive review |
| Assessment Papers    | 10    | `测评卷(大字版及答案).pdf` p2–p41 (4 pages per paper)          |
| Thinking Training    | 8     | `思维训练及答案.pdf` p3–p18 (2 pages per topic)              |

**② 2026 Autumn Edition Synchronized New Question Bank · Grade 5 Semester 1 Math (Beijing Normal Univ. Edition)**, total **12 chapters, 240 questions**​ (`data/catalog_2026_g5a.js`):

- Table of contents follows the 2026 autumn textbook: 8 units + 2 comprehensive projects + "Fun with Math" (Chicken-and-Rabbit Problem) + general review.

- 20 questions per chapter, mixed difficulty: **Basic 40% ⭐ / Intermediate 40% ⭐⭐ / Hard 20% ⭐⭐⭐**.

- All are **text-structured questions**​ with auto-grading, two-level hints, and per-question explanations.

### Questions and Answers Are Separated

All 4 PDFs are **scanned images without a text layer**, so formulas and answer text cannot be auto-recognized. The handling method:

1. Each page was rendered as a JPEG and placed into two independent directories by purpose:
- `data/pages/q/` → **question pages**​ (164 images), displayed during practice

- `data/pages/a/` → **answer pages**​ (48 images), collapsed by default, expanded only when clicking "📖 View Answer"
2. Pairing was established using the header annotation "Answer P125…P164": reference answer PDF page number = book page P − 123; answers for assessment papers are in their own PDF at p42–p49.

3. `data/catalog.js` was generated to describe each paper's name, group, question page list, answer page list, and default question count.

4. Since answers cannot be OCR'd into reliable text, the default mode is **self-checking against answer pages**; if parents are willing to manually fill in a text answer key (e.g., `1.A 2.C 3.24`), auto-grading becomes available.

> The original 4 PDFs are kept in `data/` as source material. The tool does not read them at runtime (only the split images are used), so opening via `file://` works perfectly.

Main Features

-------------

- **Four-Dimensional Filter**: Grade / Semester / Subject / Edition (e.g., "Grade 5 · Semester 1 · Math · Beijing Normal Univ. Edition"). Options are auto-collected from question bank metadata. Adding other grades or subjects in the future only requires adding corresponding question bank files — no code changes needed.

- **Paper-Based Units, No Daily Question Limit**. The practice page allows `− question / + question`微调 (fine-tuning) of the question count per paper.

- **Multi-Paper Independent Save**: Click "💾 Save & Exit" mid-session; the home page lists all incomplete papers, allowing you to resume or abandon; progress across different papers does not overwrite each other.

- **Split-Screen Layout**: Left side shows questions (with page-flip / zoom), right side for entering answers per question.

- **Per-Question Splitting (done for main book)**: Question pages in the main book are auto-segmented by blue question-number blocks to locate each question's boundary. During practice, the default is "current question only"; one click switches back to the full page. Answers are similarly split per question, with **one-to-one question-to-answer display**. If mismatched, use "Swap Block" to manually specify (selection is remembered).

- **Previous Question ◀**: Both the practice page header and answer area have a "◀ Previous Question" button (← key also works), allowing review of already-graded questions without re-scoring.

- **Hints**: Two levels of conceptual guidance (generic hints for scanned papers).

- **Grading & Attribution**: Shows correct answer/answer page. After a wrong answer, select a reason — Habit Issue 😅 / Reading Comprehension 📖 / Writing Error ✍️ / Calculation Mistake 🧮 / Conceptual Gap 🤔 — each with improvement suggestions.

- **Ore Incentive System (Minecraft-style)**: 12 ore types. Rewards for consecutive correct answers (3/5/8/12), hard questions answered correctly on first try, full paper perfect score, cumulative 100/300 correct answers, and 7-day consecutive practice. **Ores are permanent collectibles, never deducted.**

- **Mistake Notebook**: Auto-collects wrong answers; allows redo of "unconquered" mistakes (correct redo earns Copper Ore). Attribution reasons can be supplemented at any time.

- **Statistics**: Accuracy rate, last 7 days, error cause distribution, progress per paper. Error causes are counted "once per wrong question"; changing attribution auto-moves the count to the new category without artificial inflation from repeated clicks.

- **Settings**: Custom learner name (takes effect immediately), avatar, sound effects, data export/import, and reset.

Extending to Other Grades / Subjects

------------------------------------

1. Copy `data/catalog.js` to `catalog_g6a_math.js`, replacing `name`, `meta` (grade/term/subject/edition), and `sections`.

2. Place the new question bank page images into `data/pages/q/` and `data/pages/a/`.

3. Add one line in `index.html`: `<script src="data/catalog_g6a_math.js"></script>`.

Format for each paper in `sections`:

```js
{
  id: 'k01', name: 'Lesson 1 · Revisiting Decimals (Part 1)',
  type: 'Lesson', unit: 'Unit 1', group: 'Lesson Exercises',
  qImages: ['data/pages/q/q_main_006.jpg', '...'],  // question pages
  aImages: ['data/pages/a/a_ans_002.jpg'],          // answer pages (stored separately)
  qCount: 12,          // default question count, adjustable during practice
  key: ''              // optional text answer key, e.g., '1.A 2.C 3.24'
}
```

You can also directly **upload question PDFs and answer PDFs separately**​ on the "Question Bank" page (stored in IndexedDB), fill in grade/semester/subject/edition to register as a new bank, then use "✂️ Manage Chapters" to adjust each paper's question and answer page ranges.

**🧩 Questions and answers mixed in one PDF?**​ Use "Mixed Upload": select one PDF → fill in name → "Answer starts from page ___" (leave 0 = auto-detect page with "Reference Answer" text; scanned versions lack a text layer, so please manually enter the answer start page number) → click "🧩 Smart Split & Register". The tool slices each page into "one block per question" based on blank gaps; question blocks and answer blocks are paired **one-to-one in order**. During practice, only the current question block is shown on the left; clicking "View Answer" shows the paired answer block. If mismatched, use "◀ Swap Block / Swap Block ▶" to correct (selection is saved). Note: sliced images are saved in the browser's IndexedDB; switching computers requires re-uploading and splitting. To preview the slicing effect beforehand, use the diagnostic page `tools/split-lab.html` (start a static server in the same directory to access).

Also supports importing **JSON structured question banks**​ (with options, answers, hints, explanations, and auto-grading). Format is the same as above but uses a `qs` array instead of `qImages`:

```json
{
  "name": "Grade 4 · Some Workbook",
  "meta": { "grade": "Grade 4", "term": "Semester 1", "subject": "Math", "edition": "People's Education Edition" },
  "sections": [{
    "id": "g4s1", "name": "Unit 1", "group": "Unit",
    "qs": [{
      "t": "c", "d": 2, "q": "Question text…",
      "o": ["Option A", "Option B", "Option C"],
      "a": "B", "h": "Hint 1", "h2": "Hint 2", "e": "Explanation"
    }]
  }]
}
```

Data & Privacy

--------------

- Name/settings, per-paper progress & saves, mistake notebook, ores, statistics: `localStorage` (key prefix `mo_`)

- Uploaded PDFs: `IndexedDB` (local only)

- Settings page supports JSON backup export/import; **question bank images and original PDFs must be archived separately**​ (backup JSON does not include images).

Sharing with Others

-------------------

`math-practice-tool.zip` in the same directory is a **portable version ready to share**: includes `index.html`, `app.js`, `style.css`, `README.md`, `vendor/`, `data/catalog.js`, and all question/answer page images. The recipient can simply unzip and double-click `index.html` — no installation needed.

The original 4 scanned PDFs total nearly 200MB and are not read at runtime, so they are **not included in the zip**​ (still fully preserved in the local `data/` directory). If the recipient needs the original PDFs for re-splitting, simply copy `data/*.pdf` separately.

> Learning records (name, progress, mistakes, ores) are stored in each browser's `localStorage` and do not transfer with the folder. To migrate, use the Settings page "⬇️ Export All Data (JSON)", then "⬆️ Import Data" on the recipient's machine.

File Structure

--------------

```
math-practice-tool/
├── index.html
├── style.css
├── app.js
├── README.md
├── data/
│   ├── catalog.js            # 70 papers catalog (per-question split + 1-to-1 answers)
│   ├── catalog_2026_g5a.js   # 2026 Autumn synchronized new question bank (12 chapters, 240 questions)
│   ├── pages/q/*.jpg         # 164 question pages
│   ├── pages/a/*.jpg         # 48 answer pages
│   └── *.pdf                 # Original 4 PDFs (source material, not read at runtime)
├── tools/
│   └── split-lab.html        # Mixed PDF split diagnostic page (optional)
└── vendor/
    ├── pdf.min.js            # For "self-upload PDF" feature, already localized
    └── pdf.worker.min.js
```









# ⛏️ 矿石数学 · 补充练习小工具

纯本地 HTML 的补充练习工具。双击 `index.html` 即可用，**无需联网、不上传任何数据**。

## 当前题库（data/ 目录）

**① 5·3天天练 2026 秋季版 · 五年级上 · 数学 · 北师大版（BSD）**，共 **70 张卷子**：

| 分组   | 张数  | 来源                                   |
| ---- | --- | ------------------------------------ |
| 课时练习 | 51  | `53天练5年级上2026版.pdf` p6–p107（每课时 2 页） |
| 综合复习 | 1   | 主册 p108–p113 期末综合复习                  |
| 测评卷  | 10  | `测评卷(大字版及答案).pdf` p2–p41（每卷 4 页）     |
| 思维训练 | 8   | `思维训练及答案.pdf` p3–p18（每专题 2 页）        |

**② 2026 秋版同步新编题库 · 五年级上 数学（北师大版）**，共 **12 章 240 题**（`data/catalog_2026_g5a.js`）：

- 目录按 2026 秋版教材：8 个单元 + 2 个综合实践 + 数学好玩（鸡兔同笼）+ 总复习。
- 每章 20 题，难度混合出现：**基础 40% ⭐ / 提高 40% ⭐⭐ / 难题 20% ⭐⭐⭐**。
- 全部为**文字结构化题**，可自动判分，带两级提示与逐题解释。

### 题目与答案已拆开

这 4 份 PDF 都是**扫描版，没有文字层**，无法自动识别公式和答案文字。处理方式：

1. 把每一页渲染成 JPEG，按用途放进两个独立目录：
   - `data/pages/q/` → **题目页**（164 张），练习时展示
   - `data/pages/a/` → **答案页**（48 张），默认折叠，点「📖 看答案」才展开
2. 靠页眉的「答案 P125…P164」标注建立配对：参考答案册 PDF 页码 = 书页 P − 123；测评卷的答案在其自身 PDF 的 p42–p49。
3. 生成 `data/catalog.js` 描述每张卷子的名称、分组、题目页列表、答案页列表、默认题数。
4. 因为答案无法 OCR 成可靠文字，默认采用**对照答案页自评**；如果家长愿意手填文字答案钥匙（`1.A 2.C 3.24`），则可自动判分。

> 原始 4 份 PDF 保留在 `data/` 里作为底本，工具运行时不读取它们（只读拆分后的图片），因此 `file://` 直接打开也能显示。

## 主要功能

- **四维筛选框**：年级 / 册 / 科目 / 版本（如「五年级 · 上 · 数学 · 北师大版」）。选项从题库元数据自动收集，未来加其它年级或科目，只要加对应题库文件即可，无需改代码。
- **按卷子为单位，不设每日题数限制**。练习页可 `－题 / ＋题` 微调本卷题数。
- **多卷子独立暂存**：做到一半点「💾 存档退出」，首页列出所有没做完的卷子，可继续或放弃；不同卷子的进度互不覆盖。
- **左右分栏**：左边题目（可翻页 / 放大），右边逐题输入答案。
- **按题切分（主册已做）**：课时练习的题目页按蓝色题号方块自动定位每题边界，练习时默认「只看本题」，可一键切回整页；答案同样切成每题一块，**题目与答案一对一**展示，配错了可用「换一块」手动指定（选择会记住）。
- **上一题 ◀**：练习页题头和作答区都有「◀ 上一题」（← 键同样有效），可回看已批改的题，只回看不重复计分。
- **提示**：两级思路点拨（扫描卷用通用思路提示）。
- **批改与归因**：显示正确答案/答案页，答错后选原因——习惯问题😅 / 读题理解📖 / 写错✍️ / 计算问题🧮 / 概念不清🤔，每类附改进建议。
- **矿石激励（Minecraft 风）**：12 种矿石，连对 3/5/8/12 题、难题一次做对、整卷全对、累计 100/300 题、连续 7 天都有奖励，**只增不减**。
- **错题本**：自动收录，可重做「未征服」错题（答对得铜矿石），原因随时补归类。
- **统计**：正确率、最近 7 天、错因分布、各卷子进度。错因按「一道错题只计一次」统计，改动归因时自动把计数挪到新类别，重复点击不会虚增。
- **设置**：自定义学习者名字（立即生效）、头像、音效、数据导出/导入、清空。

## 扩展其它年级 / 科目

1. 复制 `data/catalog.js` 改成 `catalog_g6a_math.js`，替换 `name`、`meta`（grade/term/subject/edition）和 `sections`。
2. 把新题库的页面图片放进 `data/pages/q/`、`data/pages/a/`。
3. 在 `index.html` 里加一行 `<script src="data/catalog_g6a_math.js"></script>`。

`sections` 里每张卷子的格式：

```js
{
  id: 'k01', name: '第1课时 · 小数的再认识（一）',
  type: '课时', unit: '第一单元', group: '课时练习',
  qImages: ['data/pages/q/q_main_006.jpg', '...'],  // 题目页
  aImages: ['data/pages/a/a_ans_002.jpg'],          // 答案页（单独存放）
  qCount: 12,          // 默认题数，练习时可增减
  key: ''              // 可选文字答案钥匙，如 '1.A 2.C 3.24'
}
```

也可以在「题库」页直接**分别上传题目 PDF 和答案 PDF**（存 IndexedDB），填好年级/册/科目/版本后登记为新题库，再用「✂️ 管理章节」调整每张卷子的题目页与答案页范围。

**🧩 题目和答案混在一份 PDF 里？** 用「混合上传」：选一份 PDF → 填名字 → 「答案从第几页开始」（留 0 = 自动找「参考答案」字样所在页；扫描版没有文字层，请手填答案首页码）→ 点「🧩 智能拆分并登记」。工具会逐页按空白带把内容切成「一题一块」，题目块和答案块按顺序**一对一配对**；练习时左边只显示本题块，点「看答案」显示配对的答案块，配错了用「◀ 换一块 / 换一块 ▶」修正（选择会保存）。注意：切块图保存在本机浏览器的 IndexedDB 里，换电脑需要重新上传拆分。想预先检查切块效果，可用诊断页 `tools/split-lab.html`（同目录起个静态服务后访问）。

另支持导入 **JSON 结构化题库**（带选项、答案、提示、解释，可自动判分），格式同上但用 `qs` 数组代替 `qImages`：

```json
{
  "name": "四年级 · 某练习册",
  "meta": { "grade": "四年级", "term": "上", "subject": "数学", "edition": "人教版" },
  "sections": [{
    "id": "g4s1", "name": "第一单元", "group": "单元",
    "qs": [{
      "t": "c", "d": 2, "q": "题干……",
      "o": ["选项A", "选项B", "选项C"],
      "a": "B", "h": "提示1", "h2": "提示2", "e": "解释"
    }]
  }]
}
```

## 数据与隐私

- 名字/设置、各卷子进度与暂存、错题本、矿石、统计：`localStorage`（键前缀 `mo_`）
- 上传的 PDF：`IndexedDB`（仅本机）
- 设置页可导出/导入 JSON 备份；**题库图片与 PDF 原件请自行留档**（备份 JSON 不含图片）。

## 发给别人

同目录下的 `math-practice-tool.zip` 是**可直接转发的便携版**：包含 `index.html`、`app.js`、`style.css`、`README.md`、`vendor/`、`data/catalog.js` 与全部题目页/答案页图片。对方解压后双击 `index.html` 就能用，不需要安装任何东西。

原始 4 份扫描 PDF 体积接近 200MB，且工具运行时并不读取它们，因此**未放进 zip**（仍完整保留在本机 `data/` 目录里）。如果对方需要底本 PDF 重新拆分，单独把 `data/*.pdf` 复制过去即可。

> 学习记录（名字、进度、错题、矿石）存在各自浏览器的 `localStorage`，不会随文件夹一起转移；要带走请用设置页的「⬇️ 导出全部数据（JSON）」，在对方机器上「⬆️ 导入数据」。

## 文件结构

```
math-practice-tool/
├── index.html
├── style.css
├── app.js
├── README.md
├── data/
│   ├── catalog.js            # 70 张卷子目录（已按题切分 + 答案一对一）
│   ├── catalog_2026_g5a.js   # 2026 秋版同步新编题库（12 章 240 题）
│   ├── pages/q/*.jpg         # 164 张题目页
│   ├── pages/a/*.jpg         # 48 张答案页
│   └── *.pdf                 # 原始 4 份 PDF（底本，工具运行时不读）
├── tools/
│   └── split-lab.html        # 混合 PDF 拆分效果诊断页（可选）
└── vendor/
    ├── pdf.min.js            # 供「自行上传 PDF」用，已本地化
    └── pdf.worker.min.js
```
