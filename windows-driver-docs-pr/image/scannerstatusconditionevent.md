---
title: ScannerStatusConditionEvent 元素
description: 必需的 ScannerStatusConditionEvent 元素为客户端提供有关扫描设备中单个状态更改的详细信息。
keywords:
- ScannerStatusConditionEvent 元素图像设备
topic_type:
- apiref
api_name:
- wscn ScannerStatusConditionEvent
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2de595a6ea5df725ec591d647af1f440d80600bf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816195"
---
# <a name="scannerstatusconditionevent-element"></a>ScannerStatusConditionEvent 元素


必需的 **ScannerStatusConditionEvent** 元素为客户端提供有关扫描设备中单个状态更改的详细信息。

<a name="usage"></a>使用情况
-----

```xml
<wscn:ScannerStatusConditionEvent>
  child elements
</wscn:ScannerStatusConditionEvent>
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
<td><p><a href="devicecondition.md" data-raw-source="[&lt;strong&gt;DeviceCondition&lt;/strong&gt;](devicecondition.md)"><strong>DeviceCondition</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>父元素


没有父元素。

<a name="remarks"></a>备注
-------

当在 [**ActiveConditions**](activeconditions.md)元素表中添加或更改 [**DeviceCondition**](devicecondition.md)元素时，WSD 扫描服务会向客户端发送一个 **ScannerStatusConditionEvent** 元素。 **ScannerStatusConditionEvent** 的主体包含新的或已更改的 **DeviceCondition** 元素。

清除报告的 **DeviceCondition** 时，WSD 扫描服务应将 [**ScannerStatusConditionClearedEvent**](scannerstatusconditionclearedevent.md)元素发送到客户端。

<a name="examples"></a>示例
--------

下面的代码示例演示扫描设备如何向客户端通知扫描灯泡故障。

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
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/ScannerStatusConditionEvent
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
  </soap:Header>

  <soap:Body>
    <wscn:ScannerStatusConditionEvent>
      <wscn:DeviceCondition wscn:Id="1543">
        <wscn:Time>2006-01-21T17:22:27.5242689Z</wscn:Time>
        <wscn:Name>LampError</wscn:Name>
        <wscn:Component>Platen</wscn:Component>
        <wscn:Severity>Critical</wscn:Severity>
      </wscn:DeviceCondition>
    </wscn:ScannerStatusConditionEvent>
  </soap:Body
</soap:Envelope>
```

## <a name="see-also"></a>请参阅

[**ActiveConditions**](activeconditions.md)

[**DeviceCondition**](devicecondition.md)

[**ScannerStatusConditionClearedEvent**](scannerstatusconditionclearedevent.md)
