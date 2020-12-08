---
title: FormatValue 元素
description: 必需的 FormatValue 元素指定一种受支持的文件格式和压缩类型。
keywords:
- FormatValue 元素图像设备
topic_type:
- apiref
api_name:
- wscn FormatValue
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08bcec47a34bcaf7f9364a4db3325595dd2819b9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808235"
---
# <a name="formatvalue-element"></a>FormatValue 元素


必需的 **FormatValue** 元素指定一种受支持的文件格式和压缩类型。

<a name="usage"></a>使用情况
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
<td><p>与 Windows 设备无关的位图。</p></td>
</tr>
<tr class="even">
<td><p><span id="exif"></span><span id="EXIF"></span>exif</p></td>
<td><p>可交换图像文件格式版本2.x。</p></td>
</tr>
<tr class="odd">
<td><p><span id="jbig"></span><span id="JBIG"></span>jbig</p></td>
<td><p>ISO/IEC 11544:1993 标准编码表示形式的图片和音频信息;渐进式 bi 级别图像压缩。</p></td>
</tr>
<tr class="even">
<td><p><span id="jfif"></span><span id="JFIF"></span>jfif</p></td>
<td><p>JPEG 文件交换格式1.x。</p></td>
</tr>
<tr class="odd">
<td><p><span id="jpeg2k"></span><span id="JPEG2K"></span>jpeg2k</p></td>
<td><p>JPEG 2000 基于标准的文件格式和压缩。</p></td>
</tr>
<tr class="even">
<td><p><span id="pdf-a"></span><span id="PDF-A"></span>pdf-a</p></td>
<td><p>PDF/格式 (标准版基于 ISO/CD 19005-1) 。</p></td>
</tr>
<tr class="odd">
<td><p><span id="png"></span><span id="PNG"></span>png</p></td>
<td><p>可移植网络图形 (PNG) 格式。 此格式仅支持 PNG 压缩类型。</p></td>
</tr>
<tr class="even">
<td><p><span id="tiff-single-uncompressed"></span><span id="TIFF-SINGLE-UNCOMPRESSED"></span>tiff-单压缩</p></td>
<td><p>不带压缩类型的单页面 TIFF 文件。</p></td>
</tr>
<tr class="odd">
<td><p><span id="tiff-single-g4"></span><span id="TIFF-SINGLE-G4"></span>tiff-单 g4</p></td>
<td><p>具有 g4 压缩类型的单页面 TIFF 文件。</p></td>
</tr>
<tr class="even">
<td><p><span id="tiff-single-g3mh"></span><span id="TIFF-SINGLE-G3MH"></span>tiff-g3mh</p></td>
<td><p>具有 g3mh 压缩类型的单页面 TIFF 文件。</p></td>
</tr>
<tr class="odd">
<td><p><span id="tiff-single-jpeg-tn2"></span><span id="TIFF-SINGLE-JPEG-TN2"></span>tiff-单 jpeg-tn2</p></td>
<td><p>带有 jpeg 压缩类型的单页面 TIFF 文件，如技术说明2中所述。</p></td>
</tr>
<tr class="even">
<td><p><span id="tiff-multi-uncompressed"></span><span id="TIFF-MULTI-UNCOMPRESSED"></span>tiff-多未压缩</p></td>
<td><p>不带压缩类型的多个页面 TIFF 文件。</p></td>
</tr>
<tr class="odd">
<td><p><span id="tiff-multi-g4"></span><span id="TIFF-MULTI-G4"></span>tiff-多 g4</p></td>
<td><p>具有 g4 压缩类型的多页 TIFF 文件。</p></td>
</tr>
<tr class="even">
<td><p><span id="tiff-multi-g3mh"></span><span id="TIFF-MULTI-G3MH"></span>tiff-多 g3mh</p></td>
<td><p>多页面 TIFF 文件，其中包含 g3mh 压缩类型。</p></td>
</tr>
<tr class="odd">
<td><p><span id="tiff-multi-jpeg-tn2"></span><span id="TIFF-MULTI-JPEG-TN2"></span>tiff-多 jpeg-tn2</p></td>
<td><p>多页面 TIFF 文件，其中包含 jpeg 压缩类型，如技术说明2中所述。</p></td>
</tr>
<tr class="even">
<td><p><span id="xps"></span><span id="XPS"></span>xps</p></td>
<td><p>XML 纸张规范。</p></td>
</tr>
<tr class="odd">
<td><p><span id="Any_vendor-defined_values."></span><span id="any_vendor-defined_values."></span><span id="ANY_VENDOR-DEFINED_VALUES."></span>供应商定义的任何值。</p></td>
<td></td>
</tr>
</tbody>
</table>

 

## <a name="child-elements"></a>子元素


没有任何子元素。

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

可以扩展和子集化此元素的允许值。

尽管 WSD 扫描服务支持 JBIG 文件格式 (ISO/IEC 11544:1993) ，但目前 *不* 支持 JBIG2 (ISO/iec 14492:2001) 。

## <a name="see-also"></a>请参阅


[**FormatsSupported**](formatssupported.md)

 

 






