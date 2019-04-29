---
title: ElementChanges 元素
description: 所需的 ElementChanges 元素包含对 ScannerDescription、 ScannerConfiguration、 DefaultScanTicket 和供应商扩展元素的更改。
ms.assetid: d6f1d188-beb6-4ea3-a362-de64d8d8dacb
keywords:
- ElementChanges 元素成像设备
topic_type:
- apiref
api_name:
- wscn ElementChanges
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67a3307002c9315605924a70c2837265ad0af3a6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364461"
---
# <a name="elementchanges-element"></a>ElementChanges 元素


所需**ElementChanges**元素包含的更改[ **ScannerDescription**](scannerdescription.md)， [ **ScannerConfiguration**](scannerconfiguration.md)， [ **DefaultScanTicket**](defaultscanticket.md)，和供应商扩展元素。

<a name="usage"></a>用法
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

WSD 扫描服务必须包括**ElementChanges**元素时它将生成[ **ScannerElementsChangeEvent** ](scannerelementschangeevent.md)元素。 每个子元素**ElementChanges**必须包含所有必需的子元素。 如果返回的 XML 中缺少可选元素，WSD 扫描服务表示向客户端中，该服务不再支持该元素。

## <a name="see-also"></a>请参阅


[**DefaultScanTicket**](defaultscanticket.md)

[**ScannerConfiguration**](scannerconfiguration.md)

[**ScannerDescription**](scannerdescription.md)

[**ScannerElementsChangeEvent**](scannerelementschangeevent.md)

 

 






