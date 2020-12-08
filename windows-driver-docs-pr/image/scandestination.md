---
title: ScanDestination 元素
description: 必需的 ScanDestination 元素在客户端上指定单个扫描目标。
keywords:
- ScanDestination 元素图像设备
topic_type:
- apiref
api_name:
- wscn ScanDestination
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92ba58780b407a47f22afebfb3fe7757a5e28ce5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840707"
---
# <a name="scandestination-element"></a>ScanDestination 元素


必需的 **ScanDestination** 元素在客户端上指定单个扫描目标。

<a name="usage"></a>使用情况
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

客户端在创建订阅时，在它发送的 **ScanDestinations** 元素中包含一个或多个 **ScanDestination** 元素。 WSD 扫描服务使用 **ScanDestination** 中提供的信息来创建相应的 [**ScanAvailableEvent**](scanavailableevent.md) 事件元素。

## <a name="see-also"></a>请参阅


[**ClientContext**](clientcontext.md)

[**ClientDisplayName**](clientdisplayname.md)

[**ScanAvailableEvent**](scanavailableevent.md)

[**ScanDestinations**](scandestinations.md)

 

 






