---
title: ClientDisplayName 元素
description: 必需的 ClientDisplayName 元素指定扫描程序应在其用户界面中显示的字符串。
keywords:
- ClientDisplayName 元素图像设备
topic_type:
- apiref
api_name:
- wscn ClientDisplayName
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 040b474bce5242e9f7c88006a4c93f5b8a7ca2e6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798175"
---
# <a name="clientdisplayname-element"></a>ClientDisplayName 元素


必需的 **ClientDisplayName** 元素指定扫描程序应在其用户界面中显示的字符串。

<a name="usage"></a>使用情况
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

必需。 任何有效的字符串。

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
<td><p><a href="scandestination.md" data-raw-source="[&lt;strong&gt;ScanDestination&lt;/strong&gt;](scandestination.md)"><strong>ScanDestination</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

显示的名称使用户能够选择请求客户端作为扫描目标。 当用户选择此显示名称并按下 "扫描" 按钮时，WSD 扫描服务会将 [**ScanAvailableEvent**](scanavailableevent.md) 事件发送到订阅接收它的扫描目标。

## <a name="see-also"></a>请参阅


[**ScanAvailableEvent**](scanavailableevent.md)

[**ScanDestination**](scandestination.md)

 

 






