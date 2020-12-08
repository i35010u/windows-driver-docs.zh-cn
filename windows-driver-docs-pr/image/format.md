---
title: 格式元素
description: 可选的 Format 元素指示扫描程序支持的单个文件格式和压缩类型。
keywords:
- 设置元素图像处理设备的格式
topic_type:
- apiref
api_name:
- wscn Format wscn Override "" wscn UsedDefault ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e112cd55f78fa8b3789e970b9f53a91e27a7107b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808239"
---
# <a name="format-element"></a>格式元素


可选的 **Format** 元素指示扫描程序支持的单个文件格式和压缩类型。

<a name="usage"></a>使用情况
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

<a name="attributes"></a>特性
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
<th>类型</th>
<th>必须</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>忽略</strong></p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p></p>
<p>可选。 必须为0、 <strong>false</strong>、1或 <strong>true</strong>的布尔值。</p></td>
</tr>
<tr class="even">
<td><p><strong>UsedDefault</strong></p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p></p>
<p>可选。 必须为0、 <strong>false</strong>、1或 <strong>true</strong>的布尔值。</p></td>
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
<td><p>带有 JPEG 压缩类型的单页面 TIFF 文件，如技术说明2中所述。</p></td>
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
<td><p>带有 JPEG 压缩类型的多页 TIFF 文件，如技术说明2中所述。</p></td>
</tr>
<tr class="even">
<td><p><span id="xps"></span><span id="XPS"></span>xps</p></td>
<td><p>XML 纸张规范</p></td>
</tr>
<tr class="odd">
<td><p><span id="Any_vendor-defined_values"></span><span id="any_vendor-defined_values"></span><span id="ANY_VENDOR-DEFINED_VALUES"></span>任何供应商定义的值</p></td>
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
<td><p><a href="documentfinalparameters.md" data-raw-source="[&lt;strong&gt;DocumentFinalParameters&lt;/strong&gt;](documentfinalparameters.md)"><strong>DocumentFinalParameters</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="documentparameters.md" data-raw-source="[&lt;strong&gt;DocumentParameters&lt;/strong&gt;](documentparameters.md)"><strong>DocumentParameters</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

如果图像 **格式** 元素不受支持，则扫描程序必须拒绝请求并返回 **ClientErrorDocumentFormatNotSupported** 错误代码。

当扫描程序发出 **ClientErrorDocumentFormatNotSupported** 错误代码时，因为它不支持图像格式，因此 WSD 扫描器驱动程序将尝试按以下顺序选择其他图像格式，以查找扫描程序支持的格式。

1. 如果扫描程序支持 PNG (W3C PNG) 格式。

2. 选中 "EXIF 格式"，如果扫描程序支持它，并且颜色模式与 RGB (24bpp) 或灰度 (8pp) 匹配。

3. 选择 G4 单页 TIFF (tiff-单 g4) 格式，如果扫描程序和彩色模式支持单色 (1bpp) 。

4. 如果扫描程序支持未压缩的单页 TIFF (tiff-单未压缩的) 格式。

从 Windows 7 开始，WIA 支持自动配置的扫描。 如果请求使用 DIB 格式自动配置的扫描，但扫描程序不支持 DIB 格式，则 WSD 扫描器驱动程序将使用前面步骤中所示的相同算法来选择扫描仪支持的图像格式。

**注意**  对于自动配置的扫描，颜色模式不可选择。

 

仅当 **Format** 元素包含在 **DocumentFinalParameters** 层次结构中时，WSD 扫描服务才能指定 optional **Override** 和 **UsedDefault** 属性。 有关 **Override** 和 **UsedDefault** 及其用法的详细信息，请参阅 [**DocumentFinalParameters**](documentfinalparameters.md)。

您可以扩展和创建此元素允许的值的子集。

尽管 WSD 扫描服务支持 JBIG 文件格式 (ISO/IEC 11544:1993) ，但目前不支持 JBIG2 (ISO/IEC 14492:2001) 。

## <a name="see-also"></a>请参阅


[**DocumentFinalParameters**](documentfinalparameters.md)

[**DocumentParameters**](documentparameters.md)

[**FormatValue**](formatvalue.md)

 

 






