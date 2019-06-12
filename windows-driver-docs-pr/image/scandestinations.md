---
title: ScanDestinations 元素
description: 所需的 ScanDestinations 元素是所有客户端想要使用扫描设备注册的扫描目标的集合。
ms.assetid: 50f87269-4d95-4653-ba93-aa752bdc9168
keywords:
- ScanDestinations 元素成像设备
topic_type:
- apiref
api_name:
- wscn ScanDestinations
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f05c61058b070b9ababa8112169b6a3f407fc377
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364368"
---
# <a name="scandestinations-element"></a>ScanDestinations 元素


所需**ScanDestinations**元素是所有客户端想要使用扫描设备注册的扫描目标的集合。

<a name="usage"></a>用法
-----

```xml
<wscn:ScanDestinations>
  child elements
</wscn:ScanDestinations>
```

<a name="attributes"></a>特性
----------

没有特性。

<a name="text-value"></a>文本值
----------

无

## <a name="child-elements"></a>子元素


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
<td><p><a href="scandestination.md" data-raw-source="[&lt;strong&gt;ScanDestination&lt;/strong&gt;](scandestination.md)"><strong>ScanDestination</strong></a></p></td>
</tr>
</tbody>
</table>

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
<td><p>&lt;wse:Subscribe&gt;</p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

客户端必须发送**ScanDestinations**中的元素 **&lt;wse： 订阅&gt;** 请求操作元素，将注册一个或多个扫描目标 WSD 扫描服务。 客户端订阅之前从 WSD 扫描服务获取扫描票证信息的客户端安装过程。 **&lt;Wse： 订阅&gt;** 规范中定义元素。

**ScanDestinations**元素提供客户端可以灵活地同时注册多个唯一扫描目标。

## <a name="see-also"></a>请参阅


[**ScanDestination**](scandestination.md)

 

 






