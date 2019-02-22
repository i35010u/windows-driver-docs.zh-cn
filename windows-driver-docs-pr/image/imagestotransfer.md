---
title: ImagesToTransfer 元素
description: 可选 ImagesToTransfer 元素指定的映像扫描当前作业的数量。
ms.assetid: d3f06104-17a5-41e4-ab80-1228ee342b7d
keywords:
- ImagesToTransfer 元素成像设备
topic_type:
- apiref
api_name:
- wscn ImagesToTransfer wscn MustHonor "" wscn Override "" wscn UsedDefault ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ae87936af242793afcd036876a1a33700edf3bc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521853"
---
# <a name="imagestotransfer-element"></a>ImagesToTransfer 元素


可选**ImagesToTransfer**元素指定的映像扫描当前作业的数量。

<a name="usage"></a>用法
-----

```xml
<wscn:ImagesToTransfer wscn:MustHonor=""                       wscn:Override=""                       wscn:UsedDefault=""
  MustHonor = "xs:string"
  Override = "xs:string"
  UsedDefault = "xs:string">
  text
</wscn:ImagesToTransfer wscn:MustHonor=""                       wscn:Override=""                       wscn:UsedDefault="">
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

必需。 从 0 到 2147483648 范围内的整数。

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

**ImagesToTransfer**扫描设备具有可以包含的媒体比当前作业的更多页文档送纸器时，值很有用。

如果值为 0，设备会扫描可用于所选的输入源中指定的所有页面[ **InputSource** ](inputsource.md)元素。 如果输入的源**辊**或**电影**，值为 0 中**ImagesToTransfer**会产生单个映像获取。 如果输入的源**ADF**或**ADFDuplex**，值为 0 中**ImagesToTransfer**指示该设备应获取图像，直到送纸器为空。

当设备获取中的映像**ADFDuplex**，媒体的每一端表示单个图像。 为指定的奇数的值时**ADFDuplex**，设备将获取仅前方的媒体的最后一个表。

客户端可以指定可选**MustHonor**属性时，才**ImagesToTransfer**元素包含在**CreateScanJobRequest**层次结构。 有关详细信息**MustHonor**及其使用情况，请参阅[ **CreateScanJobRequest**](createscanjobrequest.md)。

WSD 扫描服务可以指定可选**重写**并**UsedDefault**属性时，才**ImagesToTransfer**元素包含在**DocumentFinalParameters**层次结构。 有关详细信息**重写**并**UsedDefault**及其使用情况，请参阅[ **DocumentFinalParameters**](documentfinalparameters.md)。

## <a name="see-also"></a>另请参阅


[**CreateScanJobRequest**](createscanjobrequest.md)

[**DocumentFinalParameters**](documentfinalparameters.md)

[**DocumentParameters**](documentparameters.md)

[**InputSource**](inputsource.md)

 

 






