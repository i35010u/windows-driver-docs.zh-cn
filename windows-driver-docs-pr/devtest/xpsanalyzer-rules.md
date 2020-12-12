---
title: XpsAnalyzer 规则
description: XpsAnalyzer 规则
keywords:
- XpsAnalyzer WDK，规则
ms.date: 09/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: e23d5206a2159c7d1ee918e8d610fbc0c5945a5b
ms.sourcegitcommit: a6b027c53492a3cdd62abfa92bc07711e46a6acb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/12/2020
ms.locfileid: "97366131"
---
# <a name="xpsanalyzer-rules"></a>XpsAnalyzer 规则

下表描述了 XpsAnalysis 工具用于分析 XPS 文件的规则。 这些规则基于 XML 纸张规范 (XPS) 1.0 规范。 有关此规范的详细信息，请下载 [XML 纸张规范](https://download.microsoft.com/download/1/6/a/16acc601-1b7a-42ad-8d4e-4f0aa156ec3e/xps_1_0.zip)。

## <a name="open-packaging-conventions-opc-rules"></a> (OPC) 规则打开打包约定

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
<td align="left"><p>字符串</p></td>
<td align="left"><p>XPS 包的 Compression 选项的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>CorruptedOpc</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包不符合 OPC 规范，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ForeignContentType</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>不属于 XPS 规范的内容类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ForeignRelationshipType</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>不属于 XPS 1.0 规范的关系类型。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>LargePartCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>大小超过指定量的部分数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MaxFileSizeInBytes</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS 包中的部件集的最大大小。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MaxPartRelationships</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS 包某个部分的最大关系数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PackageRelationshipCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS 包中的关系总数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PartCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>OPC 文件中的部件总数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>TotalPartRelationships</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>部分关系的总数。</p></td>
</tr>
</tbody>
</table>

## <a name="xps-trunk-rules"></a>XPS 干线规则

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
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包不符合 XPS 1.0 规范 (中继级别) ，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FixedDocumentCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS 包中的文档总数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasCoreProperties</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含 XPS Core Properties 部分，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasDiscardControl</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含 DiscardControl 部分，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasDocumentPrintTicket</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含文档级 PrintTicket，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasDocumentStructure</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含 DocumentStructure 元素，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasJobPrintTicket</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含 DocumentSequence 级别的 PrintTicket，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasMoreThanOneSignatureBlockResourceInADocument</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含具有多个签名块资源的文档，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PackageThumbnailType</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>XPS 包级缩略图的图像类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SignatureBlockRequestCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS 包中的签名总数。</p></td>
</tr>
</tbody>
</table>

 

## <a name="xps-page-rules"></a>XPS 页面规则

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
<td align="left"><p>字符串</p></td>
<td align="left"><p>XPS 包中的非默认 BleedBox 的维度。</p></td>
</tr>
<tr class="even">
<td align="left"><p>BrushCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS 包中的画笔元素总数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CanvasCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS 包中的画布元素总数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>CanvasLanguage</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>Canvas 元素的语言。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CanvasOpacityMaskBrush</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>画布 OpacityMask 元素的画笔类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ContentBoxDimension</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>XPS 包中的非默认 ContentBox 的维度。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CorruptedXpsPage</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包不符合 XPS 1.0 规范 (页面级别) ，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FixedPageCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS 包中的页元素总数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FontType</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>XPS 包中的字体类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GeometryCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS 包中的 Geometry 元素总数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>GeometryFigureClosedFilledPatternRule</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>GeometryFigure 的类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GeometryFigureMaxSegmentCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>GeometryFigures 中的 SegmentCount 元素的最大数目。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>GeometryFigureMaxSegmentDataCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>GeometryFigures 中的 SegmentDataCount 元素的最大数目。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GeometryFigureSegmentStrokePattern</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>GeometryFigures 元素的笔划模式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>GeometryFigureSegmentType</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>GeometryFigure 元素的段类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GeometryFillRule</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>几何图形的 FillRule。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>GlyphsBidiLevel</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>标志符号的 BidiLevel。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GlyphsCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS 包中的标志符号元素总数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>GlyphsFillBrush</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>字形填充的画笔类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GlyphsLanguage</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>字形的语言。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>GlyphsOpacityMaskBrush</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>字形 OpacityMask 的画笔类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GlyphsStyleSimulations</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>标志符号的 StyleSimulations。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasCanvasClipGeometryLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含带有本地 ClipGeometry 的 Canvas 元素，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasCanvasClipGeometryRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含带有 remote ClipGeometry 的 Canvas 元素，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasCanvasHyperlinkTarget</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含带有 Reportviewer.hyperlinktarget 的 Canvas 元素，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasCanvasName</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含具有 Name 属性的 Canvas 元素，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasCanvasOpacityEqualsOne</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含不透明度为1的 Canvas 元素，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasCanvasOpacityEqualsToZero</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含不透明度为0的 Canvas 元素，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasCanvasOpacityMaskBrushLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含带有本地 OpacityMaskBrush 的 Canvas 元素，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasCanvasOpacityMaskBrushRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含带有 remote OpacityMaskBrush 的 Canvas 元素，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasCanvasTransformLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含带有本地 MatrixTransform 的 Canvas 元素，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasCanvasTransformRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含带有 remote MatrixTransform 的 Canvas 元素，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasCanvasWithAccessibilityLongDescription</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含带有 AccessibilityLongDescription 的 Canvas 元素，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasCanvasWithAccessibilityShortDescription</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含带有 AccessibilityShortDescription 的 Canvas 元素，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasCanvasWithUseAliasedEdgeMode</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含带有 UseAliasedEdgeMode = True 的 Canvas 元素，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasColorProfile</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含 ColorProfile，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasGeometryFigureWithMultipleSegmentTypes</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含具有多个段类型的 GeometryFigure 元素，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasGeometryFigureWithNonDefaultStartPoint</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含具有非默认 StartPoint (0.0，0.0) 的 GeometryFigure 元素，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasGeometryTransformLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含包含本地 MatrixTransform 的几何图形，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasGeometryTransformRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含具有远程 MatrixTransform 的几何图形，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasGlyphsClipGeometryLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含带有本地 ClipGeometry 的标志符号，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasGlyphsClipGeometryRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含带有远程 ClipGeometry 的字形元素，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasGlyphsDeviceFontName</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含带有 DeviceFontName 的字形元素，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasGlyphsFillBrushLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含带有本地 FillBrush 的字形元素，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasGlyphsFillBrushRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含带有远程 FillBrush 的字形元素，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasGlyphsFontFaceIndex</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含带有 FontFaceIndex 的字形元素，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasGlyphsHyperlinkTarget</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含带有 Reportviewer.hyperlinktarget 的字形元素，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasGlyphsName</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含具有 Name 属性的字形元素，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasGlyphsOpacityEqualsOne</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含不透明度为1的标志符号元素，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasGlyphsOpacityEqualsToZero</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含不透明度为0的标志符号元素，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasGlyphsOpacityMaskBrushLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含带有本地 OpacityMaskBrush 的字形元素，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasGlyphsOpacityMaskBrushRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含带有远程 OpacityMaskBrush 的字形元素，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasGlyphsTransformLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含带有本地 MatrixTransform 的字形元素，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasGlyphsTransformRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含带有远程 MatrixTransform 的字形元素，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasGlyphsUnicodeString</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含带有 UnicodeString 的字形元素，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasGlyphsWithSideways</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含启用了 IsSideways 属性的字形元素，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasHyperlinkTarget</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含包含 aHyperlink 目标的页，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasImageBrushOpacityEqualsToOne</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含不透明度为1的 System.windows.media.imagebrush>，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasImageBrushOpacityEqualsToZero</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含不透明度为0的 System.windows.media.imagebrush>，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasImageBrushTransformLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含包含本地 MatrixTransform 的 System.windows.media.imagebrush>，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasImageBrushTransformRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含具有远程 MatrixTransform 的 System.windows.media.imagebrush>，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasImageBrushWithColorProfileResource</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含带有 ColorProfileResource 的 System.windows.media.imagebrush>，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasImageBrushWithNonDefaultViewBox</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含带有非默认 ViewBox (0，0，1，1) 的 System.windows.media.imagebrush>，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasImageBrushWithNonDefaultViewPort</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含非默认视区的 System.windows.media.imagebrush>， (0，0，1，1) ，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasLinearGradientBrushOpacityEqualsToOne</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含不透明度为1的 LinearGradientBrush，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasLinearGradientBrushOpacityEqualsToZero</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含不透明度为0的 LinearGradientBrush，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasLinearGradientBrushTransformLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含包含本地 MatrixTransform 的 LinearGradientBrush，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasLinearGradientBrushTransformRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含具有远程 MatrixTransform 的 LinearGradientBrush，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasLinearGradientBrushWithColorProfileResource</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含带有 ColorProfileResource 的 LinearGradientBrush，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasLinearGradientBrushWithNonDefaultEndPoint</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>如果 XPS 包包含带有非默认终结点的 LinearGradientBrush，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasLinearGradientBrushWithNonDefaultGradientStopOffset</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含带有非默认 GradientStopOffset 的 LinearGradientBrush，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasLinearGradientBrushWithNonDefaultStartPoint</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>如果 XPS 包包含带有非默认 StartPoint 的 LinearGradientBrush，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasLocalDictionary</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含使用本地字典的页，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasNonDefaultBleedBox</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含具有非默认 BleedBox 值的页，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasNonDefaultContentBox</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含具有非默认 ContentBox 值的页，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPageName</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含设置了 Name 属性的页，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPagePrintTicket</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含页级别 PrintTicket，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathClipGeometryLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含包含本地 ClipGeometry 的路径，则为 True</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathClipGeometryRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含具有远程 ClipGeometry 值的路径，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathFillBrushLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含包含本地 FillBrush 的路径，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathFillBrushRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含带有远程 FillBrush 的路径，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathGeometryLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含带有 Geometry 属性的路径，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathGeometryRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含具有远程 Geometry 属性的路径，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathHyperlinkTarget</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含具有 Reportviewer.hyperlinktarget 值的路径，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathName</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含名称属性的路径，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathOpacityEqualsOne</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含不透明度为1的路径，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathOpacityEqualsToZero</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含不透明度为0的路径，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathOpacityMaskBrushLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含具有本地 OpacityMaskBrush 值的路径，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathOpacityMaskBrushRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含具有远程 OpacityMaskBrush 的路径，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathStrokeBrushLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含具有本地 StrokeBrush 属性的路径，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathStrokeBrushRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含具有远程 StrokeBrush 属性的路径，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathStrokeDashOffset</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含具有 StrokeDashOffset 的路径，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathTransformLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含包含本地 MatrixTransform 的路径，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathTransformRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含带有远程 MatrixTransform 的路径，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathWithAccessibilityLongDescription</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含具有 AccessibilityLongDescription 值的路径，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathWithAccessibilityShortDescription</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含具有 AccessibilityShortDescription 的路径，则为 True</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathWithNonDefaultStrokeMiterLimit</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含带有非默认 StrokeMiterLimit 的路径，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathWithNonDefaultStrokeThickness</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含带有非默认 StrokeThickness 的路径，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathWithSnapsToPixel</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含具有 SnapToPixels 值的路径，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasRadialGradientBrushOpacityEqualsToOne</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含不透明度为1的 RadialGradientBrush，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasRadialGradientBrushOpacityEqualsToZero</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含不透明度为0的 RadialGradientBrush，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasRadialGradientBrushTransformLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含包含本地 MatrixTransform 的 RadialGradientBrush，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasRadialGradientBrushTransformRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含具有远程 MatrixTransform 的 RadialGradientBrush，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasRadialGradientBrushWithColorProfileResource</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含带有 ColorProfileResource 的 RadialGradientBrush，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasRadialGradientBrushWithNonDefaultCenter</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含非默认中心的 RadialGradientBrush，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasRadialGradientBrushWithNonDefaultGradientOrigin</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含带有非默认 System.windows.media.radialgradientbrush.gradientorigin 的 RadialGradientBrush，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasRadialGradientBrushWithNonDefaultGradientStopOffset</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含带有非默认 GradientStopOffset 的 RadialGradientBrush，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasRadialGradientBrushWithNonDefaultRadiiSizes</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含带有非默认 RadiiSizes 的 RadialGradientBrush，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasRemoteDictionary</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含使用 RemoteDictionary 的页，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasSolidColorBrushOpacityEqualsToOne</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含不透明度为1的 System.windows.media.solidcolorbrush>，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasSolidColorBrushOpacityEqualsToZero</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含不透明度为0的 System.windows.media.solidcolorbrush>，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasSolidColorBrushWithColorProfileResource</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含带有 ColorProfileResource 的 System.windows.media.solidcolorbrush>，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasStoryFragment</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含 StoryFragment 部分，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasVisualBrushOpacityEqualsToOne</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含不透明度为1的 System.windows.media.visualbrush> 元素，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasVisualBrushOpacityEqualsToZero</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含不透明度为0的 System.windows.media.visualbrush> 元素，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasVisualBrushTransformLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含包含本地 MatrixTransform 的 System.windows.media.visualbrush> 元素，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasVisualBrushTransformRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含带有 Remote MatrixTransform 的 System.windows.media.visualbrush> 元素，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasVisualBrushWithLocalCanvas</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含带有本地画布的 System.windows.media.visualbrush> 元素，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasVisualBrushWithLocalGlyphs</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含带有本地标志符号的 System.windows.media.visualbrush> 元素，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasVisualBrushWithLocalPath</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含包含本地路径的 System.windows.media.visualbrush> 元素，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasVisualBrushWithNonDefaultViewBox</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含一个具有非默认 ViewBox (0，0，1，1) 的 System.windows.media.visualbrush> 元素，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasVisualBrushWithNonDefaultViewPort</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含一个具有非默认视区 (0，0，1，1) 的 System.windows.media.visualbrush> 元素，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasVisualBrushWithRemoteCanvas</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含带有远程画布的 System.windows.media.visualbrush> 元素，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasVisualBrushWithRemoteGlyphs</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含具有远程标志符号的 System.windows.media.visualbrush> 元素，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasVisualBrushWithRemotePath</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含具有远程路径的 System.windows.media.visualbrush> 元素，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ImageBrushCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS 包中的 System.windows.media.imagebrush> 元素总数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ImageBrushTileMode</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>System.windows.media.imagebrush> 元素的 System.windows.media.tilemode> 值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ImageBrushType</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>System.windows.media.imagebrush> 元素的图像类型值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>LinearGradientBrushColorInterpolationMode</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>LinearGradientBrush 元素的 ColorInterpolationMode 值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>LinearGradientBrushColorType</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>LinearGradientBrush 元素的颜色类型值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>LinearGradientBrushContextColorChannelCount</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>LinearGradientBrush 元素的上下文颜色通道计数值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>LinearGradientBrushCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS 包中的 LinearGradientBrush 元素总数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>LinearGradientBrushSpreadMethod</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>LinearGradientBrush 元素的 SpreadMethod 值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>LinkTargetsCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS 包中的 LinkTargets 元素总数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>LocalDictionaryContent</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>在此本地字典中找到的可共享对象的类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MaxGlyphsFontRenderingEMSize</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>标志符号元素中的最大 FontRenderingEmSize。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MaxGlyphsIndicesInAGlyphs</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>标志符号元素中索引的最大大小。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MaxGlyphsMappingsInAGlyphs</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>标志符号元素中映射的最大大小。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MaxGlyphsProhibitedCaretStopCountInAGlyphs</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>标志符号元素中 ProhibitedCaretStopCount 的最大大小。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MaxGradientStopsInALinearGradientBrush</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>LinearGradientBrush 元素中的最大 GradientStops 数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MaxGradientStopsInARadialGradientBrush</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>RadialGradientBrush 元素中的最大 GradientStops 数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MaxStrokeDashesInAPath</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>路径元素中的最大 StrokeDashes 数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PageDimension</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>XPS 包中页面的宽度和高度。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PageLanguage</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>页面的语言。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PageThumbnailType</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>页面级缩略图的图像类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PathCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS 包中的路径元素总数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PathFillBrush</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>路径填充的画笔类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PathLanguage</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>Path 元素的语言值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PathOpacityMaskBrush</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>路径 OpacityMask 的画笔类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PathStrokeBrush</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>路径笔划属性的画笔类型。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PathStrokeDashCap</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>路径元素的 StrokeDashCap 类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PathStrokeEndLineCap</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>Path 元素的 StrokeEndLineCap 值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PathStrokeLineJoin</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>Path 元素的 StrokeLineJoin 值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PathStrokeStartLineCap</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>Path 元素的 StrokeStartLineCap 值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RadialGradientBrushColorInterpolationMode</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>RadialGradientBrush 元素的 ColorInterpolationMode 值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>RadialGradientBrushColorType</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>RadialGradientBrush 元素的颜色类型值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RadialGradientBrushContextColorChannelCount</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>RadialGradientBrush 元素的上下文颜色通道计数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>RadialGradientBrushCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS 包中的 RadialGradientBrush 元素总数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RadialGradientBrushEllipseOrCircle</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>定义渐变画笔是椭圆还是圆。</p></td>
</tr>
<tr class="even">
<td align="left"><p>RadialGradientBrushSpreadMethod</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>RadialGradientBrush 元素的 SpreadMethod 值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RemoteDictionaryContent</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>在此远程字典中找到的可共享对象的类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SolidColorBrushColorType</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>System.windows.media.solidcolorbrush> 元素的颜色类型。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SolidColorBrushContextColorChannelCount</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>System.windows.media.solidcolorbrush> 元素的上下文颜色通道计数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SolidColorBrushCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS 包中的 System.windows.media.solidcolorbrush> 元素总数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>VisualBrushCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS 包中的 System.windows.media.visualbrush> 元素总数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>VisualBrushTileMode</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>System.windows.media.visualbrush> 元素的 System.windows.media.tilemode> 值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>VisualCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS 包中的视觉对象总数。</p></td>
</tr>
</tbody>
</table>

## <a name="digital-signature-rules"></a>数字签名规则

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
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含损坏的数字签名，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SignatureCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS 包中的数字签名总数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>XpsSignaturePolicy</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>签名元素的 XPS 签名策略值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasInvalidXpsSignature</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含无效的 XPS 签名元素，则为 True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>XpsSignatureStatus</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>签名无效的情况下的签名元素的签名状态值。 换言之，仅当 HasInvalidXpsSignature 为 True 时才启用此规则。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MaxNumberOfCertificatesInASignature</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>在签名元素中找到的证书的最大数目。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasXpsSignatureWithEmptyID</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含包含空 ID 的 XPS 签名元素，则为 True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SignatureTimeFormat</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>签名元素的签名时间格式值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MaxNumberOfCustomObjectsInASignature</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>在签名元素中找到的自定义对象的最大数目。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MaxNumberOfCustomReferencesInASignature</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>在签名元素中找到的最大自定义引用数。</p></td>
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
<td align="left"><p>bool</p></td>
<td align="left"><p>如果 XPS 包包含非呈现页，则为 True。</p></td>
</tr>
</tbody>
</table>
