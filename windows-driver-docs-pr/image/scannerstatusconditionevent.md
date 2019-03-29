---
title: ScannerStatusConditionEvent 元素
description: 所需的 ScannerStatusConditionEvent 元素提供有关中扫描设备的单个状态更改的详细信息的客户端。
ms.assetid: 0a61fe67-ea1e-4143-afb8-edcdf50ee7c4
keywords:
- ScannerStatusConditionEvent 元素成像设备
topic_type:
- apiref
api_name:
- wscn ScannerStatusConditionEvent
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f017efb6e15d450f79c169d21ecffde4be19fee2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576794"
---
# <a name="scannerstatusconditionevent-element"></a>ScannerStatusConditionEvent 元素


所需**ScannerStatusConditionEvent**元素提供有关中扫描设备的单个状态更改的详细信息的客户端。

<a name="usage"></a>用法
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

WSD 扫描服务发送**ScannerStatusConditionEvent**向客户端的元素时[ **DeviceCondition** ](devicecondition.md)元素已添加或更改在[ **ActiveConditions** ](activeconditions.md)元素表。 正文**ScannerStatusConditionEvent**包含新的或已更改**DeviceCondition**元素。

WSD 扫描服务应发送[ **ScannerStatusConditionClearedEvent** ](scannerstatusconditionclearedevent.md)到客户端的元素时报告**DeviceCondition**已被清除。

<a name="examples"></a>示例
--------

下面的代码示例显示了扫描设备通知有关扫描 lamp 失败的客户端的方式。

```xml
<soap:Envelope
  xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="http://schemas.xmlsoap.org/ws/2004/08/addressing"
  xmlns:wse="http://schemas.xmlsoap.org/ws/2004/08/eventing"
  xmlns:wscn="http://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='http://www.w3.org/2002/12/soap-encoding'>

  <soap:Header>
    <wsa:To>AddressofEventSink</wsa:To>
    <wsa:Action>
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/ScannerStatusConditionEvent
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
