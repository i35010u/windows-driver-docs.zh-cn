---
title: ScannerStatusSummaryEvent element
description: 所需的 ScannerStatusSummaryEvent 元素告知客户端扫描设备的状态已更改。
ms.assetid: a1297e25-1136-49ef-8b8e-e7c8c62bec13
keywords:
- ScannerStatusSummaryEvent 元素成像设备
topic_type:
- apiref
api_name:
- wscn ScannerStatusSummaryEvent
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc4a96a329fa4ced7e8ab9c4b33b69742d802d43
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569379"
---
# <a name="scannerstatussummaryevent-element"></a>ScannerStatusSummaryEvent element


所需**ScannerStatusSummaryEvent**元素告知客户端扫描设备的状态已更改。

<a name="usage"></a>用法
-----

```xml
<wscn:ScannerStatusSummaryEvent>
  child elements
</wscn:ScannerStatusSummaryEvent>
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
<td><p><a href="statussummary.md" data-raw-source="[&lt;strong&gt;StatusSummary&lt;/strong&gt;](statussummary.md)"><strong>StatusSummary</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>父元素


没有父元素。

<a name="remarks"></a>备注
-------

WSD 扫描服务应发送**ScannerStatusSummaryEvent**到客户端扫描设备的状态发生更改时的元素。

正文**ScannerStatusSummaryEvent**必须包含[ **StatusSummary** ](statussummary.md)描述对扫描程序的状态更改的元素。

<a name="examples"></a>示例
--------

下面的代码示例指示由于媒体源路径在卡纸问题而停止时扫描设备。

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
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/ScannerStatusSummaryEvent
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
  </soap:Header>

  <soap:Body>
    <wscn:ScannerStatusSummaryEvent>
      <wscn:StatusSummary>
        <wscn:ScannerState>Stopped</wscn:ScannerState>
        <wscn:ScannerStateReasons>
          <wscn:ScannerStateReason>MediaJam</wscn:ScannerStateReason>
        </wscn:ScannerStateReasons>
      </wscn:StatusSummary>
    </wscn:ScannerStatusSummaryEvent>
  </soap:Body
</soap:Envelope>
```

## <a name="see-also"></a>请参阅


[**StatusSummary**](statussummary.md)

 

 






