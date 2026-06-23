<div align="center">

# ocrmypdf-skills

**OCRmyPDF skills — PDF OCR, image processing, optimization, batch processing**

[![GitHub](https://img.shields.io/badge/github-full--stack--skills%2Focrmypdf-skills-green.svg)](https://github.com/full-stack-skills/ocrmypdf-skills)
[![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](LICENSE)
[![Agent Skills](https://img.shields.io/badge/Agent%20Skills-Compatible-purple.svg)](https://agentskills.io)

English | [简体中文](./README.zh-CN.md)

[Introduction](#-introduction) ·
[Install](#-install) ·
[Skills](#-skills) ·
[Supported Agents](#-supported-agents) ·
[Ecosystem](#-ecosystem)

</div>

---

## 📖 Introduction

**OCRmyPDF Skills** is a curated collection of Agent Skills for AI coding agents, part of the [Full Stack Skills](https://github.com/partme-ai/full-stack-skills) ecosystem maintained by [PartMe.AI](https://github.com/partme-ai).

This package includes **5 skills**. Each skill is a self-contained `SKILL.md` file that AI agents load on-demand.

## 📦 Install

```bash
npx skills add full-stack-skills/ocrmypdf-skills
```

Or install specific skills:

```bash
npx skills add full-stack-skills/ocrmypdf-skills --skill <skill-name>
```

## 🎯 Skills (5)

| Skill | Description |
|-------|-------------|
| `ocrmypdf-api` | OCRmyPDF Python API and plugin skill — use OCRmyPDF programmatically from Python, integrate with applications, and ex... |
| `ocrmypdf-batch` | OCRmyPDF batch processing skill — process multiple PDFs, Docker automation, shell scripting, and CI/CD integration. U... |
| `ocrmypdf-image` | OCRmyPDF image processing skill — deskew, rotate, clean, despeckle, remove border from scanned documents. Use when th... |
| `ocrmypdf-optimize` | OCRmyPDF optimization skill — compress PDFs, configure PDF/A output, JBIG2 encoding, and lossless optimization. Use w... |
| `ocrmypdf` | OCRmyPDF core skill — add searchable OCR text layer to scanned PDFs, convert images to searchable PDFs, support 100+ ... |

## 🤖 Supported Agents

Works with [Claude Code](https://code.claude.com), [Codex](https://developers.openai.com/codex), [Cursor](https://cursor.com), [OpenCode](https://opencode.ai), [Gemini CLI](https://geminicli.com), [GitHub Copilot](https://github.com/features/copilot), [Windsurf](https://codeium.com/windsurf), and [70+ others](https://agentskills.io/clients).

### Claude Code Installation

**Option 1: npx skills CLI (Recommended)**

```bash
npx skills add full-stack-skills/ocrmypdf-skills
```

**Option 2: Manual Installation**

```bash
git clone https://github.com/full-stack-skills/ocrmypdf-skills.git
cp -r ocrmypdf-skills/skills/* .claude/skills/
```

For more details, see the [Claude Code Skills Guide](https://code.claude.com/docs/en/skills) and [Agent Skills Spec](https://agentskills.io/).

## 🌐 Ecosystem

| Resource | Link |
|----------|------|
| **Full Stack Skills** | [github.com/partme-ai/full-stack-skills](https://github.com/partme-ai/full-stack-skills) |
| **All Skill Groups** | [github.com/full-stack-skills](https://github.com/full-stack-skills) |
| **Agent Skills Spec** | [agentskills.io](https://agentskills.io) |
| **Skills CLI** | [github.com/vercel-labs/skills](https://github.com/vercel-labs/skills) |

## 📄 License

Apache 2.0 — see [LICENSE](LICENSE).
