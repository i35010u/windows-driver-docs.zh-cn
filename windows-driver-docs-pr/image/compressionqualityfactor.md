---
title: CompressionQualityFactor 元素
description: 可选 CompressionQualityFactor 元素指定的图像质量的理想化的整数金额在 0 到 100 范围内。
ms.assetid: e66ab41d-3f77-4c60-b0bf-d050f467c6b4
keywords:
- CompressionQualityFactor 元素成像设备
topic_type:
- apiref
api_name:
- wscn CompressionQualityFactor wscn MustHonor "" wscn Override "" wscn UsedDefault ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae5c6b719bab6d10143944b21870bb9e5f641787
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373188"
---
# <a name="compressionqualityfactor-element"></a>CompressionQualityFactor 元素


可选**CompressionQualityFactor**元素指定的图像质量的理想化的整数金额在 0 到 100 范围内。

<a name="usage"></a>用法
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
<th>特性</th>
<th>在任务栏的搜索框中键入</th>
<th>必需</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong><strong>MustHonor</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p></p>
<p>可选。 一个布尔值，必须为 0，为 false，1 或 true。<strong>falsetrue</strong></p></td>
</tr>
<tr class="even">
<td><p><strong><strong>Override</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p></p>
<p>可选。 一个布尔值，必须为 0，为 false，1 或 true。<strong>falsetrue</strong></p></td>
</tr>
<tr class="odd">
<td><p><strong><strong>UsedDefault</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p></p>
<p>可选。 一个布尔值，必须为 0，为 false，1 或 true。<strong>falsetrue</strong></p></td>
</tr>
</tbody>
</table>

<a name="text-value"></a>文本值
----------

必需。 从 0 到 100 范围内的整数。

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

任何有损压缩类型使用的整数值来确定可接受映像丢失量较高值表示较高的图像质量并相应地更大的文件大小。 值为 100 指示设备应使用它支持以生成的最大的图像质量可能的压缩量最少。 目前，JPEG 压缩是唯一受支持的有损压缩类型。

如果请求的图像的压缩类型是无损并**MustHonor**不存在或者是**false**，WSD 扫描服务应忽略**CompressionQualityFactor**元素，并改为使用的值为 100。 如果是无损的压缩类型和**MustHonor**是**true**，WSD 扫描服务应拒绝[ **ScanTicket** ](scanticket.md)元素如果指定 100 以外的值。

客户端可以指定可选**MustHonor**属性时，才**CompressionQualityFactor**元素包含在**CreateScanJobRequest**层次结构。 有关详细信息**MustHonor**及其使用情况，请参阅[ **CreateScanJobRequest**](createscanjobrequest.md)。

WSD 扫描服务可以指定可选**重写**并**UsedDefault**属性时，才**CompressionQualityFactor**元素包含在内**DocumentFinalParameters**层次结构。 有关详细信息**重写**并**UsedDefault**及其使用情况，请参阅[ **DocumentFinalParameters**](documentfinalparameters.md)。

你可以部分为此元素允许的值。

## <a name="see-also"></a>请参阅


[**CreateScanJobRequest**](createscanjobrequest.md)

[**DocumentFinalParameters**](documentfinalparameters.md)

[**DocumentParameters**](documentparameters.md)

 

 






