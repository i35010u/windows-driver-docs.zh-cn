---
title: ScannerElements 元素的 ElementData
description: 必需的 ElementData 元素包含为与扫描程序相关的架构请求返回的数据。
keywords:
- ElementData for ScannerElements element Imaging 设备
topic_type:
- apiref
api_name:
- wscn ElementData Name "" Valid ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7c28dbd677322efe82d0cab83f8b5d3b41744cf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819553"
---
# <a name="elementdata-for-scannerelements-element"></a>ScannerElements 元素的 ElementData


必需的 **ElementData** 元素包含为与扫描程序相关的架构请求返回的数据。

<a name="usage"></a>使用情况
-----

```xml
<wscn:ElementData Name="" Valid=""
  Name = "xs:string"
  Valid = "xs:string">
  child elements
</wscn:ElementData Name="" Valid="">
```

<a name="attributes"></a>特性
----------

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>类型</th>
<th>必须</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong><strong>“属性”</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p></p>
<p>必需。 以下 QNames： xmlns： ScannerDescriptionReturn 中的一种： currentScannerDescription schema.xmlns： ScannerConfigurationReturn 当前 ScannerConfiguration schema.xmlns： ScannerStatusReturn 当前 ScannerStatus schema.xmlns： DefaultScanTicketReturn 当前 DefaultScanTicket schema.xmlns： VendorSectionReturn 已识别供应商定义的扩展到 WSD 扫描服务的部分。</p></td>
</tr>
<tr class="even">
<td><p><strong><strong>有效</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p></p>
<p>必需。 必须为0、false、1或 true 的布尔值。</p></td>
</tr>
</tbody>
</table>

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
<tr class="even">
<td><p><a href="scannerstatus.md" data-raw-source="[&lt;strong&gt;ScannerStatus&lt;/strong&gt;](scannerstatus.md)"><strong>ScannerStatus</strong></a></p></td>
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
<td><p><a href="scannerelements.md" data-raw-source="[&lt;strong&gt;ScannerElements&lt;/strong&gt;](scannerelements.md)"><strong>ScannerElements</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

客户端调用 [**GetScannerElementsRequest**](getscannerelementsrequest.md) 来确定与扫描程序相关的元素的值。 WSD 扫描服务通过 [**GetScannerElementsResponse**](getscannerelementsresponse.md)操作在 **ElementData** 元素中返回此信息。

**Name** 属性的 QName 值必须是一个 schema 关键字，表示客户端请求其信息的 WSD 扫描服务内的顶级部分。 扫描服务必须同时指定命名空间前缀和有效的以冒号分隔的元素名称。

**有效** 的属性指示客户端提供的架构关键字是否有效。 如果 WSD 扫描服务可以将请求的架构关键字映射到其架构的有效部分，则将此特性设置为 **true** ;否则，它必须将此属性设置为 **false**。

## <a name="see-also"></a>请参阅


[**DefaultScanTicket**](defaultscanticket.md)

[**GetScannerElementsRequest**](getscannerelementsrequest.md)

[**GetScannerElementsResponse**](getscannerelementsresponse.md)

[**ScannerConfiguration**](scannerconfiguration.md)

[**ScannerDescription**](scannerdescription.md)

[**ScannerElements**](scannerelements.md)

[**ScannerStatus**](scannerstatus.md)

 

 






