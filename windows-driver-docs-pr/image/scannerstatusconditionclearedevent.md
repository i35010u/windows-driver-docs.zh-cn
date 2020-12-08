---
title: ScannerStatusConditionClearedEvent 元素
description: 必需的 ScannerStatusConditionClearedEvent 元素通知客户端在扫描程序中清除了之前报告的 DeviceCondition 条件。
keywords:
- ScannerStatusConditionClearedEvent 元素图像设备
topic_type:
- apiref
api_name:
- wscn ScannerStatusConditionClearedEvent
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1257569063e33d05b800f1fff45402b2e4ae7a8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816197"
---
# <a name="scannerstatusconditionclearedevent-element"></a>ScannerStatusConditionClearedEvent 元素


必需的 **ScannerStatusConditionClearedEvent** 元素通知客户端在扫描程序中清除了之前报告的 [**DeviceCondition**](devicecondition.md) 条件。

<a name="usage"></a>使用情况
-----

```xml
<wscn:ScannerStatusConditionClearedEvent>
  child elements
</wscn:ScannerStatusConditionClearedEvent>
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
<td><p><a href="deviceconditioncleared.md" data-raw-source="[&lt;strong&gt;DeviceConditionCleared&lt;/strong&gt;](deviceconditioncleared.md)"><strong>DeviceConditionCleared</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>父元素


没有父元素。

<a name="remarks"></a>备注
-------

当 [**ScannerStatusConditionEvent**](scannerstatusconditionevent.md)中标识的设备条件已清除时，WSD 扫描服务将发送 **ScannerStatusConditionClearedEvent** 元素。 **ScannerStatusConditionClearedEvent** 包含一个 [**DeviceConditionCleared**](deviceconditioncleared.md) 元素，该元素包含清除的条件和清除它的时间。

<a name="examples"></a>示例
--------

下面的代码示例演示设备如何通知客户端： ConditionId 1543 标识的上一个条件已清除：

```xml
<soap:Envelope
  xmlns:soap="https://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="https://schemas.xmlsoap.org/ws/2004/08/addressing"
  xmlns:wse="https://schemas.xmlsoap.org/ws/2004/08/eventing"
  xmlns:wscn="https://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='https://www.w3.org/2002/12/soap-encoding'>

  <soap:Header>
    <wsa:To>AddressofEventSink</wsa:To>
    <wsa:Action>
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/ScannerStatusConditionClearedEvent
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
  </soap:Header>

  <soap:Body>
    <wscn:ScannerStatusConditionClearedEvent>
      <wscn:DeviceConditionCleared>
        <wscn:ConditionId>1543</wscn:ConditionId>
        <wscn:ConditionClearTime>
          2006-01-21T17:22:35.8345Z
        </wscn:ConditionClearTime>
      </wscn:DeviceConditionCleared>
    </wscn:ScannerStatusConditionClearedEvent>
  </soap:Body
</soap:Envelope>
```

## <a name="see-also"></a>请参阅

[**ConditionId**](conditionid.md)

[**DeviceCondition**](devicecondition.md)

[**DeviceConditionCleared**](deviceconditioncleared.md)

[**ScannerStatusConditionEvent**](scannerstatusconditionevent.md)
