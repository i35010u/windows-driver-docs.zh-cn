---
title: ImagesToTransfer 元素
description: 可选的 ImagesToTransfer 元素指定要扫描的当前作业的映像数。
keywords:
- ImagesToTransfer 元素图像设备
topic_type:
- apiref
api_name:
- wscn ImagesToTransfer wscn MustHonor "" wscn Override "" wscn UsedDefault ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90522b4d4f628a99de7efb5df7f650b6423d70ea
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824127"
---
# <a name="imagestotransfer-element"></a>ImagesToTransfer 元素


可选的 **ImagesToTransfer** 元素指定要扫描的当前作业的映像数。

<a name="usage"></a>使用情况
-----

```xml
<wscn:ImagesToTransfer wscn:MustHonor=""                       wscn:Override=""                       wscn:UsedDefault=""
  MustHonor = "xs:string"
  Override = "xs:string"
  UsedDefault = "xs:string">
  text
</wscn:ImagesToTransfer wscn:MustHonor=""                       wscn:Override=""                       wscn:UsedDefault="">
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

必需。 介于0到2147483648之间的整数。

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

扫描设备具有的文档送纸器可以包含比当前作业更多的介质页面时， **ImagesToTransfer** 值非常有用。

如果该值为0，则设备将扫描在 [**InputSource**](inputsource.md) 元素中指定的所选输入源的可用页数。 如果输入源为 **影印** 或 **胶片**，则 **ImagesToTransfer** 中的值为0将生成单个图像采集。 如果输入源为 **ADF** 或 **ADFDuplex**，则 **ImagesToTransfer** 中的值为0，表示设备应获取图像，直到送纸器为空。

当设备从 **ADFDuplex** 获取图像时，介质的每一侧都表示一个图像。 如果为 **ADFDuplex** 指定了奇数值，设备将仅获取最后一张纸的前端。

仅当 **ImagesToTransfer** 元素包含在 **CreateScanJobRequest** 层次结构内时，客户端才能指定可选的 **MustHonor** 属性。 有关 **MustHonor** 及其用法的详细信息，请参阅 [**CreateScanJobRequest**](createscanjobrequest.md)。

仅当 **ImagesToTransfer** 元素包含在 **DocumentFinalParameters** 层次结构中时，WSD 扫描服务才能指定可选 **Override** 和 **UsedDefault** 属性。 有关 **Override** 和 **UsedDefault** 及其用法的详细信息，请参阅 [**DocumentFinalParameters**](documentfinalparameters.md)。

## <a name="see-also"></a>请参阅


[**CreateScanJobRequest**](createscanjobrequest.md)

[**DocumentFinalParameters**](documentfinalparameters.md)

[**DocumentParameters**](documentparameters.md)

[**InputSource**](inputsource.md)

 

 






