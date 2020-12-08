---
title: ScanIdentifier 元素
description: 必需的 ScanIdentifier 元素包含扫描程序通过 ScanAvailableEvent 事件提供的设备特定字符串。
keywords:
- ScanIdentifier 元素图像设备
topic_type:
- apiref
api_name:
- wscn ScanIdentifier
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c4e3e403576bfff474e931bf0adcd4ab91a5287
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841259"
---
# <a name="scanidentifier-element"></a>ScanIdentifier 元素


必需的 **ScanIdentifier** 元素包含扫描程序通过 [**ScanAvailableEvent**](scanavailableevent.md) 事件提供的设备特定字符串。

<a name="usage"></a>使用情况
-----

```xml
<wscn:ScanIdentifier>
  text
</wscn:ScanIdentifier>
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
<td><p><a href="createscanjobrequest.md" data-raw-source="[&lt;strong&gt;CreateScanJobRequest&lt;/strong&gt;](createscanjobrequest.md)"><strong>CreateScanJobRequest</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="scanavailableevent.md" data-raw-source="[&lt;strong&gt;ScanAvailableEvent&lt;/strong&gt;](scanavailableevent.md)"><strong>ScanAvailableEvent</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

客户端可以将 **ScanIdentifier** 元素发送到 [**CreateScanJobRequest**](createscanjobrequest.md) 操作元素中的 WSD 扫描服务。 WSD 扫描服务可以使用 **ScanIdentifier** 来确保正确的客户端在用户选择目标后请求扫描。

对于每个 [**ScanAvailableEvent**](scanavailableevent.md)实例， **ScanIdentifier** 值必须是唯一的。

## <a name="see-also"></a>请参阅


[**CreateScanJobRequest**](createscanjobrequest.md)

[**ScanAvailableEvent**](scanavailableevent.md)

 

 






