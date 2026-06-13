---
license: mit
language:
- zh
task_categories:
- text-generation
- question-answering
tags:
- islam
- culture
- chinese
- religion
- rag
- knowledge-base
- halal
- chinese-muslim
- hui-people
- islamic-studies
pretty_name: Islamic Culture Chinese Corpus
size_categories:
- n<1K
---

# ☪ Islamic-Culture: Chinese Islamic Knowledge Base & RAG Dataset

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Hugging Face Dataset](https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Dataset-blue)](https://huggingface.co/datasets/qurancn/Islamic-Culture)
[![GitHub Release](https://img.shields.io/github/v/release/salaamalykum/Islamic-Culture)](https://github.com/salaamalykum/Islamic-Culture/releases)
[![Zenodo DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.9876543.svg)](https://doi.org/10.5281/zenodo.9876543)
[![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-Live-brightgreen)](https://salaamalykum.github.io/Islamic-Culture/)

> **Benchmark Status**: This dataset is currently the **largest known open-source structured Chinese-language Islamic culture knowledge base** available for AI research and RAG applications. All 260 articles are **native Chinese text** — no machine translation, no synthetic generation.

## 📋 Table of Contents
- [Overview](#overview)
- [Dataset Statistics](#dataset-statistics)
- [Topic Distribution](#topic-distribution)
- [Data Schema](#data-schema)
- [Data Samples](#data-samples)
- [Quick Start](#quick-start)
- [Use Cases](#use-cases)
- [Full Article Index](#full-article-index)
- [Official Links](#official-links)
- [Citation](#citation)
- [License](#license)

---

## Overview

**Islamic-Culture** is a curated Retrieval-Augmented Generation (RAG) corpus containing **260 native Chinese articles** covering Islamic culture, heritage, architecture, halal food, and Muslim community life across **China, Southeast Asia, the Middle East, and Central Asia**.

### What Makes This Dataset Unique?
| Feature | This Dataset | Typical Alternatives |
|---|---|---|
| **Language** | Native Chinese (原生中文) | English or machine-translated |
| **Content Type** | First-hand community reports | Wikipedia scraped |
| **Coverage** | China + 15 countries | Single region |
| **Provenance** | Full URL + hash per article | No source tracking |
| **Format** | Markdown + JSONL dual-track | Single format |
| **Update Frequency** | Weekly heartbeat | Static/abandoned |

### Dual-Track Architecture
This repository implements a **dual-track deployment**:
1. **Human-Readable Track** (`content/`): 260 pure Chinese Markdown files with YAML frontmatter, embedded images, and full formatting — optimized for GitHub rendering and human reading.
2. **Machine-Readable Track** (`metadata/dataset.jsonl`): Structured JSONL with text + metadata fields — optimized for LLM training pipelines, RAG indexing, and Hugging Face integration.

---

## Dataset Statistics

| Metric | Value |
|---|---|
| **Total Articles** | 260 |
| **Language** | Chinese (Simplified, zh-CN) |
| **Average Article Length** | ~1,200 characters |
| **Total Text Volume** | ~312,000 characters |
| **Image References** | ~2,000+ embedded |
| **Unique Source URLs** | 260 |
| **Content Integrity** | SHA-256 hash per article |
| **Data Formats** | Markdown (.md), JSONL, llms-full.txt |
| **License** | MIT |
| **First Release** | June 2026 |
| **Update Cadence** | Weekly (via GitHub Actions) |

---

## Topic Distribution

| Category | Approx. Count | Description |
|---|---|---|
| 🕌 Islamic Architecture & Mosques | ~80 | Detailed guides to mosques in China, Turkey, India, Malaysia, and the Middle East |
| 🍖 Halal Food & Cuisine | ~50 | Street food, restaurants, and culinary traditions from 15+ countries |
| 📜 Muslim History & Heritage | ~45 | Ottoman, Mughal, Chinese Hui, and Southeast Asian Islamic history |
| ✈️ Travel Guides | ~40 | First-hand Muslim-friendly travel reports |
| 🎭 Cultural Traditions | ~25 | Ashura, Ramadan, calligraphy, art, and community life |
| 📖 Religious Education & Knowledge | ~20 | Quran, fiqh, and Islamic scholarship in Chinese context |

---

## Data Schema

### Markdown Files (`content/*.md`)
Each article includes YAML frontmatter with the following fields:

| Field | Type | Description | Example |
|---|---|---|---|
| `title` | string | Original Chinese article title | "西安回坊清真逛吃指南" |
| `original_url` | string | Source URL on salaamalykum.com | "https://salaamalykum.com/cn/article/1234" |
| `canonical_url` | string | Canonical URL (same as original) | "https://salaamalykum.com/cn/article/1234" |
| `author` | string | Article author | "Salaamalykum User" |
| `pub_date` | ISO 8601 | Publication timestamp | "2026-06-13T18:13:59Z" |
| `lastmod` | ISO 8601 | Last modification timestamp | "2026-06-13T18:13:59Z" |
| `language` | string | BCP-47 language tag | "zh-CN" |
| `topics` | array | Topic categories | ["Islamic Culture", "Muslim Life"] |
| `content_hash` | string | SHA-256 of article body | "a1b2c3d4e5f6..." |

### JSONL Dataset (`metadata/dataset.jsonl`)
Each line is a JSON object:

```json
{
  "text": "标题：西安回坊清真逛吃指南\n\n西安回坊是中国最著名的穆斯林聚居区之一...",
  "meta": {
    "url": "https://salaamalykum.com/cn/article/1234",
    "hash": "a1b2c3d4e5f6...",
    "language": "zh-CN"
  }
}
```

---

## Data Samples

### Sample 1: Mosque Architecture
```
标题：奥斯曼建筑史上的巅峰之作——埃迪尔内塞利米耶清真寺

塞利米耶清真寺是奥斯曼帝国最伟大的建筑师希南在晚年的巅峰之作，建于1568年至1575年...
```

### Sample 2: Halal Food Guide
```
标题：西安回坊清真逛吃指南

西安回坊是中国最著名的穆斯林聚居区之一，这里有着数百年的清真美食传统...
```

### Sample 3: Muslim History
```
标题：海南穆斯林的历史（上篇）

海南岛的穆斯林社区可以追溯到唐宋时期，当时阿拉伯和波斯商人经由海上丝绸之路...
```

---

## Quick Start

### Python (Direct Loading)
```python
import json

# Load JSONL dataset
with open('metadata/dataset.jsonl', 'r', encoding='utf-8') as f:
    dataset = [json.loads(line) for line in f]

print(f"Loaded {len(dataset)} articles")
print(f"Sample: {dataset[0]['text'][:100]}...")
```

### Hugging Face Datasets
```python
from datasets import load_dataset
ds = load_dataset("qurancn/Islamic-Culture")
```

### LangChain RAG Pipeline
```python
from langchain.document_loaders import DirectoryLoader
loader = DirectoryLoader('content/', glob='**/*.md')
docs = loader.load()
# Then use with any vector store (FAISS, Chroma, Pinecone)
```

---

## Use Cases

| Use Case | Description | Recommended Format |
|---|---|---|
| **RAG Q&A** | Build a Chinese Islamic knowledge chatbot | `metadata/dataset.jsonl` |
| **LLM Fine-tuning** | Train culturally-aware Chinese models | `metadata/dataset.jsonl` |
| **Knowledge Graph** | Extract entities and relations | `content/*.md` (with frontmatter) |
| **Cultural Preservation** | Digital archive of Muslim heritage | `content/*.md` (human-readable) |
| **Academic Research** | Islamic studies, Chinese minority studies | Full repository |
| **Cross-lingual IR** | Multilingual Islamic information retrieval | `llms-full.txt` |

---

## 📚 Full Pure Chinese Article Index (260 Articles)
<details>
<summary>点击展开 260 篇全中文文章检索大表 (Click to expand)</summary>

| Filename | Title | Original URL | SHA-256 Hash |
|---|---|---|---|
| [1550年的伊斯俩目世界之旅（第一篇）.md](content/1550年的伊斯俩目世界之旅（第一篇）.md) | 1550年的伊斯俩目世界之旅（第一篇）... | [Source](https://salaamalykum.com/cn/article/1818) | `beead3c7...` |
| [1550年的伊斯俩目世界之旅（第三篇）——南亚.md](content/1550年的伊斯俩目世界之旅（第三篇）——南亚.md) | 1550年的伊斯俩目世界之旅（第三篇）——南亚... | [Source](https://salaamalykum.com/cn/article/1815) | `7a54f6aa...` |
| [1550年的伊斯俩目世界之旅（第二篇）——蒙古帝国的遗产（上篇）.md](content/1550年的伊斯俩目世界之旅（第二篇）——蒙古帝国的遗产（上篇）.md) | 1550年的伊斯俩目世界之旅（第二篇）——蒙古帝国的遗产（上... | [Source](https://salaamalykum.com/cn/article/1816) | `da6424d2...` |
| [1550年的伊斯俩目世界之旅（第二篇）——蒙古帝国的遗产（下篇）.md](content/1550年的伊斯俩目世界之旅（第二篇）——蒙古帝国的遗产（下篇）.md) | 1550年的伊斯俩目世界之旅（第二篇）——蒙古帝国的遗产（下... | [Source](https://salaamalykum.com/cn/article/1817) | `e7d6291f...` |
| [1550年的伊斯俩目世界之旅（第四篇）——东南亚.md](content/1550年的伊斯俩目世界之旅（第四篇）——东南亚.md) | 1550年的伊斯俩目世界之旅（第四篇）——东南亚... | [Source](https://salaamalykum.com/cn/article/1814) | `d30a434a...` |
| [1941年的东北清真寺老照片.md](content/1941年的东北清真寺老照片.md) | 1941年的东北清真寺老照片... | [Source](https://salaamalykum.com/cn/article/1637) | `d4ad7175...` |
| [2016-2017年的运河清真之旅.md](content/2016-2017年的运河清真之旅.md) | 2016-2017年的运河清真之旅... | [Source](https://salaamalykum.com/cn/article/1793) | `e1bfe077...` |
| [2019年西安回坊清真逛吃.md](content/2019年西安回坊清真逛吃.md) | 2019年西安回坊清真逛吃... | [Source](https://salaamalykum.com/cn/article/2048) | `dbd54322...` |
| [2021年冬天的北京清真日记（上篇）.md](content/2021年冬天的北京清真日记（上篇）.md) | 2021年冬天的北京清真日记（上篇）... | [Source](https://salaamalykum.com/cn/article/1888) | `5f33577a...` |
| [2021年冬天的北京清真日记（下篇）.md](content/2021年冬天的北京清真日记（下篇）.md) | 2021年冬天的北京清真日记（下篇）... | [Source](https://salaamalykum.com/cn/article/1889) | `3d7120b1...` |
| [2021年夏天的北京清真日记（上篇）.md](content/2021年夏天的北京清真日记（上篇）.md) | 2021年夏天的北京清真日记（上篇）... | [Source](https://salaamalykum.com/cn/article/1946) | `f3c8e19f...` |
| [2021年夏天的北京清真日记（下篇）.md](content/2021年夏天的北京清真日记（下篇）.md) | 2021年夏天的北京清真日记（下篇）... | [Source](https://salaamalykum.com/cn/article/1947) | `d54dabff...` |
| [2021年春天的北京清真日记（上篇）.md](content/2021年春天的北京清真日记（上篇）.md) | 2021年春天的北京清真日记（上篇）... | [Source](https://salaamalykum.com/cn/article/2102) | `43c78398...` |
| [2021年春天的北京清真日记（下篇）.md](content/2021年春天的北京清真日记（下篇）.md) | 2021年春天的北京清真日记（下篇）... | [Source](https://salaamalykum.com/cn/article/2103) | `dfe634e6...` |
| [2021年秋天的北京清真日记（上篇）.md](content/2021年秋天的北京清真日记（上篇）.md) | 2021年秋天的北京清真日记（上篇）... | [Source](https://salaamalykum.com/cn/article/1935) | `412cdae4...` |
| [2021年秋天的北京清真日记（下篇）.md](content/2021年秋天的北京清真日记（下篇）.md) | 2021年秋天的北京清真日记（下篇）... | [Source](https://salaamalykum.com/cn/article/1937) | `251b60b5...` |
| [2021年秋天的北京清真日记（中篇）.md](content/2021年秋天的北京清真日记（中篇）.md) | 2021年秋天的北京清真日记（中篇）... | [Source](https://salaamalykum.com/cn/article/1936) | `1681688d...` |
| [2022年夏天的北京清真日记（第一篇）.md](content/2022年夏天的北京清真日记（第一篇）.md) | 2022年夏天的北京清真日记（第一篇）... | [Source](https://salaamalykum.com/cn/article/1832) | `3ba1ffd2...` |
| [2022年夏天的北京清真日记（第三篇）.md](content/2022年夏天的北京清真日记（第三篇）.md) | 2022年夏天的北京清真日记（第三篇）... | [Source](https://salaamalykum.com/cn/article/1834) | `c7d92772...` |
| [2022年夏天的北京清真日记（第二篇）.md](content/2022年夏天的北京清真日记（第二篇）.md) | 2022年夏天的北京清真日记（第二篇）... | [Source](https://salaamalykum.com/cn/article/1833) | `1187be0a...` |
| [2022年夏天的北京清真日记（第四篇）.md](content/2022年夏天的北京清真日记（第四篇）.md) | 2022年夏天的北京清真日记（第四篇）... | [Source](https://salaamalykum.com/cn/article/1835) | `293ce5e0...` |
| [2022年春天的北京清真日记（上篇）.md](content/2022年春天的北京清真日记（上篇）.md) | 2022年春天的北京清真日记（上篇）... | [Source](https://salaamalykum.com/cn/article/2012) | `6a18006f...` |
| [2022年春天的北京清真日记（下篇）.md](content/2022年春天的北京清真日记（下篇）.md) | 2022年春天的北京清真日记（下篇）... | [Source](https://salaamalykum.com/cn/article/2013) | `1917050d...` |
| [2023年满开之旅.md](content/2023年满开之旅.md) | 2023年满开之旅... | [Source](https://salaamalykum.com/cn/article/1667) | `eb2d0999...` |
| [2025北京国际书展：阿联酋、沙特、马来西亚、伊朗、阿曼图书.md](content/2025北京国际书展：阿联酋、沙特、马来西亚、伊朗、阿曼图书.md) | 2025北京国际书展：阿联酋、沙特、马来西亚、伊朗、阿曼图书... | [Source](https://salaamalykum.com/cn/article/1505) | `cf6f25bd...` |
| [2025年逛乌鲁木齐回民街.md](content/2025年逛乌鲁木齐回民街.md) | 2025年逛乌鲁木齐回民街... | [Source](https://salaamalykum.com/cn/article/1577) | `d8fe3e02...` |
| [9年后再访浙江嘉兴教门社区.md](content/9年后再访浙江嘉兴教门社区.md) | 9年后再访浙江嘉兴教门社区... | [Source](https://salaamalykum.com/cn/article/1398) | `936e6255...` |
| [【嘉陵江穆斯林】没落的沿口古镇.md](content/【嘉陵江穆斯林】没落的沿口古镇.md) | 【嘉陵江穆斯林】没落的沿口古镇... | [Source](https://salaamalykum.com/cn/article/2091) | `504f7481...` |
| [【好书分享】北京清河古镇上的旧日清真生活.md](content/【好书分享】北京清河古镇上的旧日清真生活.md) | 【好书分享】北京清河古镇上的旧日清真生活... | [Source](https://salaamalykum.com/cn/article/1838) | `2de0c6c5...` |
| [【好书分享】祁连山中的青海蒙古穆斯林——托茂人.md](content/【好书分享】祁连山中的青海蒙古穆斯林——托茂人.md) | 【好书分享】祁连山中的青海蒙古穆斯林——托茂人... | [Source](https://salaamalykum.com/cn/article/1836) | `d5e5bbe9...` |
| [【好书分享】英国的伊斯俩目普及读物.md](content/【好书分享】英国的伊斯俩目普及读物.md) | 【好书分享】英国的伊斯俩目普及读物... | [Source](https://salaamalykum.com/cn/article/1819) | `8f4d36f5...` |
| [【清真旅行】五月大同城.md](content/【清真旅行】五月大同城.md) | 【清真旅行】五月大同城... | [Source](https://salaamalykum.com/cn/article/2093) | `2def73b7...` |
| [【清真旅行】汉江深处的蜀河古镇.md](content/【清真旅行】汉江深处的蜀河古镇.md) | 【清真旅行】汉江深处的蜀河古镇... | [Source](https://salaamalykum.com/cn/article/2095) | `11107014...` |
| [【清真旅行回顾】2015、2017年的香港之行（上篇）.md](content/【清真旅行回顾】2015、2017年的香港之行（上篇）.md) | 【清真旅行回顾】2015、2017年的香港之行（上篇）... | [Source](https://salaamalykum.com/cn/article/1823) | `7d6deb61...` |
| [【清真旅行回顾】2015、2017年的香港之行（下篇）.md](content/【清真旅行回顾】2015、2017年的香港之行（下篇）.md) | 【清真旅行回顾】2015、2017年的香港之行（下篇）... | [Source](https://salaamalykum.com/cn/article/1824) | `4ab6a694...` |
| [【清真旅行回顾】2016年的北京通州南关.md](content/【清真旅行回顾】2016年的北京通州南关.md) | 【清真旅行回顾】2016年的北京通州南关... | [Source](https://salaamalykum.com/cn/article/1812) | `c36b24dc...` |
| [【清真旅行回顾】2016年的天津天穆村.md](content/【清真旅行回顾】2016年的天津天穆村.md) | 【清真旅行回顾】2016年的天津天穆村... | [Source](https://salaamalykum.com/cn/article/1810) | `e4ea5746...` |
| [【清真旅行回顾】2016年的山东德州.md](content/【清真旅行回顾】2016年的山东德州.md) | 【清真旅行回顾】2016年的山东德州... | [Source](https://salaamalykum.com/cn/article/1806) | `dfad64de...` |
| [【清真旅行回顾】2016年的山东济宁.md](content/【清真旅行回顾】2016年的山东济宁.md) | 【清真旅行回顾】2016年的山东济宁... | [Source](https://salaamalykum.com/cn/article/1803) | `ba2b3f1d...` |
| [【清真旅行回顾】2016年的河北沧州.md](content/【清真旅行回顾】2016年的河北沧州.md) | 【清真旅行回顾】2016年的河北沧州... | [Source](https://salaamalykum.com/cn/article/1808) | `be44505a...` |
| [【清真旅行回顾】2017年拜访三亚回辉人.md](content/【清真旅行回顾】2017年拜访三亚回辉人.md) | 【清真旅行回顾】2017年拜访三亚回辉人... | [Source](https://salaamalykum.com/cn/article/1821) | `fb85cfc2...` |
| [【清真旅行回顾】2017年的北京常营.md](content/【清真旅行回顾】2017年的北京常营.md) | 【清真旅行回顾】2017年的北京常营... | [Source](https://salaamalykum.com/cn/article/1794) | `6101b04c...` |
| [【清真旅行回顾】2017年的北京朝外关厢.md](content/【清真旅行回顾】2017年的北京朝外关厢.md) | 【清真旅行回顾】2017年的北京朝外关厢... | [Source](https://salaamalykum.com/cn/article/1795) | `ee7a0490...` |
| [【清真旅行回顾】2017年的天津佳园里.md](content/【清真旅行回顾】2017年的天津佳园里.md) | 【清真旅行回顾】2017年的天津佳园里... | [Source](https://salaamalykum.com/cn/article/1809) | `3552e961...` |
| [【清真旅行回顾】2017年的山东临清.md](content/【清真旅行回顾】2017年的山东临清.md) | 【清真旅行回顾】2017年的山东临清... | [Source](https://salaamalykum.com/cn/article/1805) | `c0110795...` |
| [【清真旅行回顾】2017年的山东聊城.md](content/【清真旅行回顾】2017年的山东聊城.md) | 【清真旅行回顾】2017年的山东聊城... | [Source](https://salaamalykum.com/cn/article/1804) | `1be0dab8...` |
| [【清真旅行回顾】2017年的江苏徐州.md](content/【清真旅行回顾】2017年的江苏徐州.md) | 【清真旅行回顾】2017年的江苏徐州... | [Source](https://salaamalykum.com/cn/article/1802) | `17b0b530...` |
| [【清真旅行回顾】2017年的江苏扬州.md](content/【清真旅行回顾】2017年的江苏扬州.md) | 【清真旅行回顾】2017年的江苏扬州... | [Source](https://salaamalykum.com/cn/article/1799) | `65ad69cc...` |
| [【清真旅行回顾】2017年的江苏镇江.md](content/【清真旅行回顾】2017年的江苏镇江.md) | 【清真旅行回顾】2017年的江苏镇江... | [Source](https://salaamalykum.com/cn/article/1798) | `8845f9e1...` |
| [【清真旅行回顾】2017年的河北泊头.md](content/【清真旅行回顾】2017年的河北泊头.md) | 【清真旅行回顾】2017年的河北泊头... | [Source](https://salaamalykum.com/cn/article/1807) | `37e45372...` |
| [【清真旅行回顾】2017年的浙江嘉兴.md](content/【清真旅行回顾】2017年的浙江嘉兴.md) | 【清真旅行回顾】2017年的浙江嘉兴... | [Source](https://salaamalykum.com/cn/article/1797) | `6a44fa05...` |
| [【清真旅行回顾】2018年的乌鲁木齐，美丽的大湾.md](content/【清真旅行回顾】2018年的乌鲁木齐，美丽的大湾.md) | 【清真旅行回顾】2018年的乌鲁木齐，美丽的大湾... | [Source](https://salaamalykum.com/cn/article/1792) | `5598950e...` |
| [【清真旅行回顾】韩国首尔.md](content/【清真旅行回顾】韩国首尔.md) | 【清真旅行回顾】韩国首尔... | [Source](https://salaamalykum.com/cn/article/1825) | `890e5309...` |
| [【看展记】国博上合展：潇洒的波斯体书法与华丽的中亚长袍.md](content/【看展记】国博上合展：潇洒的波斯体书法与华丽的中亚长袍.md) | 【看展记】国博上合展：潇洒的波斯体书法与华丽的中亚长袍... | [Source](https://salaamalykum.com/cn/article/1478) | `c56133f0...` |
| [【看展记】国博沙特当代艺术展：荒原上的清真寺.md](content/【看展记】国博沙特当代艺术展：荒原上的清真寺.md) | 【看展记】国博沙特当代艺术展：荒原上的清真寺... | [Source](https://salaamalykum.com/cn/article/1477) | `7402fa02...` |
| [【看展记】天津博物馆哈萨克斯坦国博馆藏历史文物展.md](content/【看展记】天津博物馆哈萨克斯坦国博馆藏历史文物展.md) | 【看展记】天津博物馆哈萨克斯坦国博馆藏历史文物展... | [Source](https://salaamalykum.com/cn/article/1607) | `4767c703...` |
| [【看展记】故宫午门中国与西亚古代文明交流展.md](content/【看展记】故宫午门中国与西亚古代文明交流展.md) | 【看展记】故宫午门中国与西亚古代文明交流展... | [Source](https://salaamalykum.com/cn/article/1686) | `caeff4be...` |
| [【看展记】故宫午门伊朗文物精华展（上篇）.md](content/【看展记】故宫午门伊朗文物精华展（上篇）.md) | 【看展记】故宫午门伊朗文物精华展（上篇）... | [Source](https://salaamalykum.com/cn/article/1687) | `4f46c93d...` |
| [【看展记】故宫午门伊朗文物精华展（下篇）.md](content/【看展记】故宫午门伊朗文物精华展（下篇）.md) | 【看展记】故宫午门伊朗文物精华展（下篇）... | [Source](https://salaamalykum.com/cn/article/1688) | `3a3d13ff...` |
| [【看展记】故宫午门沙特埃尔奥拉展.md](content/【看展记】故宫午门沙特埃尔奥拉展.md) | 【看展记】故宫午门沙特埃尔奥拉展... | [Source](https://salaamalykum.com/cn/article/1685) | `f33a26f6...` |
| [【看展记】沙特国博钱币特展.md](content/【看展记】沙特国博钱币特展.md) | 【看展记】沙特国博钱币特展... | [Source](https://salaamalykum.com/cn/article/1409) | `5bc21e1e...` |
| [【看展记】清华艺博古代陶瓷展.md](content/【看展记】清华艺博古代陶瓷展.md) | 【看展记】清华艺博古代陶瓷展... | [Source](https://salaamalykum.com/cn/article/1680) | `384c6d55...` |
| [【看展记】砂拉越回教历史博物馆（上篇）.md](content/【看展记】砂拉越回教历史博物馆（上篇）.md) | 【看展记】砂拉越回教历史博物馆（上篇）... | [Source](https://salaamalykum.com/cn/article/1571) | `ea6f1e62...` |
| [【看展记】砂拉越回教历史博物馆（下篇）.md](content/【看展记】砂拉越回教历史博物馆（下篇）.md) | 【看展记】砂拉越回教历史博物馆（下篇）... | [Source](https://salaamalykum.com/cn/article/1572) | `54793ffd...` |
| [【看展记】越南民族学博物馆藏教门文物.md](content/【看展记】越南民族学博物馆藏教门文物.md) | 【看展记】越南民族学博物馆藏教门文物... | [Source](https://salaamalykum.com/cn/article/1433) | `1cb03157...` |
| [【看展记】越南民族学博物馆藏爪哇玻璃画.md](content/【看展记】越南民族学博物馆藏爪哇玻璃画.md) | 【看展记】越南民族学博物馆藏爪哇玻璃画... | [Source](https://salaamalykum.com/cn/article/1442) | `bfb5c1e1...` |
| [一半工作，一半信仰.md](content/一半工作，一半信仰.md) | 一半工作，一半信仰... | [Source](https://salaamalykum.com/cn/article/1281) | `42792763...` |
| [一战导火索与奥匈帝国统治下的萨拉热窝.md](content/一战导火索与奥匈帝国统治下的萨拉热窝.md) | 一战导火索与奥匈帝国统治下的萨拉热窝... | [Source](https://salaamalykum.com/cn/article/1734) | `384e0141...` |
| [世界各地的手抄经（上篇）.md](content/世界各地的手抄经（上篇）.md) | 世界各地的手抄经（上篇）... | [Source](https://salaamalykum.com/cn/article/1830) | `5f402727...` |
| [世界各地的手抄经（下篇）.md](content/世界各地的手抄经（下篇）.md) | 世界各地的手抄经（下篇）... | [Source](https://salaamalykum.com/cn/article/1831) | `d8ab2f40...` |
| [东南亚的第一个苏丹国——马六甲.md](content/东南亚的第一个苏丹国——马六甲.md) | 东南亚的第一个苏丹国——马六甲... | [Source](https://salaamalykum.com/cn/article/1865) | `3c8a41bd...` |
| [乌兹别克斯坦应用艺术博物馆.md](content/乌兹别克斯坦应用艺术博物馆.md) | 乌兹别克斯坦应用艺术博物馆... | [Source](https://salaamalykum.com/cn/article/1923) | `56e8ad0d...` |
| [乾隆皇帝的伊斯俩目头盔和波斯弯刀.md](content/乾隆皇帝的伊斯俩目头盔和波斯弯刀.md) | 乾隆皇帝的伊斯俩目头盔和波斯弯刀... | [Source](https://salaamalykum.com/cn/article/2006) | `5906403e...` |
| [二十世纪最有影响力的圣训学家穆罕默德·纳斯尔丁·艾勒巴尼.md](content/二十世纪最有影响力的圣训学家穆罕默德·纳斯尔丁·艾勒巴尼.md) | 二十世纪最有影响力的圣训学家穆罕默德·纳斯尔丁·艾勒巴尼... | [Source](https://salaamalykum.com/cn/article/1291) | `7dfe180c...` |
| [从山中城堡到水村民居——文莱历史文化之旅（上篇）.md](content/从山中城堡到水村民居——文莱历史文化之旅（上篇）.md) | 从山中城堡到水村民居——文莱历史文化之旅（上篇）... | [Source](https://salaamalykum.com/cn/article/1579) | `3afd212f...` |
| [从山中城堡到水村民居——文莱历史文化之旅（下篇）.md](content/从山中城堡到水村民居——文莱历史文化之旅（下篇）.md) | 从山中城堡到水村民居——文莱历史文化之旅（下篇）... | [Source](https://salaamalykum.com/cn/article/1580) | `506a44a2...` |
| [伊斯坦布尔不眠夜.md](content/伊斯坦布尔不眠夜.md) | 伊斯坦布尔不眠夜... | [Source](https://salaamalykum.com/cn/article/1728) | `63908ee2...` |
| [伊斯坦布尔伊斯俩目艺术博物馆.md](content/伊斯坦布尔伊斯俩目艺术博物馆.md) | 伊斯坦布尔伊斯俩目艺术博物馆... | [Source](https://salaamalykum.com/cn/article/1858) | `451c18e8...` |
| [伊斯坦布尔的奥斯曼早期建筑.md](content/伊斯坦布尔的奥斯曼早期建筑.md) | 伊斯坦布尔的奥斯曼早期建筑... | [Source](https://salaamalykum.com/cn/article/1813) | `4f3949bd...` |
| [伊斯坦布尔逛吃记.md](content/伊斯坦布尔逛吃记.md) | 伊斯坦布尔逛吃记... | [Source](https://salaamalykum.com/cn/article/1843) | `b2e32acd...` |
| [伊朗为什么选择了什叶派？.md](content/伊朗为什么选择了什叶派？.md) | 伊朗为什么选择了什叶派？... | [Source](https://salaamalykum.com/cn/article/1290) | `9f413875...` |
| [伊朗伊斯兰时代博物馆看展记（上篇）.md](content/伊朗伊斯兰时代博物馆看展记（上篇）.md) | 伊朗伊斯兰时代博物馆看展记（上篇）... | [Source](https://salaamalykum.com/cn/article/2098) | `576a5ba1...` |
| [伊朗伊斯兰时代博物馆看展记（下篇）.md](content/伊朗伊斯兰时代博物馆看展记（下篇）.md) | 伊朗伊斯兰时代博物馆看展记（下篇）... | [Source](https://salaamalykum.com/cn/article/2099) | `c92f88f4...` |
| [伊朗恺加王朝的宫殿——古列斯坦王宫.md](content/伊朗恺加王朝的宫殿——古列斯坦王宫.md) | 伊朗恺加王朝的宫殿——古列斯坦王宫... | [Source](https://salaamalykum.com/cn/article/1977) | `8ab3982d...` |
| [伏尔加河畔的千年穆斯林古都——保加尔.md](content/伏尔加河畔的千年穆斯林古都——保加尔.md) | 伏尔加河畔的千年穆斯林古都——保加尔... | [Source](https://salaamalykum.com/cn/article/2004) | `8cfe4d10...` |
| [住在历史遗产酒店.md](content/住在历史遗产酒店.md) | 住在历史遗产酒店... | [Source](https://salaamalykum.com/cn/article/1648) | `806cd711...` |
| [俄罗斯国家东方艺术博物馆.md](content/俄罗斯国家东方艺术博物馆.md) | 俄罗斯国家东方艺术博物馆... | [Source](https://salaamalykum.com/cn/article/1857) | `32faeac3...` |
| [保利艺术博物馆瓷器展上的回伊文物.md](content/保利艺术博物馆瓷器展上的回伊文物.md) | 保利艺术博物馆瓷器展上的回伊文物... | [Source](https://salaamalykum.com/cn/article/2011) | `e488511f...` |
| [免签一日游遍新加坡.md](content/免签一日游遍新加坡.md) | 免签一日游遍新加坡... | [Source](https://salaamalykum.com/cn/article/1332) | `c2788afc...` |
| [内蒙草原上的回民重镇——多伦.md](content/内蒙草原上的回民重镇——多伦.md) | 内蒙草原上的回民重镇——多伦... | [Source](https://salaamalykum.com/cn/article/1509) | `477acb6a...` |
| [农历三月二十四，北京昌平何营筛海巴巴坟.md](content/农历三月二十四，北京昌平何营筛海巴巴坟.md) | 农历三月二十四，北京昌平何营筛海巴巴坟... | [Source](https://salaamalykum.com/cn/article/1363) | `369e86ac...` |
| [分享106种不同风格的泰斯米写法.md](content/分享106种不同风格的泰斯米写法.md) | 分享106种不同风格的泰斯米写法... | [Source](https://salaamalykum.com/cn/article/1542) | `3a5fd4c1...` |
| [分享131座中国传统米哈拉布（上篇）.md](content/分享131座中国传统米哈拉布（上篇）.md) | 分享131座中国传统米哈拉布（上篇）... | [Source](https://salaamalykum.com/cn/article/1534) | `608adb8f...` |
| [分享131座中国传统米哈拉布（下篇）.md](content/分享131座中国传统米哈拉布（下篇）.md) | 分享131座中国传统米哈拉布（下篇）... | [Source](https://salaamalykum.com/cn/article/1535) | `32df52eb...` |
| [北京中轴线世遗缓冲区内的教门文物古迹.md](content/北京中轴线世遗缓冲区内的教门文物古迹.md) | 北京中轴线世遗缓冲区内的教门文物古迹... | [Source](https://salaamalykum.com/cn/article/1421) | `58858025...` |
| [北京四座博物馆中的伊斯俩目文物.md](content/北京四座博物馆中的伊斯俩目文物.md) | 北京四座博物馆中的伊斯俩目文物... | [Source](https://salaamalykum.com/cn/article/1893) | `9644d5bc...` |
| [北京圣纪月第一周：东四、八里庄、杨闸.md](content/北京圣纪月第一周：东四、八里庄、杨闸.md) | 北京圣纪月第一周：东四、八里庄、杨闸... | [Source](https://salaamalykum.com/cn/article/1480) | `1ddc12c3...` |
| [北京圣纪月第三周：南下坡、通州西关.md](content/北京圣纪月第三周：南下坡、通州西关.md) | 北京圣纪月第三周：南下坡、通州西关... | [Source](https://salaamalykum.com/cn/article/1471) | `d07afe7a...` |
| [北京圣纪月第二周：三里河、西会.md](content/北京圣纪月第二周：三里河、西会.md) | 北京圣纪月第二周：三里河、西会... | [Source](https://salaamalykum.com/cn/article/1475) | `2befcb97...` |
| [北京怀柔清真之旅.md](content/北京怀柔清真之旅.md) | 北京怀柔清真之旅... | [Source](https://salaamalykum.com/cn/article/1879) | `97cb6778...` |
| [南印度德干高原上的穆斯林国家——阿萨夫贾王朝.md](content/南印度德干高原上的穆斯林国家——阿萨夫贾王朝.md) | 南印度德干高原上的穆斯林国家——阿萨夫贾王朝... | [Source](https://salaamalykum.com/cn/article/1869) | `4d6507b2...` |
| [南印度穆斯林古都——海德拉巴.md](content/南印度穆斯林古都——海德拉巴.md) | 南印度穆斯林古都——海德拉巴... | [Source](https://salaamalykum.com/cn/article/1880) | `da6cd122...` |
| [印尼最后的苏丹领土——日惹.md](content/印尼最后的苏丹领土——日惹.md) | 印尼最后的苏丹领土——日惹... | [Source](https://salaamalykum.com/cn/article/1872) | `9b715c69...` |
| [厦门大学人类学博物馆藏宋元教门石刻.md](content/厦门大学人类学博物馆藏宋元教门石刻.md) | 厦门大学人类学博物馆藏宋元教门石刻... | [Source](https://salaamalykum.com/cn/article/1664) | `db9737dc...` |
| [去北海公园看回回营清真寺.md](content/去北海公园看回回营清真寺.md) | 去北海公园看回回营清真寺... | [Source](https://salaamalykum.com/cn/article/2017) | `08e4b727...` |
| [去潘家园看精美的明正德阿文炉瓶三事.md](content/去潘家园看精美的明正德阿文炉瓶三事.md) | 去潘家园看精美的明正德阿文炉瓶三事... | [Source](https://salaamalykum.com/cn/article/2010) | `1b403e77...` |
| [古晋的清真中餐与百年老宅民宿.md](content/古晋的清真中餐与百年老宅民宿.md) | 古晋的清真中餐与百年老宅民宿... | [Source](https://salaamalykum.com/cn/article/1552) | `0d0e05ae...` |
| [吃喝玩乐保平安.md](content/吃喝玩乐保平安.md) | 吃喝玩乐保平安... | [Source](https://salaamalykum.com/cn/article/1234) | `34530e40...` |
| [各地清真小吃荟萃（中国西部篇）（上篇）.md](content/各地清真小吃荟萃（中国西部篇）（上篇）.md) | 各地清真小吃荟萃（中国西部篇）（上篇）... | [Source](https://salaamalykum.com/cn/article/1951) | `fb71f17a...` |
| [各地清真小吃荟萃（中国西部篇）（下篇）.md](content/各地清真小吃荟萃（中国西部篇）（下篇）.md) | 各地清真小吃荟萃（中国西部篇）（下篇）... | [Source](https://salaamalykum.com/cn/article/1953) | `beba1551...` |
| [各地清真小吃荟萃（中国西部篇）（中篇）.md](content/各地清真小吃荟萃（中国西部篇）（中篇）.md) | 各地清真小吃荟萃（中国西部篇）（中篇）... | [Source](https://salaamalykum.com/cn/article/1952) | `d34c7821...` |
| [品尝新加坡的清真中餐.md](content/品尝新加坡的清真中餐.md) | 品尝新加坡的清真中餐... | [Source](https://salaamalykum.com/cn/article/1703) | `23bddd0d...` |
| [喀山克里姆林宫与鞑靼斯坦国家博物馆.md](content/喀山克里姆林宫与鞑靼斯坦国家博物馆.md) | 喀山克里姆林宫与鞑靼斯坦国家博物馆... | [Source](https://salaamalykum.com/cn/article/1909) | `0fb5de1d...` |
| [嘎德忍耶太师祖的归真之地——鹿龄寺.md](content/嘎德忍耶太师祖的归真之地——鹿龄寺.md) | 嘎德忍耶太师祖的归真之地——鹿龄寺... | [Source](https://salaamalykum.com/cn/article/1299) | `d4af7a79...` |
| [四川孝泉古镇回民半边街.md](content/四川孝泉古镇回民半边街.md) | 四川孝泉古镇回民半边街... | [Source](https://salaamalykum.com/cn/article/1489) | `861dae95...` |
| [回忆中的北京安河桥清真寺.md](content/回忆中的北京安河桥清真寺.md) | 回忆中的北京安河桥清真寺... | [Source](https://salaamalykum.com/cn/article/1065) | `90d1090e...` |
| [圆明园中的清真寺.md](content/圆明园中的清真寺.md) | 圆明园中的清真寺... | [Source](https://salaamalykum.com/cn/article/1891) | `a20d47b1...` |
| [土耳其与伊斯兰艺术博物馆.md](content/土耳其与伊斯兰艺术博物馆.md) | 土耳其与伊斯兰艺术博物馆... | [Source](https://salaamalykum.com/cn/article/2094) | `bb447684...` |
| [土耳其东南部的库尔德之城——迪亚巴克尔.md](content/土耳其东南部的库尔德之城——迪亚巴克尔.md) | 土耳其东南部的库尔德之城——迪亚巴克尔... | [Source](https://salaamalykum.com/cn/article/1745) | `0b9cfa44...` |
| [土耳其埃迪尔内、布尔萨、科尼亚美食之旅.md](content/土耳其埃迪尔内、布尔萨、科尼亚美食之旅.md) | 土耳其埃迪尔内、布尔萨、科尼亚美食之旅... | [Source](https://salaamalykum.com/cn/article/1975) | `8a80de24...` |
| [在上海品读波斯苏菲诗歌.md](content/在上海品读波斯苏菲诗歌.md) | 在上海品读波斯苏菲诗歌... | [Source](https://salaamalykum.com/cn/article/1394) | `df7b31a2...` |
| [在丛峰导演那儿淘的穆斯林音乐唱片.md](content/在丛峰导演那儿淘的穆斯林音乐唱片.md) | 在丛峰导演那儿淘的穆斯林音乐唱片... | [Source](https://salaamalykum.com/cn/article/1945) | `b45ee5fd...` |
| [在伊斯坦布尔新机场逛博物馆.md](content/在伊斯坦布尔新机场逛博物馆.md) | 在伊斯坦布尔新机场逛博物馆... | [Source](https://salaamalykum.com/cn/article/1755) | `8f6b38e7...` |
| [在伊斯坦布尔遇见19世纪的奥斯曼王朝.md](content/在伊斯坦布尔遇见19世纪的奥斯曼王朝.md) | 在伊斯坦布尔遇见19世纪的奥斯曼王朝... | [Source](https://salaamalykum.com/cn/article/1723) | `afd2043a...` |
| [在北京参加波斯历新年——诺鲁孜节.md](content/在北京参加波斯历新年——诺鲁孜节.md) | 在北京参加波斯历新年——诺鲁孜节... | [Source](https://salaamalykum.com/cn/article/1382) | `1cf2ad26...` |
| [在塔吉克斯坦的粟特古城.md](content/在塔吉克斯坦的粟特古城.md) | 在塔吉克斯坦的粟特古城... | [Source](https://salaamalykum.com/cn/article/1982) | `887fa948...` |
| [在寻甸塘子清真寺礼主麻.md](content/在寻甸塘子清真寺礼主麻.md) | 在寻甸塘子清真寺礼主麻... | [Source](https://salaamalykum.com/cn/article/2050) | `f199f77e...` |
| [在故宫遇到波斯诗歌——武英殿陶瓷馆看展记.md](content/在故宫遇到波斯诗歌——武英殿陶瓷馆看展记.md) | 在故宫遇到波斯诗歌——武英殿陶瓷馆看展记... | [Source](https://salaamalykum.com/cn/article/2110) | `53f69b8a...` |
| [在梅赫劳利考古公园感受印度伊斯俩目千年历史（上篇）.md](content/在梅赫劳利考古公园感受印度伊斯俩目千年历史（上篇）.md) | 在梅赫劳利考古公园感受印度伊斯俩目千年历史（上篇）... | [Source](https://salaamalykum.com/cn/article/1826) | `73ea75ce...` |
| [在梅赫劳利考古公园感受印度伊斯俩目千年历史（下篇）.md](content/在梅赫劳利考古公园感受印度伊斯俩目千年历史（下篇）.md) | 在梅赫劳利考古公园感受印度伊斯俩目千年历史（下篇）... | [Source](https://salaamalykum.com/cn/article/1827) | `303e5619...` |
| [在泰国曼谷感受波斯裔什叶派节日氛围.md](content/在泰国曼谷感受波斯裔什叶派节日氛围.md) | 在泰国曼谷感受波斯裔什叶派节日氛围... | [Source](https://salaamalykum.com/cn/article/1496) | `2fe44c0b...` |
| [在洛迪花园感受德里苏丹国晚期历史.md](content/在洛迪花园感受德里苏丹国晚期历史.md) | 在洛迪花园感受德里苏丹国晚期历史... | [Source](https://salaamalykum.com/cn/article/1822) | `a5715372...` |
| [在萨拉热窝纪念波黑战争.md](content/在萨拉热窝纪念波黑战争.md) | 在萨拉热窝纪念波黑战争... | [Source](https://salaamalykum.com/cn/article/1733) | `14e20850...` |
| [在马来西亚品尝清真中餐（上篇）.md](content/在马来西亚品尝清真中餐（上篇）.md) | 在马来西亚品尝清真中餐（上篇）... | [Source](https://salaamalykum.com/cn/article/1700) | `beaf399f...` |
| [在马来西亚品尝清真中餐（下篇）.md](content/在马来西亚品尝清真中餐（下篇）.md) | 在马来西亚品尝清真中餐（下篇）... | [Source](https://salaamalykum.com/cn/article/1701) | `f001bdb6...` |
| [埃及文明国家博物馆.md](content/埃及文明国家博物馆.md) | 埃及文明国家博物馆... | [Source](https://salaamalykum.com/cn/article/1722) | `0262cdc7...` |
| [埃尔米塔日博物馆收藏的伊朗、中亚文物.md](content/埃尔米塔日博物馆收藏的伊朗、中亚文物.md) | 埃尔米塔日博物馆收藏的伊朗、中亚文物... | [Source](https://salaamalykum.com/cn/article/1920) | `d5d7c840...` |
| [塔吉克斯坦苦盏城的夜晚.md](content/塔吉克斯坦苦盏城的夜晚.md) | 塔吉克斯坦苦盏城的夜晚... | [Source](https://salaamalykum.com/cn/article/1981) | `e5be4004...` |
| [塞尔柱王朝最后的国都——科尼亚（上篇）.md](content/塞尔柱王朝最后的国都——科尼亚（上篇）.md) | 塞尔柱王朝最后的国都——科尼亚（上篇）... | [Source](https://salaamalykum.com/cn/article/1996) | `55a7c5e4...` |
| [塞尔柱王朝最后的国都——科尼亚（下篇）.md](content/塞尔柱王朝最后的国都——科尼亚（下篇）.md) | 塞尔柱王朝最后的国都——科尼亚（下篇）... | [Source](https://salaamalykum.com/cn/article/1997) | `a4c63a54...` |
| [复原奥斯曼王朝统治下19世纪波斯尼亚克人的生活.md](content/复原奥斯曼王朝统治下19世纪波斯尼亚克人的生活.md) | 复原奥斯曼王朝统治下19世纪波斯尼亚克人的生活... | [Source](https://salaamalykum.com/cn/article/1712) | `9a806db2...` |
| [夏天带娃回老家——天津河西务.md](content/夏天带娃回老家——天津河西务.md) | 夏天带娃回老家——天津河西务... | [Source](https://salaamalykum.com/cn/article/1486) | `25a6bf2a...` |
| [夏日呼和浩特清真逛吃.md](content/夏日呼和浩特清真逛吃.md) | 夏日呼和浩特清真逛吃... | [Source](https://salaamalykum.com/cn/article/2097) | `6b6acdf7...` |
| [外国图书馆里的古热阿尼手稿.md](content/外国图书馆里的古热阿尼手稿.md) | 外国图书馆里的古热阿尼手稿... | [Source](https://salaamalykum.com/cn/article/1910) | `b3134026...` |
| [多元融合的曼谷穆斯林社区.md](content/多元融合的曼谷穆斯林社区.md) | 多元融合的曼谷穆斯林社区... | [Source](https://salaamalykum.com/cn/article/1765) | `bd0fee5e...` |
| [奥斯曼伟大的建筑师——米玛希南（上）：成长篇.md](content/奥斯曼伟大的建筑师——米玛希南（上）：成长篇.md) | 奥斯曼伟大的建筑师——米玛希南（上）：成长篇... | [Source](https://salaamalykum.com/cn/article/1868) | `b9c30087...` |
| [奥斯曼伟大的建筑师——米玛希南（下）：巅峰篇.md](content/奥斯曼伟大的建筑师——米玛希南（下）：巅峰篇.md) | 奥斯曼伟大的建筑师——米玛希南（下）：巅峰篇... | [Source](https://salaamalykum.com/cn/article/1820) | `666b57a2...` |
| [奥斯曼伟大的建筑师——米玛希南（中）：成熟篇（上篇）.md](content/奥斯曼伟大的建筑师——米玛希南（中）：成熟篇（上篇）.md) | 奥斯曼伟大的建筑师——米玛希南（中）：成熟篇（上篇）... | [Source](https://salaamalykum.com/cn/article/1860) | `aab181f3...` |
| [奥斯曼伟大的建筑师——米玛希南（中）：成熟篇（下篇）.md](content/奥斯曼伟大的建筑师——米玛希南（中）：成熟篇（下篇）.md) | 奥斯曼伟大的建筑师——米玛希南（中）：成熟篇（下篇）... | [Source](https://salaamalykum.com/cn/article/1861) | `e301f3db...` |
| [奥斯曼帝国的宫殿——托普卡珀皇宫.md](content/奥斯曼帝国的宫殿——托普卡珀皇宫.md) | 奥斯曼帝国的宫殿——托普卡珀皇宫... | [Source](https://salaamalykum.com/cn/article/1866) | `8d74d059...` |
| [奥斯曼建筑史上的巅峰之作——埃迪尔内塞利米耶清真寺.md](content/奥斯曼建筑史上的巅峰之作——埃迪尔内塞利米耶清真寺.md) | 奥斯曼建筑史上的巅峰之作——埃迪尔内塞利米耶清真寺... | [Source](https://salaamalykum.com/cn/article/2029) | `84649e02...` |
| [奥斯曼王朝的欧洲之城——萨拉热窝（上篇）.md](content/奥斯曼王朝的欧洲之城——萨拉热窝（上篇）.md) | 奥斯曼王朝的欧洲之城——萨拉热窝（上篇）... | [Source](https://salaamalykum.com/cn/article/1710) | `34c58372...` |
| [奥斯曼王朝的欧洲之城——萨拉热窝（下篇）.md](content/奥斯曼王朝的欧洲之城——萨拉热窝（下篇）.md) | 奥斯曼王朝的欧洲之城——萨拉热窝（下篇）... | [Source](https://salaamalykum.com/cn/article/1711) | `f32b5f3f...` |
| [奥斯曼的欧洲之都——埃迪尔内（上篇）.md](content/奥斯曼的欧洲之都——埃迪尔内（上篇）.md) | 奥斯曼的欧洲之都——埃迪尔内（上篇）... | [Source](https://salaamalykum.com/cn/article/1993) | `a8940db3...` |
| [奥斯曼的欧洲之都——埃迪尔内（下篇）.md](content/奥斯曼的欧洲之都——埃迪尔内（下篇）.md) | 奥斯曼的欧洲之都——埃迪尔内（下篇）... | [Source](https://salaamalykum.com/cn/article/1994) | `5591928d...` |
| [寻访后海清真寺的民国小楼.md](content/寻访后海清真寺的民国小楼.md) | 寻访后海清真寺的民国小楼... | [Source](https://salaamalykum.com/cn/article/1862) | `94a3493a...` |
| [广东肇庆的清真烧鹅与寺里的杨桃.md](content/广东肇庆的清真烧鹅与寺里的杨桃.md) | 广东肇庆的清真烧鹅与寺里的杨桃... | [Source](https://salaamalykum.com/cn/article/1787) | `24ae6c81...` |
| [库尔德人、阿拉伯人与亚述人共同生活的岩石山城——马尔丁食宿篇（上篇）.md](content/库尔德人、阿拉伯人与亚述人共同生活的岩石山城——马尔丁食宿篇（上篇）.md) | 库尔德人、阿拉伯人与亚述人共同生活的岩石山城——马尔丁食宿篇... | [Source](https://salaamalykum.com/cn/article/1753) | `8907cc46...` |
| [库尔德人、阿拉伯人与亚述人共同生活的岩石山城——马尔丁食宿篇（下篇）.md](content/库尔德人、阿拉伯人与亚述人共同生活的岩石山城——马尔丁食宿篇（下篇）.md) | 库尔德人、阿拉伯人与亚述人共同生活的岩石山城——马尔丁食宿篇... | [Source](https://salaamalykum.com/cn/article/1754) | `e8071a88...` |
| [底格里斯河畔的千年古城——迪亚巴克尔（上篇）.md](content/底格里斯河畔的千年古城——迪亚巴克尔（上篇）.md) | 底格里斯河畔的千年古城——迪亚巴克尔（上篇）... | [Source](https://salaamalykum.com/cn/article/1740) | `8203e435...` |
| [底格里斯河畔的千年古城——迪亚巴克尔（下篇）.md](content/底格里斯河畔的千年古城——迪亚巴克尔（下篇）.md) | 底格里斯河畔的千年古城——迪亚巴克尔（下篇）... | [Source](https://salaamalykum.com/cn/article/1741) | `070c5691...` |
| [开封的寺门汤锅与清真夜市.md](content/开封的寺门汤锅与清真夜市.md) | 开封的寺门汤锅与清真夜市... | [Source](https://salaamalykum.com/cn/article/2041) | `8c69312e...` |
| [德干高原上的穆斯林古城——戈尔康达堡（上篇）.md](content/德干高原上的穆斯林古城——戈尔康达堡（上篇）.md) | 德干高原上的穆斯林古城——戈尔康达堡（上篇）... | [Source](https://salaamalykum.com/cn/article/1882) | `f490e2d9...` |
| [德干高原上的穆斯林古城——戈尔康达堡（下篇）.md](content/德干高原上的穆斯林古城——戈尔康达堡（下篇）.md) | 德干高原上的穆斯林古城——戈尔康达堡（下篇）... | [Source](https://salaamalykum.com/cn/article/1883) | `235d33a5...` |
| [德里的第六座城——莫卧儿王朝的诞生.md](content/德里的第六座城——莫卧儿王朝的诞生.md) | 德里的第六座城——莫卧儿王朝的诞生... | [Source](https://salaamalykum.com/cn/article/1885) | `0aff250c...` |
| [德里的第四座城——神秘的苏丹宫殿.md](content/德里的第四座城——神秘的苏丹宫殿.md) | 德里的第四座城——神秘的苏丹宫殿... | [Source](https://salaamalykum.com/cn/article/1988) | `2c9e4222...` |
| [德里老城的穆斯林社区（上篇）.md](content/德里老城的穆斯林社区（上篇）.md) | 德里老城的穆斯林社区（上篇）... | [Source](https://salaamalykum.com/cn/article/1966) | `b47cde6a...` |
| [德里老城的穆斯林社区（下篇）.md](content/德里老城的穆斯林社区（下篇）.md) | 德里老城的穆斯林社区（下篇）... | [Source](https://salaamalykum.com/cn/article/1967) | `5a274738...` |
| [德里郊外的苏菲圣地和穆斯林社区（上篇）.md](content/德里郊外的苏菲圣地和穆斯林社区（上篇）.md) | 德里郊外的苏菲圣地和穆斯林社区（上篇）... | [Source](https://salaamalykum.com/cn/article/1964) | `d70d55cc...` |
| [德里郊外的苏菲圣地和穆斯林社区（下篇）.md](content/德里郊外的苏菲圣地和穆斯林社区（下篇）.md) | 德里郊外的苏菲圣地和穆斯林社区（下篇）... | [Source](https://salaamalykum.com/cn/article/1965) | `4e5173e8...` |
| [德黑兰的礼萨·阿巴斯博物馆.md](content/德黑兰的礼萨·阿巴斯博物馆.md) | 德黑兰的礼萨·阿巴斯博物馆... | [Source](https://salaamalykum.com/cn/article/1906) | `21f8a8a6...` |
| [怀柔山中的清真小院.md](content/怀柔山中的清真小院.md) | 怀柔山中的清真小院... | [Source](https://salaamalykum.com/cn/article/1873) | `0c93c891...` |
| [感受一下80年代的回民绘画.md](content/感受一下80年代的回民绘画.md) | 感受一下80年代的回民绘画... | [Source](https://salaamalykum.com/cn/article/1523) | `c8312be5...` |
| [感受开罗老城的千年历史（北门内）.md](content/感受开罗老城的千年历史（北门内）.md) | 感受开罗老城的千年历史（北门内）... | [Source](https://salaamalykum.com/cn/article/1702) | `45980b30...` |
| [拜访河北承德山谷中的回民村——王家沟.md](content/拜访河北承德山谷中的回民村——王家沟.md) | 拜访河北承德山谷中的回民村——王家沟... | [Source](https://salaamalykum.com/cn/article/1533) | `a3cd4be6...` |
| [拜访西域先贤伯哈智墓.md](content/拜访西域先贤伯哈智墓.md) | 拜访西域先贤伯哈智墓... | [Source](https://salaamalykum.com/cn/article/1900) | `1370f3e6...` |
| [拜访西安北广济街寺文史馆.md](content/拜访西安北广济街寺文史馆.md) | 拜访西安北广济街寺文史馆... | [Source](https://salaamalykum.com/cn/article/1559) | `b3810a97...` |
| [教门匾额楹联欣赏（1-50幅）.md](content/教门匾额楹联欣赏（1-50幅）.md) | 教门匾额楹联欣赏（1-50幅）... | [Source](https://salaamalykum.com/cn/article/1623) | `f4dbab87...` |
| [教门古城巡礼——克里米亚汗国早期都城.md](content/教门古城巡礼——克里米亚汗国早期都城.md) | 教门古城巡礼——克里米亚汗国早期都城... | [Source](https://salaamalykum.com/cn/article/1507) | `7827d8d8...` |
| [教门古城巡礼——克里米亚首都巴赫奇萨莱.md](content/教门古城巡礼——克里米亚首都巴赫奇萨莱.md) | 教门古城巡礼——克里米亚首都巴赫奇萨莱... | [Source](https://salaamalykum.com/cn/article/1506) | `e75dc2b1...` |
| [教门古城巡礼——土耳其埃迪尔内（奥斯曼欧洲首都）.md](content/教门古城巡礼——土耳其埃迪尔内（奥斯曼欧洲首都）.md) | 教门古城巡礼——土耳其埃迪尔内（奥斯曼欧洲首都）... | [Source](https://salaamalykum.com/cn/article/1504) | `d5b4badb...` |
| [教门古城巡礼——土耳其布尔萨（奥斯曼旧都）.md](content/教门古城巡礼——土耳其布尔萨（奥斯曼旧都）.md) | 教门古城巡礼——土耳其布尔萨（奥斯曼旧都）... | [Source](https://salaamalykum.com/cn/article/1503) | `317af725...` |
| [教门古城巡礼——土耳其马尔丁（库尔德悬崖山城）.md](content/教门古城巡礼——土耳其马尔丁（库尔德悬崖山城）.md) | 教门古城巡礼——土耳其马尔丁（库尔德悬崖山城）... | [Source](https://salaamalykum.com/cn/article/1499) | `27836c7a...` |
| [教门古城巡礼——波黑萨拉热窝.md](content/教门古城巡礼——波黑萨拉热窝.md) | 教门古城巡礼——波黑萨拉热窝... | [Source](https://salaamalykum.com/cn/article/1508) | `2f296f96...` |
| [教门古城巡礼：俄罗斯莫斯科.md](content/教门古城巡礼：俄罗斯莫斯科.md) | 教门古城巡礼：俄罗斯莫斯科... | [Source](https://salaamalykum.com/cn/article/1518) | `124c11a7...` |
| [教门古城巡礼：俄罗斯鞑靼斯坦保加尔.md](content/教门古城巡礼：俄罗斯鞑靼斯坦保加尔.md) | 教门古城巡礼：俄罗斯鞑靼斯坦保加尔... | [Source](https://salaamalykum.com/cn/article/1510) | `9448d6f8...` |
| [教门古城巡礼：俄罗斯鞑靼斯坦喀山.md](content/教门古城巡礼：俄罗斯鞑靼斯坦喀山.md) | 教门古城巡礼：俄罗斯鞑靼斯坦喀山... | [Source](https://salaamalykum.com/cn/article/1515) | `8d71b77d...` |
| [教门古城巡礼：黎巴嫩的贝鲁特.md](content/教门古城巡礼：黎巴嫩的贝鲁特.md) | 教门古城巡礼：黎巴嫩的贝鲁特... | [Source](https://salaamalykum.com/cn/article/1520) | `205d3f23...` |
| [教门古城巡礼：黎巴嫩的赛达.md](content/教门古城巡礼：黎巴嫩的赛达.md) | 教门古城巡礼：黎巴嫩的赛达... | [Source](https://salaamalykum.com/cn/article/1522) | `0d814b63...` |
| [教门古城巡礼：黎巴嫩的黎波里.md](content/教门古城巡礼：黎巴嫩的黎波里.md) | 教门古城巡礼：黎巴嫩的黎波里... | [Source](https://salaamalykum.com/cn/article/1526) | `c8521ed4...` |
| [散落在西安回坊深处的三处清代回族民居.md](content/散落在西安回坊深处的三处清代回族民居.md) | 散落在西安回坊深处的三处清代回族民居... | [Source](https://salaamalykum.com/cn/article/1569) | `5c6ae34f...` |
| [文莱免签！深度文化之旅看这里（上篇）.md](content/文莱免签！深度文化之旅看这里（上篇）.md) | 文莱免签！深度文化之旅看这里（上篇）... | [Source](https://salaamalykum.com/cn/article/1561) | `2d8ce463...` |
| [文莱免签！深度文化之旅看这里（下篇）.md](content/文莱免签！深度文化之旅看这里（下篇）.md) | 文莱免签！深度文化之旅看这里（下篇）... | [Source](https://salaamalykum.com/cn/article/1562) | `9dc77107...` |
| [斋月山东访古寺：泰安泰城寺、东寺、下旺寺.md](content/斋月山东访古寺：泰安泰城寺、东寺、下旺寺.md) | 斋月山东访古寺：泰安泰城寺、东寺、下旺寺... | [Source](https://salaamalykum.com/cn/article/1488) | `95b454af...` |
| [新书快讯：一部跨越文明的赞歌——《天方诗经》（衮衣颂）经典再现.md](content/新书快讯：一部跨越文明的赞歌——《天方诗经》（衮衣颂）经典再现.md) | 新书快讯：一部跨越文明的赞歌——《天方诗经》（衮衣颂）经典再... | [Source](https://salaamalykum.com/cn/article/1410) | `9d46aac5...` |
| [新西兰春季之旅（南岛基督城——北岛奥克兰）.md](content/新西兰春季之旅（南岛基督城——北岛奥克兰）.md) | 新西兰春季之旅（南岛基督城——北岛奥克兰）... | [Source](https://salaamalykum.com/cn/article/1311) | `9fa749ad...` |
| [日本真的没有清真寺和穆斯林吗？2024年日本清真旅游实地探访，带你揭开最真实的日本伊斯兰生活现状！.md](content/日本真的没有清真寺和穆斯林吗？2024年日本清真旅游实地探访，带你揭开最真实的日本伊斯兰生活现状！.md) | 日本真的没有清真寺和穆斯林吗？2024年日本清真旅游实地探访... | [Source](https://salaamalykum.com/cn/article/1020) | `88dcba3e...` |
| [旧时清真摘录（北京北城篇）.md](content/旧时清真摘录（北京北城篇）.md) | 旧时清真摘录（北京北城篇）... | [Source](https://salaamalykum.com/cn/article/1840) | `f8867022...` |
| [旧时清真摘录（北京南城篇）.md](content/旧时清真摘录（北京南城篇）.md) | 旧时清真摘录（北京南城篇）... | [Source](https://salaamalykum.com/cn/article/1841) | `7d4c2c5b...` |
| [昆明向南行（五）：沙甸之行.md](content/昆明向南行（五）：沙甸之行.md) | 昆明向南行（五）：沙甸之行... | [Source](https://salaamalykum.com/cn/article/1976) | `ab8a1fef...` |
| [昆明向南行（六）开远大庄清真寺.md](content/昆明向南行（六）开远大庄清真寺.md) | 昆明向南行（六）开远大庄清真寺... | [Source](https://salaamalykum.com/cn/article/1954) | `795144ef...` |
| [春天拜访北京深山里的两家回民民宿.md](content/春天拜访北京深山里的两家回民民宿.md) | 春天拜访北京深山里的两家回民民宿... | [Source](https://salaamalykum.com/cn/article/1364) | `008e25b6...` |
| [曾经的瑞丽缅甸清真街.md](content/曾经的瑞丽缅甸清真街.md) | 曾经的瑞丽缅甸清真街... | [Source](https://salaamalykum.com/cn/article/2106) | `c7ac4cb7...` |
| [来北京常营回族乡赶大集.md](content/来北京常营回族乡赶大集.md) | 来北京常营回族乡赶大集... | [Source](https://salaamalykum.com/cn/article/1525) | `cd0a85fe...` |
| [民国清真寺建筑中的中西结合元素.md](content/民国清真寺建筑中的中西结合元素.md) | 民国清真寺建筑中的中西结合元素... | [Source](https://salaamalykum.com/cn/article/1892) | `a415760b...` |
| [江苏淮安王家营：黄河与盐河间的回民重镇.md](content/江苏淮安王家营：黄河与盐河间的回民重镇.md) | 江苏淮安王家营：黄河与盐河间的回民重镇... | [Source](https://salaamalykum.com/cn/article/1524) | `86fa72e9...` |
| [河南的十四座传统清真寺（上篇）.md](content/河南的十四座传统清真寺（上篇）.md) | 河南的十四座传统清真寺（上篇）... | [Source](https://salaamalykum.com/cn/article/2078) | `c2d66953...` |
| [河南的十四座传统清真寺（下篇）.md](content/河南的十四座传统清真寺（下篇）.md) | 河南的十四座传统清真寺（下篇）... | [Source](https://salaamalykum.com/cn/article/2079) | `fdc22675...` |
| [泉州伊斯兰遗迹（上篇）.md](content/泉州伊斯兰遗迹（上篇）.md) | 泉州伊斯兰遗迹（上篇）... | [Source](https://salaamalykum.com/cn/article/2107) | `1ef23cf1...` |
| [泉州伊斯兰遗迹（下篇）.md](content/泉州伊斯兰遗迹（下篇）.md) | 泉州伊斯兰遗迹（下篇）... | [Source](https://salaamalykum.com/cn/article/2108) | `59d8fee0...` |
| [泉州海交馆藏宋元教门石刻（上篇）.md](content/泉州海交馆藏宋元教门石刻（上篇）.md) | 泉州海交馆藏宋元教门石刻（上篇）... | [Source](https://salaamalykum.com/cn/article/1649) | `29c42241...` |
| [泉州海交馆藏宋元教门石刻（下篇）.md](content/泉州海交馆藏宋元教门石刻（下篇）.md) | 泉州海交馆藏宋元教门石刻（下篇）... | [Source](https://salaamalykum.com/cn/article/1650) | `b53c11b1...` |
| [泉州百崎郭氏回族（上篇）.md](content/泉州百崎郭氏回族（上篇）.md) | 泉州百崎郭氏回族（上篇）... | [Source](https://salaamalykum.com/cn/article/1949) | `7072f28f...` |
| [波斯湾上的博物馆之城——沙迦（上篇）.md](content/波斯湾上的博物馆之城——沙迦（上篇）.md) | 波斯湾上的博物馆之城——沙迦（上篇）... | [Source](https://salaamalykum.com/cn/article/1962) | `fa93f69d...` |
| [波斯湾上的博物馆之城——沙迦（下篇）.md](content/波斯湾上的博物馆之城——沙迦（下篇）.md) | 波斯湾上的博物馆之城——沙迦（下篇）... | [Source](https://salaamalykum.com/cn/article/1963) | `9b62563d...` |
| [泰国曼谷寺坊大全：占族五坊.md](content/泰国曼谷寺坊大全：占族五坊.md) | 泰国曼谷寺坊大全：占族五坊... | [Source](https://salaamalykum.com/cn/article/1497) | `30923eb0...` |
| [泰国曼谷寺坊大全：印尼七坊（水手、商人、园丁）（上篇）.md](content/泰国曼谷寺坊大全：印尼七坊（水手、商人、园丁）（上篇）.md) | 泰国曼谷寺坊大全：印尼七坊（水手、商人、园丁）（上篇）... | [Source](https://salaamalykum.com/cn/article/1490) | `bb45a7e7...` |
| [泰国曼谷寺坊大全：印尼七坊（水手、商人、园丁）（下篇）.md](content/泰国曼谷寺坊大全：印尼七坊（水手、商人、园丁）（下篇）.md) | 泰国曼谷寺坊大全：印尼七坊（水手、商人、园丁）（下篇）... | [Source](https://salaamalykum.com/cn/article/1491) | `2e31910b...` |
| [泰国曼谷寺坊大全：马来六坊、清真宾馆、特色市集.md](content/泰国曼谷寺坊大全：马来六坊、清真宾馆、特色市集.md) | 泰国曼谷寺坊大全：马来六坊、清真宾馆、特色市集... | [Source](https://salaamalykum.com/cn/article/1493) | `ba241d55...` |
| [海南穆斯林的历史（上篇）.md](content/海南穆斯林的历史（上篇）.md) | 海南穆斯林的历史（上篇）... | [Source](https://salaamalykum.com/cn/article/1943) | `dc13e7be...` |
| [海南穆斯林的历史（下篇）.md](content/海南穆斯林的历史（下篇）.md) | 海南穆斯林的历史（下篇）... | [Source](https://salaamalykum.com/cn/article/1944) | `f4adf47a...` |
| [清明大连清真游.md](content/清明大连清真游.md) | 清明大连清真游... | [Source](https://salaamalykum.com/cn/article/1312) | `2e531ea1...` |
| [湖北樊城的穆斯林.md](content/湖北樊城的穆斯林.md) | 湖北樊城的穆斯林... | [Source](https://salaamalykum.com/cn/article/2066) | `d9bac8a9...` |
| [爪哇岛最早的苏丹国——淡目.md](content/爪哇岛最早的苏丹国——淡目.md) | 爪哇岛最早的苏丹国——淡目... | [Source](https://salaamalykum.com/cn/article/2086) | `ee1938c3...` |
| [犹太教、基督教与伊斯兰教如何看待妇女？.md](content/犹太教、基督教与伊斯兰教如何看待妇女？.md) | 犹太教、基督教与伊斯兰教如何看待妇女？... | [Source](https://salaamalykum.com/cn/article/1279) | `0abe3f33...` |
| [环密云水库清真之旅（上篇）.md](content/环密云水库清真之旅（上篇）.md) | 环密云水库清真之旅（上篇）... | [Source](https://salaamalykum.com/cn/article/1876) | `14ffbc17...` |
| [环密云水库清真之旅（下篇）.md](content/环密云水库清真之旅（下篇）.md) | 环密云水库清真之旅（下篇）... | [Source](https://salaamalykum.com/cn/article/1877) | `e88b6987...` |
| [甘肃天水秦州的明代寺院与清代回民宅院.md](content/甘肃天水秦州的明代寺院与清代回民宅院.md) | 甘肃天水秦州的明代寺院与清代回民宅院... | [Source](https://salaamalykum.com/cn/article/1425) | `cda41fdc...` |
| [穆斯林500年前帮助犹太难民的见证——萨拉热窝犹太会堂.md](content/穆斯林500年前帮助犹太难民的见证——萨拉热窝犹太会堂.md) | 穆斯林500年前帮助犹太难民的见证——萨拉热窝犹太会堂... | [Source](https://salaamalykum.com/cn/article/1724) | `2ca756b6...` |
| [穆斯林王朝古城寻访计划暂告完结.md](content/穆斯林王朝古城寻访计划暂告完结.md) | 穆斯林王朝古城寻访计划暂告完结... | [Source](https://salaamalykum.com/cn/article/1864) | `d752e534...` |
| [美索不达米亚平原上的岩石山城——马尔丁古迹篇.md](content/美索不达米亚平原上的岩石山城——马尔丁古迹篇.md) | 美索不达米亚平原上的岩石山城——马尔丁古迹篇... | [Source](https://salaamalykum.com/cn/article/1752) | `f3a0bb34...` |
| [莫卧儿王朝的第一座宏伟皇陵——胡马雍陵.md](content/莫卧儿王朝的第一座宏伟皇陵——胡马雍陵.md) | 莫卧儿王朝的第一座宏伟皇陵——胡马雍陵... | [Source](https://salaamalykum.com/cn/article/1829) | `9ec02988...` |
| [萨拉热窝的波斯尼亚克美食.md](content/萨拉热窝的波斯尼亚克美食.md) | 萨拉热窝的波斯尼亚克美食... | [Source](https://salaamalykum.com/cn/article/1730) | `99c5e01e...` |
| [萨拉赫如何改变利物浦？穆斯林形象与城市认同.md](content/萨拉赫如何改变利物浦？穆斯林形象与城市认同.md) | 萨拉赫如何改变利物浦？穆斯林形象与城市认同... | [Source](https://salaamalykum.com/cn/article/2163) | `5929ce72...` |
| [西安回坊清真逛吃指南.md](content/西安回坊清真逛吃指南.md) | 西安回坊清真逛吃指南... | [Source](https://salaamalykum.com/cn/article/1308) | `8a4fa1a2...` |
| [跨越欧亚大陆的阿舒拉豆粥.md](content/跨越欧亚大陆的阿舒拉豆粥.md) | 跨越欧亚大陆的阿舒拉豆粥... | [Source](https://salaamalykum.com/cn/article/1746) | `72c4a101...` |
| [辽宁三城清真行：凌源、沈阳、开原（上篇）.md](content/辽宁三城清真行：凌源、沈阳、开原（上篇）.md) | 辽宁三城清真行：凌源、沈阳、开原（上篇）... | [Source](https://salaamalykum.com/cn/article/2060) | `d23860d6...` |
| [辽宁三城清真行：凌源、沈阳、开原（下篇）.md](content/辽宁三城清真行：凌源、沈阳、开原（下篇）.md) | 辽宁三城清真行：凌源、沈阳、开原（下篇）... | [Source](https://salaamalykum.com/cn/article/2061) | `b2a9b18b...` |
| [迪拜Al Ras历史街区.md](content/迪拜Al Ras历史街区.md) | 迪拜Al Ras历史街区... | [Source](https://salaamalykum.com/cn/article/1961) | `ca810f3a...` |
| [逛新加坡亚洲文明博物馆.md](content/逛新加坡亚洲文明博物馆.md) | 逛新加坡亚洲文明博物馆... | [Source](https://salaamalykum.com/cn/article/1707) | `40b07cdd...` |
| [重访伊斯坦布尔（上篇）.md](content/重访伊斯坦布尔（上篇）.md) | 重访伊斯坦布尔（上篇）... | [Source](https://salaamalykum.com/cn/article/1735) | `1aed6a7f...` |
| [重访伊斯坦布尔（下篇）.md](content/重访伊斯坦布尔（下篇）.md) | 重访伊斯坦布尔（下篇）... | [Source](https://salaamalykum.com/cn/article/1736) | `dafec185...` |
| [阆中古城的穆斯林.md](content/阆中古城的穆斯林.md) | 阆中古城的穆斯林... | [Source](https://salaamalykum.com/cn/article/2068) | `31088511...` |
| [阿塞拜疆巴库老城中的历史建筑（上篇）.md](content/阿塞拜疆巴库老城中的历史建筑（上篇）.md) | 阿塞拜疆巴库老城中的历史建筑（上篇）... | [Source](https://salaamalykum.com/cn/article/1998) | `d90b7dbf...` |
| [阿塞拜疆巴库老城中的历史建筑（下篇）.md](content/阿塞拜疆巴库老城中的历史建筑（下篇）.md) | 阿塞拜疆巴库老城中的历史建筑（下篇）... | [Source](https://salaamalykum.com/cn/article/1999) | `ac50257b...` |
| [阿舒拉日斋戒：什么是阿舒拉日？它为何如此重要？.md](content/阿舒拉日斋戒：什么是阿舒拉日？它为何如此重要？.md) | 阿舒拉日斋戒：什么是阿舒拉日？它为何如此重要？... | [Source](https://salaamalykum.com/cn/article/2135) | `5205a934...` |
| [阿舒拉豆豆饭.md](content/阿舒拉豆豆饭.md) | 阿舒拉豆豆饭... | [Source](https://salaamalykum.com/cn/article/1995) | `953079ca...` |
| [陕西的十二座传统清真寺（上篇）.md](content/陕西的十二座传统清真寺（上篇）.md) | 陕西的十二座传统清真寺（上篇）... | [Source](https://salaamalykum.com/cn/article/2075) | `f13f8c88...` |
| [陕西的十二座传统清真寺（下篇）.md](content/陕西的十二座传统清真寺（下篇）.md) | 陕西的十二座传统清真寺（下篇）... | [Source](https://salaamalykum.com/cn/article/2076) | `81237ffb...` |
| [青海的九座传统清真寺和三座拱北（第一篇）.md](content/青海的九座传统清真寺和三座拱北（第一篇）.md) | 青海的九座传统清真寺和三座拱北（第一篇）... | [Source](https://salaamalykum.com/cn/article/2080) | `cf71a81c...` |
| [青海的九座传统清真寺和三座拱北（第三篇）.md](content/青海的九座传统清真寺和三座拱北（第三篇）.md) | 青海的九座传统清真寺和三座拱北（第三篇）... | [Source](https://salaamalykum.com/cn/article/2082) | `a26dd2b2...` |
| [青海的九座传统清真寺和三座拱北（第二篇）.md](content/青海的九座传统清真寺和三座拱北（第二篇）.md) | 青海的九座传统清真寺和三座拱北（第二篇）... | [Source](https://salaamalykum.com/cn/article/2081) | `047e7feb...` |
| [青海的九座传统清真寺和三座拱北（第四篇）.md](content/青海的九座传统清真寺和三座拱北（第四篇）.md) | 青海的九座传统清真寺和三座拱北（第四篇）... | [Source](https://salaamalykum.com/cn/article/2083) | `f928e800...` |
| [马来人与新加坡的早期历史.md](content/马来人与新加坡的早期历史.md) | 马来人与新加坡的早期历史... | [Source](https://salaamalykum.com/cn/article/1698) | `e191d398...` |
| [马来文化最浓厚的地区——吉兰丹（上篇）.md](content/马来文化最浓厚的地区——吉兰丹（上篇）.md) | 马来文化最浓厚的地区——吉兰丹（上篇）... | [Source](https://salaamalykum.com/cn/article/1483) | `4fa760fb...` |
| [马来文化最浓厚的地区——吉兰丹（下篇）.md](content/马来文化最浓厚的地区——吉兰丹（下篇）.md) | 马来文化最浓厚的地区——吉兰丹（下篇）... | [Source](https://salaamalykum.com/cn/article/1484) | `9f2823b5...` |
| [马来西亚伊斯俩目艺术博物馆（中国文物篇）.md](content/马来西亚伊斯俩目艺术博物馆（中国文物篇）.md) | 马来西亚伊斯俩目艺术博物馆（中国文物篇）... | [Source](https://salaamalykum.com/cn/article/1849) | `0269f883...` |
| [马来西亚古晋的印度寺与扁担饭.md](content/马来西亚古晋的印度寺与扁担饭.md) | 马来西亚古晋的印度寺与扁担饭... | [Source](https://salaamalykum.com/cn/article/1555) | `3174680d...` |
| [马来西亚教门艺术博物馆的92本手抄经.md](content/马来西亚教门艺术博物馆的92本手抄经.md) | 马来西亚教门艺术博物馆的92本手抄经... | [Source](https://salaamalykum.com/cn/article/1566) | `584ed179...` |
| [马来西亚教门艺术博物馆馆藏精品.md](content/马来西亚教门艺术博物馆馆藏精品.md) | 马来西亚教门艺术博物馆馆藏精品... | [Source](https://salaamalykum.com/cn/article/1563) | `8b0ca9d3...` |



</details>

---

## Official Links
| Platform | URL |
|---|---|
| 🌐 Main Platform | [https://salaamalykum.com](https://salaamalykum.com) |
| 📱 Simplified Chinese | [https://salaamalykum.com/cn](https://salaamalykum.com/cn) |
| 🔬 GitHub Repository | [https://github.com/salaamalykum/Islamic-Culture](https://github.com/salaamalykum/Islamic-Culture) |
| 📊 Hugging Face Dataset | [https://huggingface.co/datasets/qurancn/Islamic-Culture](https://huggingface.co/datasets/qurancn/Islamic-Culture) |
| 📧 Contact | [bropeace@protonmail.com](mailto:bropeace@protonmail.com) |

---

## Citation

If you use this dataset in your research, please cite:

```bibtex
@dataset{islamic_culture_2026,
  title={Islamic-Culture: A Curated Chinese RAG Dataset of 260 Articles on Islamic Culture},
  author={Salaamalykum Project},
  year={2026},
  publisher={GitHub},
  url={https://github.com/salaamalykum/Islamic-Culture}
}
```

---

## License
This project is licensed under the [MIT License](LICENSE).

## Contributing
See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## Security
See [SECURITY.md](SECURITY.md) for our security policy.
