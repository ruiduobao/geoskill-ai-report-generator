# AI Remote Sensing Analysis Report Generation (geoskill-ai-report-generator)

> Fills analysis-result JSON into templates to generate structured HTML/Markdown reports (offline numpy equivalent implementation)

---

## 1. Overview

Automatically renders remote sensing analysis results (metric dictionaries / per-band raster statistics / JSON files) into structured reports: title, metadata, overview statistics, metric detail tables, threshold ratings (PASS/WARN/FAIL) and conclusions, supporting both HTML and Markdown formats. This skill is an **offline numpy equivalent implementation** of an LLM-based automatic report system: without relying on a large model, it reproduces the report generation pipeline with "result parsing → summary statistics and threshold rating (rule-based conclusion generation) → HTML-escape-safe template filling"; all dynamic content is HTML-escaped to prevent injection.

## 3. Quick Start

```bash
pip install -r requirements.txt
python geoskill-ai-report-generator.py --bbox 116 39 117 40 --synthetic --output-dir ./out
```

## 4. CLI Parameters

Run `python <skill>.py --help` for the full list. Common parameters:

| Parameter | Type | Description |
|---|---|---|
| `--bbox` | `float[4]` | WGS84 bounding box `min_lon min_lat max_lon max_lat` |
| `--input` | `path` | Local input file (GeoJSON/GeoTIFF/etc.) |
| `--output-dir` | `path` | Output directory (default `./output`) |
| `--synthetic` | `flag` | Use synthetic data instead of real input |
| `--quiet` | `flag` | Suppress non-essential stdout |

## 5. Input / Output

| File | Format | Description |
|---|---|---|
| `report.html` | HTML | Self-contained HTML report with inline styles |
| `report.md` | Markdown | Markdown report with the same content |
| `report_summary.json` | JSON | Summary statistics + rating flags + raw results |
| `output-manifest.json` | JSON | Run manifest (input/output/QA/exit code) |


## 6. Technical Principle

(see SKILL.md for details)

## 8. License

MIT License. See [`LICENSE`](./LICENSE) for full text.

---

> 中文完整版：[references/SKILL.zh-CN.md](references/SKILL.zh-CN.md)
