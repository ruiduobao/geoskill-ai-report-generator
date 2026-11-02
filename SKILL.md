---
name: geoskill-ai-report-generator
description: '分析结果JSON模板填充，生成结构化HTML/Markdown报告（离线numpy等价实现）'
---

# AI遥感分析报告生成 | AI Remote Sensing Report Generator

Automatically renders remote sensing analysis results (metric dictionaries / per-band raster statistics / JSON files) into structured reports: title, metadata, overview statistics, metric detail tables, threshold ratings (PASS/WARN/FAIL) and conclusions, supporting both HTML and Markdown formats.

This skill is an **offline NumPy-equivalent implementation** of an LLM-driven automatic reporting system: it reproduces the report generation pipeline without relying on a large model, using "result parsing -> summary statistics and threshold rating (rule-based conclusion generation) -> HTML-escaped template filling"; all dynamic content is HTML-escaped to prevent injection.

## Dependencies / 依赖

```bash
pip install numpy rasterio scipy scikit-learn geopandas shapely
```

## Usage / 使用方法

### Example 1 (Synthetic Data, Offline)

```bash
python geoskill-ai-report-generator.py --bbox 116.0 39.0 117.0 40.0 --synthetic --output-dir ./out
```

### Example 2: Synthetic Sample Report (Offline)

```bash
python geoskill-ai-report-generator.py --bbox 116.0 39.0 117.0 40.0 --synthetic --title "parcel monthly report" --output-dir ./out
```

### 示例 3：分析结果 JSON -> 报告

```bash
python geoskill-ai-report-generator.py --analysis results.json --title "monitoring report" --format both --output-dir ./out
```

### Example 4: Automatic Raster Statistics to Report

```bash
python geoskill-ai-report-generator.py --input scene.tif --format md --output-dir ./out
```

## Output / 输出

| File | Format | Description |
|---|---|---|
| `report.html` | HTML | Standalone HTML report with inline styles |
| `report.md` | Markdown | Markdown report with the same content |
| `report_summary.json` | JSON | Summary statistics + rating flags + raw results |
| `output-manifest.json` | JSON | Run manifest (inputs/outputs/QA/exit code) |

## Data Source / 数据源 / Source

Analysis result JSON / local GeoTIFF (per-band statistics computed automatically), or --synthetic example results.

## Privacy / 隐私声明 / Privacy

- Runs offline by default; `--synthetic` mode requires no network at all.
- All processing is done locally; no user data is ever uploaded.

## License / License

MIT

---

> 中文完整版：需要时再读 [references/SKILL.zh-CN.md](references/SKILL.zh-CN.md)，不要默认全量加载。
