# 导入样例（Trados / memoQ）

本目录是**由本工具完整管线真实产出**的术语表样例（EN↔ZH，35 条，边缘计算领域），
可直接用于验证 Trados MultiTerm 与 memoQ 的导入流程。样本内容见 `terms_sample.md`。

## Trados Studio / MultiTerm

**文件：`terms_sample.tbx`**（TBX v02 martif，含 subjectField / usageNote / partOfSpeech）

1. MultiTerm 侧：打开 **MultiTerm Desktop → Catalogue → New → Create termbine from scratch**（或 Convert）；
   直接导入 TBX 的最短路径是 **MultiTerm Convert**（随 Trados Studio 安装）：
   选择 *TBX → MultiTerm XML*，输入 `terms_sample.tbx`，向导会自动识别
   `langSet xml:lang`（en / zh-CN）为索引字段、`subjectField` 为描述性字段；
2. Studio 侧：项目设置 → **Language Resources → Termbases → Add**，挂上转换后的 `.sdldb`；
3. 验证：在编辑器中打开任意句段，命中 `edge computing` 等术语时术语识别窗口应弹出「边缘计算」。

> 备注：Studio 对 `xml:lang="en"` / `zh-CN` 的语言区按名称映射；若你的目标语是繁体，
> 在 MultiTerm 中把 zh-CN 索引改名或重导（工具可导出 zh-TW 语言区）。

## memoQ

**文件：`terms_sample.csv`**（UTF-8 BOM，列：source_term / target_term / freq / confidence / status / pos / domain / note）

1. **Resources → Term bases → Create/import → Import from CSV**（或新建 term base 后 Import → CSV）；
2. 编码选 **UTF-8**（本文件带 BOM，memoQ 可自动识别），分隔符逗号；
3. 字段映射：第 1 列 → 源语（English），第 2 列 → 目标语（Simplified Chinese）；
   `domain` 可映射到自定义元数据字段（或跳过）；
4. 勾选 **First row contains column titles**；
5. 验证：翻译编辑器中 `machine learning` 应标蓝并提示「机器学习」。

> 备注：CSV 中的置信度（confidence）与状态（status）是审校辅助信息，memoQ 不使用它们；
> 若需保留这些字段，建议用 TBX（usageNote）路径或以 JSON/MD 留档。

## 其他格式

- `terms_sample.md`：人读速览表（审校/评审用，勿导入 CAT）；
- 完整结构化产物（`terms.json` + 审校报告）可用 `node scripts/finalize.js ...` 重新生成，
  schema 见 `references/architecture.md` §4。
