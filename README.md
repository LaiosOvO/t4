# T4 工业图纸多模态 · 测试与解析结果

本仓库只包含 **测试报告、测试数据与测试结果**，不包含任何业务源码。

## 目录

| 路径 | 内容 |
| --- | --- |
| `index.html` | 测试报告主页 |
| `results/output_t4_drawing_extraction.json` | 图纸批量提取结果（52 份全部成功） |
| `results/output_t4_opensource_eval_benchmark.json` | 五阶段基准评测（文本层 / 版面切分 / 向量检索 / GDT 多语 / SOP 零幻觉） |
| `results/output_anydoc_vs_markitdown_eval.json` | 解析引擎对比实测（AnyDoc vs MarkItDown） |
| `results/output_t4_embedding_model_eval.json` | Embedding 模型评测（122 页图库，5 模型） |
| `results/output_t4_milvus_roundtrip.json` | 向量库往返测试 |
| `results/output_top3_search_results.json` | Top3 图纸检索结果 |
| `data/T4_drawings/` | 测试图纸样本 |

## 报告覆盖的测试步骤

1. **图纸批量提取**：52 份全部成功
2. **文本层解析**：50 份 PDF / 120 页，PyMuPDF vs pdfplumber vs MarkItDown 三引擎实测
3. **版面切分**：模板图签命中率 / OpenCV 轮廓命中率
4. **向量检索**：122 页图库 + 3 类查询，Top3 结果带相似度与副本判定
5. **ASME/GDT 多语**：结构就绪（SCHEMA_OK_CONTENT_EMPTY）
6. **SOP 零幻觉**：INCOMPLETE（无工艺参数真值集，不宣称幻觉率 0%）

## 诚实标注原则

评测结论按实测标注（`provenance: measured`），不给写死分数。CAD 图纸 59.17% 页面零字符（尺寸/引出线为矢量几何）为实测根因，对应最佳实践为「文本检测 + 视觉大模型兜底」两步法。

## 复现

打开 `index.html` 即可查看全部测试过程与结果；`results/` 下 JSON 可直接用于比对。
