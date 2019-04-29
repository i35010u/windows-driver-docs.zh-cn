---
title: ScanDestination 元素
description: 所需的 ScanDestination 元素指定客户端上的单个扫描目标。
ms.assetid: 3cd685b2-36b2-4f28-a80f-a68204631e0c
keywords:
- ScanDestination 元素成像设备
topic_type:
- apiref
api_name:
- wscn ScanDestination
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a09785e727e2d1e16102b94ddac5b301b3f66cc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364385"
---
# <a name="scandestination-element"></a>ScanDestination 元素


所需**ScanDestination**元素指定客户端上的单个扫描目标。

<a name="usage"></a>用法
-----

```xml
<wscn:ScanDestination>
  child elements
</wscn:ScanDestination>
```

<a name="attributes"></a>特性
----------

没有特性。

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
<td><p><a href="clientcontext.md" data-raw-source="[&lt;strong&gt;ClientContext&lt;/strong&gt;](clientcontext.md)"><strong>ClientContext</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="clientdisplayname.md" data-raw-source="[&lt;strong&gt;ClientDisplayName&lt;/strong&gt;](clientdisplayname.md)"><strong>ClientDisplayName</strong></a></p></td>
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
<td><p><a href="scandestinations.md" data-raw-source="[&lt;strong&gt;ScanDestinations&lt;/strong&gt;](scandestinations.md)"><strong>ScanDestinations</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

客户端包括一个或多个**ScanDestination**中的元素**ScanDestinations**时创建的订阅发送的元素。 WSD 扫描服务使用中提供的信息**ScanDestination**以创建相应[ **ScanAvailableEvent** ](scanavailableevent.md)事件元素。

## <a name="see-also"></a>请参阅


[**ClientContext**](clientcontext.md)

[**ClientDisplayName**](clientdisplayname.md)

[**ScanAvailableEvent**](scanavailableevent.md)

[**ScanDestinations**](scandestinations.md)

 

 






