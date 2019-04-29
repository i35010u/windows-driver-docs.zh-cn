---
title: ScannerStatusConditionClearedEvent 元素
description: 所需的 ScannerStatusConditionClearedEvent 元素通知客户端已在扫描仪上中清除先前报告的 DeviceCondition 条件。
ms.assetid: c849caba-d77b-441b-a5e1-94f9285cef3f
keywords:
- ScannerStatusConditionClearedEvent 元素成像设备
topic_type:
- apiref
api_name:
- wscn ScannerStatusConditionClearedEvent
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7bee70559ed044dd9fd3a566e9d74c222f5daf3f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386304"
---
# <a name="scannerstatusconditionclearedevent-element"></a>ScannerStatusConditionClearedEvent 元素


所需**ScannerStatusConditionClearedEvent**元素将告知客户端的先前报告[ **DeviceCondition** ](devicecondition.md)条件已清除在扫描程序。

<a name="usage"></a>用法
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

WSD 扫描服务发送**ScannerStatusConditionClearedEvent**中标识元素时设备条件[ **ScannerStatusConditionEvent** ](scannerstatusconditionevent.md)已清除。 **ScannerStatusConditionClearedEvent**包含[ **DeviceConditionCleared** ](deviceconditioncleared.md)元素，其中包含已清除的条件并从该处清除它的时间。

<a name="examples"></a>示例
--------

下面的代码示例显示了设备通知前面所有条件 ConditionId 1543 标识已都清除的客户端的方式：

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
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/ScannerStatusConditionClearedEvent
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
