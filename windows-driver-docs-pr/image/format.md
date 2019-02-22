---
title: Format 元素
description: 可选的格式元素指示支持扫描程序的单个文件格式和压缩类型。
ms.assetid: aa15607b-780b-48cb-b63f-b16476f69f70
keywords:
- Format 元素成像设备
topic_type:
- apiref
api_name:
- wscn Format wscn Override "" wscn UsedDefault ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c17cf3b9a3179d6509a1f6e7f54e5d14ce699e7f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542978"
---
# <a name="format-element"></a>Format 元素


可选**格式**元素指示支持扫描程序的单个文件格式和压缩类型。

<a name="usage"></a>用法
-----

```xml
<wscn:Format wscn:Override="" wscn:UsedDefault=""
  
      Override
      = "xs:string"
  
      UsedDefault
      = "xs:string">
  text
</wscn:Format wscn:Override="" wscn:UsedDefault="">
```

<a name="attributes"></a>属性
----------

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>在任务栏的搜索框中键入</th>
<th>必需</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Override</strong></p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p></p>
<p>可选。 一个布尔值，必须为 0， <strong>false</strong>，1，或<strong>true</strong>。</p></td>
</tr>
<tr class="even">
<td><p><strong>UsedDefault</strong></p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p></p>
<p>可选。 一个布尔值，必须为 0， <strong>false</strong>，1，或<strong>true</strong>。</p></td>
</tr>
</tbody>
</table>

<a name="text-value"></a>文本值
----------

必需。 以下值之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>术语</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><span id="dib"></span><span id="DIB"></span>dib</p></td>
<td><p>Windows 设备无关的位图。</p></td>
</tr>
<tr class="even">
<td><p><span id="exif"></span><span id="EXIF"></span>exif</p></td>
<td><p>可交换图像文件格式版本 2.x。</p></td>
</tr>
<tr class="odd">
<td><p><span id="jbig"></span><span id="JBIG"></span>jbig</p></td>
<td><p>ISO/IEC 11544:1993 标准-图片和音频信息; 编码表示形式渐进式二值图像压缩。</p></td>
</tr>
<tr class="even">
<td><p><span id="jfif"></span><span id="JFIF"></span>jfif</p></td>
<td><p>JPEG 文件交换格式 1.x。</p></td>
</tr>
<tr class="odd">
<td><p><span id="jpeg2k"></span><span id="JPEG2K"></span>jpeg2k</p></td>
<td><p>JPEG 2000 基于标准的文件格式和压缩。</p></td>
</tr>
<tr class="even">
<td><p><span id="pdf-a"></span><span id="PDF-A"></span>pdf-a</p></td>
<td><p>PDF/A 格式 (标准基于 ISO/CD 19005-1)。</p></td>
</tr>
<tr class="odd">
<td><p><span id="png"></span><span id="PNG"></span>png</p></td>
<td><p>可移植网络图形 (PNG) 格式。 此格式支持仅 PNG 压缩类型。</p></td>
</tr>
<tr class="even">
<td><p><span id="tiff-single-uncompressed"></span><span id="TIFF-SINGLE-UNCOMPRESSED"></span>tiff-single-uncompressed</p></td>
<td><p>单个页面的 TIFF 文件没有压缩类型。</p></td>
</tr>
<tr class="odd">
<td><p><span id="tiff-single-g4"></span><span id="TIFF-SINGLE-G4"></span>tiff-single-g4</p></td>
<td><p>G4 压缩类型的单个页 TIFF 文件。</p></td>
</tr>
<tr class="even">
<td><p><span id="tiff-single-g3mh"></span><span id="TIFF-SINGLE-G3MH"></span>tiff-single-g3mh</p></td>
<td><p>单个页面 TIFF 文件 g3mh 压缩类型。</p></td>
</tr>
<tr class="odd">
<td><p><span id="tiff-single-jpeg-tn2"></span><span id="TIFF-SINGLE-JPEG-TN2"></span>tiff-single-jpeg-tn2</p></td>
<td><p>单个页面 TIFF 文件，其技术说明 2 中所述的 JPEG 压缩类型。</p></td>
</tr>
<tr class="even">
<td><p><span id="tiff-multi-uncompressed"></span><span id="TIFF-MULTI-UNCOMPRESSED"></span>tiff-multi-uncompressed</p></td>
<td><p>多个页面的 TIFF 文件没有压缩类型。</p></td>
</tr>
<tr class="odd">
<td><p><span id="tiff-multi-g4"></span><span id="TIFF-MULTI-G4"></span>tiff-multi-g4</p></td>
<td><p>G4 压缩类型的多个页 TIFF 文件。</p></td>
</tr>
<tr class="even">
<td><p><span id="tiff-multi-g3mh"></span><span id="TIFF-MULTI-G3MH"></span>tiff-multi-g3mh</p></td>
<td><p>多个页面的 TIFF 文件与 g3mh 压缩类型。</p></td>
</tr>
<tr class="odd">
<td><p><span id="tiff-multi-jpeg-tn2"></span><span id="TIFF-MULTI-JPEG-TN2"></span>tiff-multi-jpeg-tn2</p></td>
<td><p>技术说明 2 中所述的 JPEG 压缩类型使用多个页面的 TIFF 文件。</p></td>
</tr>
<tr class="even">
<td><p><span id="xps"></span><span id="XPS"></span>xps</p></td>
<td><p>XML 纸张规范</p></td>
</tr>
<tr class="odd">
<td><p><span id="Any_vendor-defined_values"></span><span id="any_vendor-defined_values"></span><span id="ANY_VENDOR-DEFINED_VALUES"></span>供应商定义的任何值</p></td>
<td></td>
</tr>
</tbody>
</table>

 

## <a name="child-elements"></a>子元素


没有子元素。

## <a name="parent-elements"></a>父元素


<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th>元素</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="documentfinalparameters.md" data-raw-source="[&lt;strong&gt;DocumentFinalParameters&lt;/strong&gt;](documentfinalparameters.md)"><strong>DocumentFinalParameters</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="documentparameters.md" data-raw-source="[&lt;strong&gt;DocumentParameters&lt;/strong&gt;](documentparameters.md)"><strong>DocumentParameters</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

如果图像**格式**元素不受支持，然后扫描程序必须拒绝请求并返回**ClientErrorDocumentFormatNotSupported**错误代码。

当扫描程序会发出**ClientErrorDocumentFormatNotSupported**错误代码，因为它不支持的图像格式，然后 WSD 扫描程序驱动程序将尝试按以下顺序查找一种格式选择其他图像格式扫描程序支持。

1. 选择 PNG (W3C PNG) 格式时，如果扫描仪支持。

2. 选择 EXIF 格式时，如果扫描仪支持和颜色模式与 RGB (24bpp) 或灰度 (8pp)。

3. 选择 G4 单页 TIFF (tiff 单 g4) 格式时，如果扫描仪支持和颜色模式是单色 (1bpp)。

4. 选择未压缩的单页 TIFF （tiff-单个的未压缩） 格式时，如果扫描仪支持。

从 Windows 7 开始，支持自动配置扫描 WIA。 如果请求时自动配置扫描使用 DIB 格式，但扫描程序不支持 DIB 格式，然后 WSD 扫描程序驱动程序使用上述步骤中所示相同的算法选择扫描程序支持的图像格式。

**请注意**  颜色模式不是可选择自动配置的扫描。

 

WSD 扫描服务可以指定可选**重写**并**UsedDefault**属性时，才**格式**元素包含在**DocumentFinalParameters**层次结构。 有关详细信息**重写**并**UsedDefault**及其使用情况，请参阅[ **DocumentFinalParameters**](documentfinalparameters.md)。

可以同时扩展并创建此元素的允许值的子集。

虽然 WSD 扫描服务支持 JBIG 文件格式 (ISO/IEC 11544:1993)，但它目前不支持 JBIG2 (ISO/IEC 14492:2001)。

## <a name="see-also"></a>另请参阅


[**DocumentFinalParameters**](documentfinalparameters.md)

[**DocumentParameters**](documentparameters.md)

[**FormatValue**](formatvalue.md)

 

 






