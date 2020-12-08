---
title: ScanDestinations 元素
description: 必需的 ScanDestinations 元素是客户端想要向扫描设备注册的所有扫描目标的集合。
keywords:
- ScanDestinations 元素图像设备
topic_type:
- apiref
api_name:
- wscn ScanDestinations
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3865439dbf64015a95c5e5745021deff76d93eff
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841263"
---
# <a name="scandestinations-element"></a>ScanDestinations 元素


必需的 **ScanDestinations** 元素是客户端想要向扫描设备注册的所有扫描目标的集合。

<a name="usage"></a>使用情况
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
<td><p>&lt;wse：订阅&gt;</p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

客户端必须发送 **&lt; Wse：订阅 &gt;** 请求操作元素中的 **ScanDestinations** 元素，以将一个或多个扫描目标注册到 WSD 扫描服务。 在客户端安装过程中，客户端在从 WSD 扫描服务获取扫描票证信息之前进行订阅。 在规范中定义了 **&lt; Wse：订阅 &gt;** 元素。

**ScanDestinations** 元素为客户端提供一次注册多个唯一扫描目标的灵活性。

## <a name="see-also"></a>请参阅


[**ScanDestination**](scandestination.md)

 

 






