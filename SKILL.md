---
name: ppt-asset-replacer
display_name: PPT图片字体批量替换
description: 当用户需要批量替换 PPT（.pptx）里的图片、统一或更换字体、替换年份、批量替换文字（如公司名/产品名/联系方式）、或修改主题配色时使用。触发词：替换PPT图片、统一字体、PPT字体替换、批量改PPT、换PPT里的图、PPT年份替换、PPT文字替换、PPT配色、把PPT字体改成思源黑体、批量处理PPT、PPT素材替换、PPT批量改字。
description_en: Use this skill when a user wants to batch-replace images, unify or change fonts, replace years, bulk-replace text (company/product names, contact info), or modify theme colors in a PowerPoint (.pptx) file. Triggers: replace PPT images, change PPT font, unify font, batch edit PPT, swap picture in PPT, PPT year replace, PPT text replace, PPT color theme, convert PPT font to Source Han Sans, batch process PPT, PPT asset replace.
description_zh: PPT（.pptx）图片、字体、年份、文字、配色的批量替换与统一工具。支持单份与批量处理，全程本地运行不联网。触发场景：批量替换 PPT 图片或素材、统一/更改字体（如转思源黑体/宋体/微软雅黑）、替换年份、批量改写文字（公司名/产品名/联系方式）、修改主题配色。
version: 1.0.0
author: 波段诗人
---

# PPT 图片字体批量替换

一个**纯前端、本地运行、不联网**的 PPT（.pptx）批量处理工具。直接改文件内部的图片与 XML，版式、位置、动画、引用关系一概不动，原文件不修改、只生成一份 `_替换.pptx` 新文件。

## 适用场景
- 把一整套模板里的占位图换成新素材（轮换/随机分配）
- 统一字体（如全部转思源黑体 / 思源宋体 / 微软雅黑），或「标题黑体、正文宋体」智能判断
- 把年份批量改成指定年或随机年
- 批量把旧公司名/旧产品名替换成新的（文本查找替换）
- 把主题配色统一换成品牌色（如蓝主色改品牌红）
- 一次批量处理多份 PPT，统一套用同一套规则

## 核心能力
| 能力 | 说明 |
|------|------|
| 图片替换 | 单张选图、多张素材批量（轮换/随机分配）、裁切铺满/完整留白/拉伸变形、JPEG 质量可调；矢量图(.emf/.wmf)自动跳过并提示 |
| 字体替换 | 思源黑体/宋体、微软雅黑、等线、HarmonyOS Sans SC 等可选；自定义字体名；标题黑体/正文宋体智能判断；可选是否连符号字体（Wingdings 等）一起换 |
| 年份替换 | 不替换 / 20—26 随机 / 指定年份 |
| 文本批量替换 | 多行规则 `旧文本 => 新文本`，只替换正文文字，可选区分大小写；新文本留空即删除该文字 |
| 主题配色替换 | 列出 PPT 里出现的颜色，逐色改成新色（十六进制，如 #C0392B） |
| 批量处理 | 多份 PPT 同时套用同一套规则，打包成一个 zip 下载 |
| 暗色模式 | 右上角一键切换，记忆偏好 |

## 使用方法
工具是单文件 HTML：`scripts/ppt-replacer.html`。

1. 把 `scripts/ppt-replacer.html` 下载/保存到本地，用 **Chrome 或 Edge** 打开（需要浏览器支持 CompressionStream / DecompressionStream / createImageBitmap，Safari 需较新版本）。
2. 把 .pptx 拖入页面，按步骤设置图片/字体/年份/文本/配色规则。
3. 点「生成新文件」，浏览器会下载一份 `*_替换.pptx`（批量模式下载 zip）。
4. 全程在本地完成，文件不上传、不联网。

> 若用户希望由 AI 直接处理文件（而非自己开网页）：当前环境无 python-pptx / Pillow，仅标准库可处理「文本/字体/年份/配色」类替换与图片二进制直替；高级图片重绘需用户在网页端完成。可按需扩展 `scripts/` 下的命令行脚本。

## 重要注意事项（务必告知用户）
- **字体只是改「引用名」，不会嵌进文件**。对方电脑没装目标字体会回退显示。交付前建议在 PowerPoint 里勾选「文件 → 选项 → 保存 → 将字体嵌入文件」。
- 新图会按**原图像素尺寸**重新处理再写回，幻灯片里图片框位置/大小完全不变，不会被拉扁。
- 矢量图（.emf/.wmf）浏览器读不了，会被跳过并提示，其余图片照常替换。
- 原文件不动，生成的是新文件，可放心使用。

## 资源
- 主工具：`scripts/ppt-replacer.html`（单文件，双击即用）
- 使用文档：`references/usage.md`
