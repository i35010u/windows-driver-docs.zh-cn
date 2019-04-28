---
title: FormatValue 元素
description: 所需的 FormatValue 元素指定一个受支持的文件格式和压缩类型。
ms.assetid: 0331f44d-6343-45f7-85a7-303733f3ee75
keywords:
- FormatValue 元素成像设备
topic_type:
- apiref
api_name:
- wscn FormatValue
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2dec49892f928256ff19657741f17f16b6b2eb4e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353343"
---
# <a name="formatvalue-element"></a>FormatValue 元素


所需**FormatValue**元素指定一个受支持的文件格式和压缩类型。

<a name="usage"></a>用法
-----

```xml
<wscn:FormatValue>
  text
</wscn:FormatValue>
```

<a name="attributes"></a>特性
----------

没有特性。

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
<td><p><span id="dib_"></span><span id="DIB_"></span>dib</p></td>
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
<td><p>单个页面 TIFF 文件 jpeg 压缩类型，如技术说明 2 中所述。</p></td>
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
<td><p>Jpeg 压缩类型技术说明 2 中所述的多个页 TIFF 文件。</p></td>
</tr>
<tr class="even">
<td><p><span id="xps"></span><span id="XPS"></span>xps</p></td>
<td><p>XML 纸张规范。</p></td>
</tr>
<tr class="odd">
<td><p><span id="Any_vendor-defined_values."></span><span id="any_vendor-defined_values."></span><span id="ANY_VENDOR-DEFINED_VALUES."></span>任何供应商定义的值。</p></td>
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
<td><p><a href="formatssupported.md" data-raw-source="[&lt;strong&gt;FormatsSupported&lt;/strong&gt;](formatssupported.md)"><strong>FormatsSupported</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

您都可以扩展和子集的允许的值为此元素。

尽管 WSD 扫描服务支持 JBIG 文件格式 (ISO/IEC 11544:1993)，这样*不*目前支持 JBIG2 (ISO/IEC 14492:2001)。

## <a name="see-also"></a>请参阅


[**FormatsSupported**](formatssupported.md)

 

 






