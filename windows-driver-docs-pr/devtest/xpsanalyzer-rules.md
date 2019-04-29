---
title: XpsAnalyzer 规则
description: XpsAnalyzer 规则
ms.assetid: 4f617665-4cc4-475d-ae66-abc2f00309fd
keywords:
- XpsAnalyzer WDK 规则
ms.date: 09/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: e77be3f40a0009e029c281a22c0be556928b848f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387251"
---
# <a name="xpsanalyzer-rules"></a>XpsAnalyzer 规则

下表介绍 XpsAnalysis 工具用于分析 XPS 文件的规则。 这些规则基于 XML 纸张规范 (XPS) 1.0 规范。 详细了解此规范 doiwnload [XML 纸张规范](http://download.microsoft.com/download/1/6/a/16acc601-1b7a-42ad-8d4e-4f0aa156ec3e/XPS_1_0.exe)。

## <a name="open-packaging-conventions-opc-rules"></a>开放式打包约定 (OPC) 规则

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">规则名称</th>
<th align="left">数据类型</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>CompressionOption</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>XPS 包的压缩选项的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>CorruptedOpc</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 OPC 规范不符合 XPS 包，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ForeignContentType</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>非 XPS 规范的一部分的内容类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ForeignRelationshipType</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>非 XPS 1.0 规范的一部分的关系类型。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>LargePartCount</p></td>
<td align="left"><p>长整型</p></td>
<td align="left"><p>其大小超过指定的量的部分数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MaxFileSizeInBytes</p></td>
<td align="left"><p>长整型</p></td>
<td align="left"><p>XPS 包中部件的集的最大大小。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MaxPartRelationships</p></td>
<td align="left"><p>长整型</p></td>
<td align="left"><p>XPS 包的一部分的关系的最大数目。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PackageRelationshipCount</p></td>
<td align="left"><p>长整型</p></td>
<td align="left"><p>XPS 包中的关系的总数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PartCount</p></td>
<td align="left"><p>长整型</p></td>
<td align="left"><p>OPC 文件中的部件的总数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>TotalPartRelationships</p></td>
<td align="left"><p>长整型</p></td>
<td align="left"><p>部件关系的总数。</p></td>
</tr>
</tbody>
</table>

## <a name="xps-trunk-rules"></a>XPS Trunk 规则

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">规则名称</th>
<th align="left">数据类型</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>CorruptedXpsTrunk</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包不符合 XPS 1.0 规范 （Trunk 级别），则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FixedDocumentCount</p></td>
<td align="left"><p>长整型</p></td>
<td align="left"><p>XPS 包中的文档的总数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasCoreProperties</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含的 XPS 核心属性部分，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasDiscardControl</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含的 DiscardControl 部分，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasDocumentPrintTicket</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含文档级 PrintTicket，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasDocumentStructure</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包包含 DocumentStructure 元素，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasJobPrintTicket</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含 DocumentSequence 级别 PrintTicket，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasMoreThanOneSignatureBlockResourceInADocument</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含具有多个签名块资源的文档，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PackageThumbnailType</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>XPS 包级缩略图图像类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SignatureBlockRequestCount</p></td>
<td align="left"><p>长整型</p></td>
<td align="left"><p>XPS 包中的签名的总数。</p></td>
</tr>
</tbody>
</table>

 

## <a name="xps-page-rules"></a>XPS 页规则

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">规则名称</th>
<th align="left">数据类型</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>BleedBoxDimension</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>XPS 包中的维度的非默认出血框。</p></td>
</tr>
<tr class="even">
<td align="left"><p>BrushCount</p></td>
<td align="left"><p>长整型</p></td>
<td align="left"><p>XPS 包中的画笔元素总数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CanvasCount</p></td>
<td align="left"><p>长整型</p></td>
<td align="left"><p>XPS 包中的画布元素总数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>CanvasLanguage</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>Canvas 元素的语言。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CanvasOpacityMaskBrush</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>画布 OpacityMask 元素画笔类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ContentBoxDimension</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>XPS 包中的非默认 ContentBox 维度。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CorruptedXpsPage</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包不符合 XPS 1.0 规范 （页面级别），则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FixedPageCount</p></td>
<td align="left"><p>长整型</p></td>
<td align="left"><p>XPS 包中的页面元素的总数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FontType</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>XPS 包中找到的字体类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GeometryCount</p></td>
<td align="left"><p>长整型</p></td>
<td align="left"><p>XPS 包中的几何元素的总数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>GeometryFigureClosedFilledPatternRule</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>GeometryFigure 的类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GeometryFigureMaxSegmentCount</p></td>
<td align="left"><p>长整型</p></td>
<td align="left"><p>最大 SegmentCount GeometryFigures 中的元素数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>GeometryFigureMaxSegmentDataCount</p></td>
<td align="left"><p>长整型</p></td>
<td align="left"><p>最大 SegmentDataCount GeometryFigures 中的元素数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GeometryFigureSegmentStrokePattern</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>GeometryFigures 元素笔划模式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>GeometryFigureSegmentType</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>GeometryFigure 元素的段类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GeometryFillRule</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>几何图形的 FillRule。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>GlyphsBidiLevel</p></td>
<td align="left"><p>长整型</p></td>
<td align="left"><p>字形的 BidiLevel。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GlyphsCount</p></td>
<td align="left"><p>长整型</p></td>
<td align="left"><p>XPS 包中的标志符号元素总数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>GlyphsFillBrush</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>标志符号填充画笔类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GlyphsLanguage</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>字形的语言。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>GlyphsOpacityMaskBrush</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>标志符号 OpacityMask 画笔类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GlyphsStyleSimulations</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>字形的 StyleSimulations。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasCanvasClipGeometryLocal</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含与本地 ClipGeometry Canvas 元素，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasCanvasClipGeometryRemote</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含具有远程 ClipGeometry 的 Canvas 元素，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasCanvasHyperlinkTarget</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含具有 HyperlinkTarget 的 Canvas 元素，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasCanvasName</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含具有 Name 属性的 Canvas 元素，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasCanvasOpacityEqualsOne</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>True 如果 XPS 包中包含具有不透明度的画布元素 = 1。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasCanvasOpacityEqualsToZero</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>True 如果 XPS 包中包含具有不透明度的画布元素 = 0。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasCanvasOpacityMaskBrushLocal</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含与本地 OpacityMaskBrush Canvas 元素，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasCanvasOpacityMaskBrushRemote</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含具有远程 OpacityMaskBrush 的 Canvas 元素，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasCanvasTransformLocal</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含使用本地 MatrixTransform Canvas 元素，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasCanvasTransformRemote</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含具有远程 MatrixTransform 的 Canvas 元素，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasCanvasWithAccessibilityLongDescription</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含具有 AccessibilityLongDescription 的 Canvas 元素，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasCanvasWithAccessibilityShortDescription</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含具有 AccessibilityShortDescription 的 Canvas 元素，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasCanvasWithUseAliasedEdgeMode</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>True 如果 XPS 包包含具有 UseAliasedEdgeMode 的画布元素 = True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasColorProfile</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含 ColorProfile，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasGeometryFigureWithMultipleSegmentTypes</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含具有多个段类型的 GeometryFigure 元素，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasGeometryFigureWithNonDefaultStartPoint</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含具有非默认 （0.0，0.0） 的起始点的 GeometryFigure 元素，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasGeometryTransformLocal</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含使用本地 MatrixTransform 几何图形，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasGeometryTransformRemote</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含使用远程 MatrixTransform 几何图形，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasGlyphsClipGeometryLocal</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含本地 ClipGeometry 标志符号，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasGlyphsClipGeometryRemote</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含与远程 ClipGeometry Glyphs 元素，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasGlyphsDeviceFontName</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含与 DeviceFontName Glyphs 元素，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasGlyphsFillBrushLocal</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含与本地 FillBrush Glyphs 元素，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasGlyphsFillBrushRemote</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含与远程 FillBrush Glyphs 元素，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasGlyphsFontFaceIndex</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含与 FontFaceIndex Glyphs 元素，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasGlyphsHyperlinkTarget</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含与 HyperlinkTarget Glyphs 元素，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasGlyphsName</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含具有 Name 属性的标志符号元素，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasGlyphsOpacityEqualsOne</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>True 如果 XPS 包中包含具有不透明度的标志符号元素 = 1。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasGlyphsOpacityEqualsToZero</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>True 如果 XPS 包中包含具有不透明度的标志符号元素 = 0。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasGlyphsOpacityMaskBrushLocal</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含与本地 OpacityMaskBrush Glyphs 元素，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasGlyphsOpacityMaskBrushRemote</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含与远程 OpacityMaskBrush Glyphs 元素，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasGlyphsTransformLocal</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含使用本地 MatrixTransform Glyphs 元素，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasGlyphsTransformRemote</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含使用远程 MatrixTransform Glyphs 元素，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasGlyphsUnicodeString</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含与 UnicodeString Glyphs 元素，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasGlyphsWithSideways</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包包含 Glyphs 元素的 IsSideways 属性启用的则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasHyperlinkTarget</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含的页面包含 aHyperlink 目标，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasImageBrushOpacityEqualsToOne</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>True 如果 XPS 包中包含不透明度为 ImageBrush = 1。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasImageBrushOpacityEqualsToZero</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>True 如果 XPS 包中包含不透明度为 ImageBrush = 0。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasImageBrushTransformLocal</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含使用本地 MatrixTransform ImageBrush，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasImageBrushTransformRemote</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含使用远程 MatrixTransform ImageBrush，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasImageBrushWithColorProfileResource</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含与 ColorProfileResource ImageBrush，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasImageBrushWithNonDefaultViewBox</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含非默认 viewbox （0，0，1，1） 使用 ImageBrush，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasImageBrushWithNonDefaultViewPort</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含一个非默认的视区 （0，0，1，1） 使用 ImageBrush，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasLinearGradientBrushOpacityEqualsToOne</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>True 如果 XPS 包中包含不透明度为 LinearGradientBrush = 1。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasLinearGradientBrushOpacityEqualsToZero</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>True 如果 XPS 包中包含不透明度为 LinearGradientBrush = 0。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasLinearGradientBrushTransformLocal</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含使用本地 MatrixTransform LinearGradientBrush，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasLinearGradientBrushTransformRemote</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含使用远程 MatrixTransform LinearGradientBrush，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasLinearGradientBrushWithColorProfileResource</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含与 ColorProfileResource LinearGradientBrush，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasLinearGradientBrushWithNonDefaultEndPoint</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>如果 XPS 包中包含 LinearGradientBrush 与非默认终结点，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasLinearGradientBrushWithNonDefaultGradientStopOffset</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含具有非默认 GradientStopOffset LinearGradientBrush，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasLinearGradientBrushWithNonDefaultStartPoint</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>如果 XPS 包中包含具有非默认 StartPoint LinearGradientBrush，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasLocalDictionary</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含使用本地字典的页面，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasNonDefaultBleedBox</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含的页面包含一个非默认出血框值，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasNonDefaultContentBox</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含的页面包含一个非默认 ContentBox 值，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPageName</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含的页设置名称特性，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPagePrintTicket</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含页级 PrintTicket，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathClipGeometryLocal</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含具有本地 ClipGeometry 的路径，则返回 true</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathClipGeometryRemote</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含远程 ClipGeometry 值的路径，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathFillBrushLocal</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含具有本地 FillBrush 的路径，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathFillBrushRemote</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含具有远程 FillBrush 的路径，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathGeometryLocal</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含具有本地 Geometry 属性的路径，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathGeometryRemote</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含一个远程的 Geometry 属性的路径，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathHyperlinkTarget</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含具有 HyperlinkTarget 值的路径，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathName</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含具有 Name 属性的路径，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathOpacityEqualsOne</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>True 如果 XPS 包中包含不透明度为路径 = 1。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathOpacityEqualsToZero</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>True 如果 XPS 包中包含不透明度为路径 = 0。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathOpacityMaskBrushLocal</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含具有本地 OpacityMaskBrush 值的路径，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathOpacityMaskBrushRemote</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含具有远程 OpacityMaskBrush 的路径，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathStrokeBrushLocal</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含具有本地 StrokeBrush 属性的路径，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathStrokeBrushRemote</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含具有远程 StrokeBrush 属性的路径，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathStrokeDashOffset</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含具有 StrokeDashOffset 的路径，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathTransformLocal</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含使用本地 MatrixTransform 的路径，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathTransformRemote</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含具有远程 MatrixTransform 的路径，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathWithAccessibilityLongDescription</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含具有 AccessibilityLongDescription 值的路径，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathWithAccessibilityShortDescription</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含具有 AccessibilityShortDescription 的路径，则返回 true</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathWithNonDefaultStrokeMiterLimit</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含具有非默认 StrokeMiterLimit 的路径，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathWithNonDefaultStrokeThickness</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含具有非默认 StrokeThickness 的路径，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathWithSnapsToPixel</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含具有 SnapToPixels 值的路径，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasRadialGradientBrushOpacityEqualsToOne</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>True 如果 XPS 包中包含不透明度为 RadialGradientBrush = 1。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasRadialGradientBrushOpacityEqualsToZero</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>True 如果 XPS 包中包含不透明度为 RadialGradientBrush = 0。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasRadialGradientBrushTransformLocal</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含使用本地 MatrixTransform RadialGradientBrush，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasRadialGradientBrushTransformRemote</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含使用远程 MatrixTransform RadialGradientBrush，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasRadialGradientBrushWithColorProfileResource</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含与 ColorProfileResource RadialGradientBrush，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasRadialGradientBrushWithNonDefaultCenter</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含与非默认中心 RadialGradientBrush，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasRadialGradientBrushWithNonDefaultGradientOrigin</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含具有非默认 GradientOrigin RadialGradientBrush，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasRadialGradientBrushWithNonDefaultGradientStopOffset</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含具有非默认 GradientStopOffset RadialGradientBrush，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasRadialGradientBrushWithNonDefaultRadiiSizes</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含具有非默认 RadiiSizes RadialGradientBrush，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasRemoteDictionary</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含一个使用 RemoteDictionary 页，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasSolidColorBrushOpacityEqualsToOne</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>True 如果 XPS 包中包含不透明度为 SolidColorBrush = 1。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasSolidColorBrushOpacityEqualsToZero</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>True 如果 XPS 包中包含不透明度为 SolidColorBrush = 0。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasSolidColorBrushWithColorProfileResource</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含与 ColorProfileResource SolidColorBrush，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasStoryFragment</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包包含 StoryFragment 部分，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasVisualBrushOpacityEqualsToOne</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>True 如果 XPS 包中包含具有不透明度的 VisualBrush 元素 = 1。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasVisualBrushOpacityEqualsToZero</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>True 如果 XPS 包中包含具有不透明度的 VisualBrush 元素 = 0。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasVisualBrushTransformLocal</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含具有本地 MatrixTransform 的 VisualBrush 元素，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasVisualBrushTransformRemote</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含具有远程 MatrixTransform 的 VisualBrush 元素，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasVisualBrushWithLocalCanvas</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含具有本地画布的 VisualBrush 元素，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasVisualBrushWithLocalGlyphs</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含本地的标志符号的 VisualBrush 元素，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasVisualBrushWithLocalPath</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含的本地路径的 VisualBrush 元素，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasVisualBrushWithNonDefaultViewBox</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含具有非默认 ViewBox （0，0，1，1） 的 VisualBrush 元素，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasVisualBrushWithNonDefaultViewPort</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含的 VisualBrush 元素具有一个非默认的视区 （0，0，1，1），则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasVisualBrushWithRemoteCanvas</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含具有远程画布的 VisualBrush 元素，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasVisualBrushWithRemoteGlyphs</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含远程的标志符号的 VisualBrush 元素，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasVisualBrushWithRemotePath</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含远程路径的 VisualBrush 元素，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ImageBrushCount</p></td>
<td align="left"><p>长整型</p></td>
<td align="left"><p>ImageBrush XPS 包中的元素的总数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ImageBrushTileMode</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>ImageBrush 元素的 TileMode 值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ImageBrushType</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>ImageBrush 元素的图像类型值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>LinearGradientBrushColorInterpolationMode</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>ColorInterpolationMode LinearGradientBrush 元素的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>LinearGradientBrushColorType</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>LinearGradientBrush 元素的颜色类型值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>LinearGradientBrushContextColorChannelCount</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>LinearGradientBrush 元素的上下文颜色通道计数值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>LinearGradientBrushCount</p></td>
<td align="left"><p>长整型</p></td>
<td align="left"><p>LinearGradientBrush XPS 包中的元素的总数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>LinearGradientBrushSpreadMethod</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>SpreadMethod LinearGradientBrush 元素的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>LinkTargetsCount</p></td>
<td align="left"><p>长整型</p></td>
<td align="left"><p>LinkTargets XPS 包中的元素的总数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>LocalDictionaryContent</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>此本地字典中找到可共享对象的类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MaxGlyphsFontRenderingEMSize</p></td>
<td align="left"><p>长整型</p></td>
<td align="left"><p>Glyphs 元素中最大 FontRenderingEmSize。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MaxGlyphsIndicesInAGlyphs</p></td>
<td align="left"><p>长整型</p></td>
<td align="left"><p>Glyphs 元素中的索引的最大大小。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MaxGlyphsMappingsInAGlyphs</p></td>
<td align="left"><p>长整型</p></td>
<td align="left"><p>Glyphs 元素最大大小的映射。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MaxGlyphsProhibitedCaretStopCountInAGlyphs</p></td>
<td align="left"><p>长整型</p></td>
<td align="left"><p>Glyphs 元素中 ProhibitedCaretStopCount 最大大小。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MaxGradientStopsInALinearGradientBrush</p></td>
<td align="left"><p>长整型</p></td>
<td align="left"><p>LinearGradientBrush 元素中 GradientStops 最大数目。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MaxGradientStopsInARadialGradientBrush</p></td>
<td align="left"><p>长整型</p></td>
<td align="left"><p>RadialGradientBrush 元素中 GradientStops 最大数目。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MaxStrokeDashesInAPath</p></td>
<td align="left"><p>长整型</p></td>
<td align="left"><p>中的路径元素 StrokeDashes 最大数目。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PageDimension</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>宽度和高度的 XPS 包中的页。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PageLanguage</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>页面的语言。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PageThumbnailType</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>页级缩略图图像类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PathCount</p></td>
<td align="left"><p>长整型</p></td>
<td align="left"><p>XPS 包中的路径元素的总数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PathFillBrush</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>路径填充画笔类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PathLanguage</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>路径元素的语言值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PathOpacityMaskBrush</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>路径 OpacityMask 画笔类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PathStrokeBrush</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>路径笔划属性的画笔类型。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PathStrokeDashCap</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>StrokeDashCap 路径元素的类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PathStrokeEndLineCap</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>Path 元素 StrokeEndLineCap 值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PathStrokeLineJoin</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>Path 元素 StrokeLineJoin 值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PathStrokeStartLineCap</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>Path 元素 StrokeStartLineCap 值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RadialGradientBrushColorInterpolationMode</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>RadialGradientBrush 元素 ColorInterpolationMode 值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>RadialGradientBrushColorType</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>RadialGradientBrush 元素的颜色类型值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RadialGradientBrushContextColorChannelCount</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>RadialGradientBrush 元素的上下文颜色通道计数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>RadialGradientBrushCount</p></td>
<td align="left"><p>长整型</p></td>
<td align="left"><p>RadialGradientBrush XPS 包中的元素的总数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RadialGradientBrushEllipseOrCircle</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>定义渐变画笔椭圆或圆。</p></td>
</tr>
<tr class="even">
<td align="left"><p>RadialGradientBrushSpreadMethod</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>RadialGradientBrush 元素 SpreadMethod 值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RemoteDictionaryContent</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>此远程字典中找到可共享对象的类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SolidColorBrushColorType</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>颜色的 SolidColorBrush 元素类型。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SolidColorBrushContextColorChannelCount</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>SolidColorBrush 元素的上下文颜色通道计数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SolidColorBrushCount</p></td>
<td align="left"><p>长整型</p></td>
<td align="left"><p>SolidColorBrush XPS 包中的元素的总数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>VisualBrushCount</p></td>
<td align="left"><p>长整型</p></td>
<td align="left"><p>VisualBrush XPS 包中的元素的总数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>VisualBrushTileMode</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>VisualBrush 元素的 TileMode 值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>VisualCount</p></td>
<td align="left"><p>长整型</p></td>
<td align="left"><p>XPS 包中的视觉对象总数。</p></td>
</tr>
</tbody>
</table>

## <a name="digital-signature-rules"></a>数字签名的规则

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">规则名称</th>
<th align="left">数据类型</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>CorruptedDigitalSignature</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含损坏的数字签名，则为 true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SignatureCount</p></td>
<td align="left"><p>长整型</p></td>
<td align="left"><p>XPS 包中的数字签名的总数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>XpsSignaturePolicy</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>签名元素的 XPS 签名策略值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasInvalidXpsSignature</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含无效的 XPS 签名元素，则为 true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>XpsSignatureStatus</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>在该签名是无效的情况下签名元素的签名状态值。 换而言之，当 HasInvalidXpsSignature 为 True 时才启用此规则。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MaxNumberOfCertificatesInASignature</p></td>
<td align="left"><p>长整型</p></td>
<td align="left"><p>证书签名元素中找到的最大数目。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasXpsSignatureWithEmptyID</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>XPS 包包含的 XPS 签名元素具有空的 id。 如果为 true</p></td>
</tr>
<tr class="even">
<td align="left"><p>SignatureTimeFormat</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>签名元素的签名时间格式值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MaxNumberOfCustomObjectsInASignature</p></td>
<td align="left"><p>长整型</p></td>
<td align="left"><p>签名元素中找到的自定义对象的最大数目。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MaxNumberOfCustomReferencesInASignature</p></td>
<td align="left"><p>长整型</p></td>
<td align="left"><p>在签名元素中找到自定义引用的最大数目。</p></td>
</tr>
</tbody>
</table>

## <a name="miscellaneous-rules"></a>其他规则

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">规则名称</th>
<th align="left">数据类型</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>CorruptedPageRendering</p></td>
<td align="left"><p>布尔</p></td>
<td align="left"><p>如果 XPS 包中包含的非可呈现的页面，则为 true。</p></td>
</tr>
</tbody>
</table>
