---
title: ScanIdentifier 元素
description: 所需的 ScanIdentifier 元素包含一个通过 ScanAvailableEvent 事件提供扫描程序的特定于设备的字符串。
ms.assetid: 77116871-63dc-4388-9b36-a553219ddcf7
keywords:
- ScanIdentifier 元素成像设备
topic_type:
- apiref
api_name:
- wscn ScanIdentifier
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4140becbe6f6162c9e5d0307d40955f2090f243d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364389"
---
# <a name="scanidentifier-element"></a>ScanIdentifier 元素


所需**ScanIdentifier**元素包含一个通过提供扫描程序的特定于设备的字符串[ **ScanAvailableEvent** ](scanavailableevent.md)事件。

<a name="usage"></a>用法
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
<td><p><a href="createscanjobrequest.md" data-raw-source="[&lt;strong&gt;CreateScanJobRequest&lt;/strong&gt;](createscanjobrequest.md)"><strong>CreateScanJobRequest</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="scanavailableevent.md" data-raw-source="[&lt;strong&gt;ScanAvailableEvent&lt;/strong&gt;](scanavailableevent.md)"><strong>ScanAvailableEvent</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

客户端可以发送**ScanIdentifier**元素中的 WSD 扫描服务[ **CreateScanJobRequest** ](createscanjobrequest.md)操作元素。 WSD 扫描服务可以使用**ScanIdentifier**以确保用户已选定目标之后，请求正确的客户端扫描。

**ScanIdentifier**值必须是唯一的每个[ **ScanAvailableEvent** ](scanavailableevent.md)实例。

## <a name="see-also"></a>请参阅


[**CreateScanJobRequest**](createscanjobrequest.md)

[**ScanAvailableEvent**](scanavailableevent.md)

 

 






