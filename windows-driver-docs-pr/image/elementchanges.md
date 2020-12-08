---
title: ElementChanges 元素
description: 必需的 ElementChanges 元素包含对 ScannerDescription、ScannerConfiguration、DefaultScanTicket 和供应商扩展元素的更改。
keywords:
- ElementChanges 元素图像设备
topic_type:
- apiref
api_name:
- wscn ElementChanges
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ec5a483a91e7cea711a43df5d2ea4031af5c668
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818971"
---
# <a name="elementchanges-element"></a>ElementChanges 元素


必需的 **ElementChanges** 元素包含对 [**ScannerDescription**](scannerdescription.md)、 [**ScannerConfiguration**](scannerconfiguration.md)、 [**DefaultScanTicket**](defaultscanticket.md)和供应商扩展元素的更改。

<a name="usage"></a>使用情况
-----

```xml
<wscn:ElementChanges>
  child elements
</wscn:ElementChanges>
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
<td><p><a href="defaultscanticket.md" data-raw-source="[&lt;strong&gt;DefaultScanTicket&lt;/strong&gt;](defaultscanticket.md)"><strong>DefaultScanTicket</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="scannerconfiguration.md" data-raw-source="[&lt;strong&gt;ScannerConfiguration&lt;/strong&gt;](scannerconfiguration.md)"><strong>ScannerConfiguration</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="scannerdescription.md" data-raw-source="[&lt;strong&gt;ScannerDescription&lt;/strong&gt;](scannerdescription.md)"><strong>ScannerDescription</strong></a></p></td>
</tr>
</tbody>
</table>

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
<td><p><a href="scannerelementschangeevent.md" data-raw-source="[&lt;strong&gt;ScannerElementsChangeEvent&lt;/strong&gt;](scannerelementschangeevent.md)"><strong>ScannerElementsChangeEvent</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

当 WSD 扫描服务生成 [**ScannerElementsChangeEvent**](scannerelementschangeevent.md)元素时，它必须包含 **ElementChanges** 元素。 **ElementChanges** 的每个子元素都必须包含其所有必需的子元素。 如果返回的 XML 中缺少一个可选元素，则 WSD 扫描服务将向客户端指示该服务不再支持该元素。

## <a name="see-also"></a>请参阅


[**DefaultScanTicket**](defaultscanticket.md)

[**ScannerConfiguration**](scannerconfiguration.md)

[**ScannerDescription**](scannerdescription.md)

[**ScannerElementsChangeEvent**](scannerelementschangeevent.md)

 

 






