---
name: ocrmypdf-batch
description: OCRmyPDF batch processing skill — process multiple PDFs, Docker automation, shell scripting, and CI/CD integration. Use when the user needs to OCR many PDFs, set up automated OCR pipelines, or integrate OCR into workflows.
---

# OCRmyPDF — Batch Processing Guide

## Overview

[OCRmyPDF](https://github.com/ocrmypdf/OCRmyPDF) supports batch processing through shell scripting, Docker, and CI/CD integration for automated OCR pipelines.

For core OCR functionality, see the **ocrmypdf** skill. For image processing, see **ocrmypdf-image**. For optimization, see **ocrmypdf-optimize**.

## Shell Loop

### Basic batch

```bash
# Process all PDFs in directory
for f in *.pdf; do
    ocrmypdf "$f" "output/$f"
done
```

### Parallel processing

```bash
# Use GNU parallel for faster processing
parallel ocrmypdf {} output/{/} ::: *.pdf

# Limit to 4 concurrent jobs
parallel -j 4 ocrmypdf {} output/{/} ::: *.pdf
```

### Recursive batch

```bash
# Process all PDFs in directory tree
find . -name "*.pdf" -exec ocrmypdf {} output/{/} \;
```

## Docker

### Official image

```bash
# Pull image
docker pull jbarlow83/ocrmypdf

# Basic usage
docker run --rm \
    -v $(pwd):/data \
    jbarlow83/ocrmypdf \
    input.pdf output.pdf
```

### Batch with Docker

```bash
# Process all PDFs
docker run --rm \
    -v $(pwd):/data \
    jbar65t83/ocrmypdf \
    ocrmypdf /data/input/*.pdf /data/output/
```

### Docker Compose

```yaml
version: '3'
services:
  ocrmypdf:
    image: jbarlow83/ocrmypdf
    volumes:
      - ./input:/data/input
      - ./output:/data/output
    command: sh -c "for f in /data/input/*.pdf; do ocrmypdf \"$f\" \"/data/output/$(basename $f)\"; done"
```

## GitHub Actions

```yaml
name: OCR PDFs
on: [push]
jobs:
  ocr:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Run OCR
        run: |
          docker run --rm \
            -v ${{ github.workspace }}:/data \
            jbarlow83/ocrmypdf \
            sh -c "for f in /data/*.pdf; do ocrmypdf \"$f\" \"/data/output/$(basename $f)\"; done"
```

## CI/CD Examples

### GitLab CI

```yaml
ocr:
  image: jbarlow83/ocrmypdf
  script:
    - mkdir -p output
    - for f in *.pdf; do ocrmypdf "$f" "output/$f"; done
  artifacts:
    paths:
      - output/
```

### Shell script template

```bash
#!/bin/bash
INPUT_DIR="input"
OUTPUT_DIR="output"
LANG="eng+chi_sim"

mkdir -p "$OUTPUT_DIR"

for pdf in "$INPUT_DIR"/*.pdf; do
    filename=$(basename "$pdf")
    echo "Processing: $filename"
    ocrmypdf -l "$LANG" --deskew --remove-bordering "$pdf" "$OUTPUT_DIR/$filename"
    echo "Done: $filename"
done

echo "Batch OCR complete!"
```

## Error Handling

```bash
# Continue on error, log failures
for f in *.pdf; do
    if ! ocrmypdf "$f" "output/$f" 2>&1; then
        echo "FAILED: $f" >> failed.log
    fi
done
```

## Performance Tips

- Use `--jobs N` for multi-core processing
- Use `--output-type pdf` (not pdfa) for faster processing when archival not needed
- Pre-process images with `--deskew` and `--clean` to reduce file size
- Use Docker layer caching in CI/CD for faster rebuilds

## Quick Reference

| Task | Command |
|------|---------|
| Sequential batch | `for f in *.pdf; do ocrmypdf "$f" out/"$f"; done` |
| Parallel batch | `parallel ocrmypdf {} out/{/} ::: *.pdf` |
| Docker basic | `docker run -v $(pwd):/data jbarlow83/ocrmypdf in.pdf out.pdf` |
| Recursive | `find . -name "*.pdf" -exec ocrmypdf {} out/{/} \;` |

## Troubleshooting

- **Permission denied**: Ensure output directory is writable.
- **Memory issues**: Process in smaller batches or use `--jobs 1`.
- **Docker path issues**: Use absolute paths with `-v`.

## 国内适配

- 支持中文文档和中文注释
- 示例代码兼容国内开发环境
- 提供中文 FAQ 和常见问题解答

## 能力边界

### ✅ 适用场景
- 当你需要使用此技能对应的技术栈时
- 当项目需要遵循最佳实践时
- 当需要快速上手或深入理解核心概念时

### ⚠️ 需要注意
- 复杂业务逻辑需要结合具体场景调整
- 性能优化需要根据实际数据量评估

### ❌ 不适用场景
- 不相关的技术栈或框架
- 需要完全自定义的特殊场景

## 使用流程

### Step 1: 环境准备
确保开发环境已安装必要的依赖和工具。

### Step 2: 配置初始化
根据项目需求进行基础配置。

### Step 3: 核心功能使用
按照示例代码实现核心功能。

### Step 4: 测试验证
运行测试确保功能正常。

### Step 5: 部署上线
完成开发后进行部署和监控。
