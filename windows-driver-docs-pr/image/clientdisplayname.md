---
title: ClientDisplayName 元素
description: 所需的 ClientDisplayName 元素指定扫描程序应在其用户界面中显示的字符串。
ms.assetid: e43e5c51-5f8e-47af-b5da-707b89401935
keywords:
- ClientDisplayName 元素成像设备
topic_type:
- apiref
api_name:
- wscn ClientDisplayName
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 252523edba3eea7350b9a096c0b9b5ee50df5d7e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563862"
---
# <a name="clientdisplayname-element"></a>ClientDisplayName 元素


所需**ClientDisplayName**元素指定扫描程序应在其用户界面中显示的字符串。

<a name="usage"></a>用法
-----

```xml
<wscn:ClientDisplayName>
  text
</wscn:ClientDisplayName>
```

<a name="attributes"></a>特性
----------

没有特性。

<a name="text-value"></a>文本值
----------

必需。 任何有效字符的字符串。

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
<td><p><a href="scandestination.md" data-raw-source="[&lt;strong&gt;ScanDestination&lt;/strong&gt;](scandestination.md)"><strong>ScanDestination</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

显示的名称，用户可以选择作为扫描目标的请求的客户端。 当用户选择此显示名称，并按扫描按钮时，WSD 扫描服务即会发送[ **ScanAvailableEvent** ](scanavailableevent.md)订阅接收它扫描目标的事件。

## <a name="see-also"></a>请参阅


[**ScanAvailableEvent**](scanavailableevent.md)

[**ScanDestination**](scandestination.md)

 

 






