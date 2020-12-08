---
title: CompressionQualityFactor 元素
description: 可选的 CompressionQualityFactor 元素指定理想化的图像质量的整数量，范围为0到100。
keywords:
- CompressionQualityFactor 元素图像设备
topic_type:
- apiref
api_name:
- wscn CompressionQualityFactor wscn MustHonor "" wscn Override "" wscn UsedDefault ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81e4945ffdaba420a6c8d615f2c12ab23f4587b5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783919"
---
# <a name="compressionqualityfactor-element"></a>CompressionQualityFactor 元素


可选的 **CompressionQualityFactor** 元素指定理想化的图像质量的整数量，范围为0到100。

<a name="usage"></a>使用情况
-----

```xml
<wscn:CompressionQualityFactor wscn:MustHonor=""                               wscn:Override=""                               wscn:UsedDefault=""
  MustHonor = "xs:string"
  Override = "xs:string"
  UsedDefault = "xs:string">
  text
</wscn:CompressionQualityFactor wscn:MustHonor=""                               wscn:Override=""                               wscn:UsedDefault="">
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
<td><p><strong><strong>MustHonor</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p></p>
<p>可选。 必须为0、false、1或 true 的布尔值。<strong>falsetrue</strong></p></td>
</tr>
<tr class="even">
<td><p><strong><strong>忽略</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p></p>
<p>可选。 必须为0、false、1或 true 的布尔值。<strong>falsetrue</strong></p></td>
</tr>
<tr class="odd">
<td><p><strong><strong>UsedDefault</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p></p>
<p>可选。 必须为0、false、1或 true 的布尔值。<strong>falsetrue</strong></p></td>
</tr>
</tbody>
</table>

<a name="text-value"></a>文本值
----------

必需。 介于0到100之间的整数。

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

任何损压缩类型都使用整数值来确定可接受的图像丢失量，其中较高的值表示较高的图像质量和更大的文件大小。 如果值为100，则表示设备应该使用它支持的压缩量最少，以获得尽可能高的图像质量。 目前，JPEG 压缩是唯一受支持的有损压缩类型。

如果请求的映像压缩类型为无损，并且 **MustHonor** 不存在或者为 **FALSE**，则 WSD 扫描服务应忽略 **CompressionQualityFactor** 元素，而改用值100。 如果压缩类型为无损并且 **MustHonor** 为 **true**，则当指定100以外的值时，WSD 扫描服务应拒绝 [**ScanTicket**](scanticket.md) 元素。

仅当 **CompressionQualityFactor** 元素包含在 **CreateScanJobRequest** 层次结构内时，客户端才能指定可选的 **MustHonor** 属性。 有关 **MustHonor** 及其用法的详细信息，请参阅 [**CreateScanJobRequest**](createscanjobrequest.md)。

仅当 **CompressionQualityFactor** 元素包含在 **DocumentFinalParameters** 层次结构中时，WSD 扫描服务才能指定可选 **Override** 和 **UsedDefault** 属性。 有关 **Override** 和 **UsedDefault** 及其用法的详细信息，请参阅 [**DocumentFinalParameters**](documentfinalparameters.md)。

可以将此元素的允许值作为子集。

## <a name="see-also"></a>请参阅


[**CreateScanJobRequest**](createscanjobrequest.md)

[**DocumentFinalParameters**](documentfinalparameters.md)

[**DocumentParameters**](documentparameters.md)

 

 






