---
title: ScannerStatusConditionClearedEvent 元素
description: 必需的 ScannerStatusConditionClearedEvent 元素通知客户端在扫描程序中清除了之前报告的 DeviceCondition 条件。
ms.assetid: c849caba-d77b-441b-a5e1-94f9285cef3f
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
ms.openlocfilehash: 84e2d28c03d35c8f81c245dc1a8fbe584fec0cc7
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/03/2020
ms.locfileid: "75653009"
---
# <a name="scannerstatusconditionclearedevent-element"></a>ScannerStatusConditionClearedEvent 元素


必需的**ScannerStatusConditionClearedEvent**元素通知客户端在扫描程序中清除了之前报告的[**DeviceCondition**](devicecondition.md)条件。

<a name="usage"></a>Usage
-----

```xml
<wscn:ScannerStatusConditionClearedEvent>
  child elements
</wscn:ScannerStatusConditionClearedEvent>
```

<a name="attributes"></a>属性
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

当[**ScannerStatusConditionEvent**](scannerstatusconditionevent.md)中标识的设备条件已清除时，WSD 扫描服务将发送**ScannerStatusConditionClearedEvent**元素。 **ScannerStatusConditionClearedEvent**包含一个[**DeviceConditionCleared**](deviceconditioncleared.md)元素，该元素包含清除的条件和清除它的时间。

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

## <a name="see-also"></a>另请参阅

[**ConditionId**](conditionid.md)

[**DeviceCondition**](devicecondition.md)

[**DeviceConditionCleared**](deviceconditioncleared.md)

[**ScannerStatusConditionEvent**](scannerstatusconditionevent.md)
