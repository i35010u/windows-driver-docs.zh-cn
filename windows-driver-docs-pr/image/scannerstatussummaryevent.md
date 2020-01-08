---
title: ScannerStatusSummaryEvent 元素
description: 必需的 ScannerStatusSummaryEvent 元素通知客户端扫描设备的状态已更改。
ms.assetid: a1297e25-1136-49ef-8b8e-e7c8c62bec13
keywords:
- ScannerStatusSummaryEvent 元素图像设备
topic_type:
- apiref
api_name:
- wscn ScannerStatusSummaryEvent
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89df739aaf5cd6b3d5800b0848984f1733444f7f
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/03/2020
ms.locfileid: "75653003"
---
# <a name="scannerstatussummaryevent-element"></a>ScannerStatusSummaryEvent 元素


必需的**ScannerStatusSummaryEvent**元素通知客户端扫描设备的状态已更改。

<a name="usage"></a>Usage
-----

```xml
<wscn:ScannerStatusSummaryEvent>
  child elements
</wscn:ScannerStatusSummaryEvent>
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
<td><p><a href="statussummary.md" data-raw-source="[&lt;strong&gt;StatusSummary&lt;/strong&gt;](statussummary.md)"><strong>StatusSummary</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>父元素


没有父元素。

<a name="remarks"></a>备注
-------

当扫描设备的状态发生更改时，WSD 扫描服务应将**ScannerStatusSummaryEvent**元素发送到客户端。

**ScannerStatusSummaryEvent**的主体必须包含一个[**StatusSummary**](statussummary.md)元素，该元素描述对扫描程序状态的更改。

<a name="examples"></a>示例
--------

下面的代码示例指示由于介质馈送路径中的卡纸，扫描设备已停止。

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
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/ScannerStatusSummaryEvent
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

## <a name="see-also"></a>另请参阅


[**StatusSummary**](statussummary.md)

 

 






