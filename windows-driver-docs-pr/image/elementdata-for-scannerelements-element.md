---
title: ElementData ScannerElements 元素
description: 所需的 ElementData 元素包含为扫描程序相关架构请求返回的数据。
ms.assetid: 852a7f8a-cd87-467b-8793-8a7d7943f2a9
keywords:
- ElementData ScannerElements 元素成像设备
topic_type:
- apiref
api_name:
- wscn ElementData Name "" Valid ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: df93a1b4bbc408cff1de244b816cdc714a45eae9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554078"
---
# <a name="elementdata-for-scannerelements-element"></a>ElementData ScannerElements 元素


所需**ElementData**元素包含为扫描程序相关架构请求返回的数据。

<a name="usage"></a>用法
-----

```xml
<wscn:ElementData Name="" Valid=""
  Name = "xs:string"
  Valid = "xs:string">
  child elements
</wscn:ElementData Name="" Valid="">
```

<a name="attributes"></a>属性
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
<th>在任务栏的搜索框中键入</th>
<th>必需</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong><strong>名称</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p></p>
<p>必需。 以下 QNames:xmlns:ScannerDescriptionReturn currentScannerDescription schema.xmlns:ScannerConfigurationReturn 当前 ScannerConfiguration schema.xmlns:ScannerStatusReturn 当前 ScannerStatus schema.xmlns:D 之一efaultScanTicketReturn 当前 DefaultScanTicket schema.xmlns:VendorSectionReturn 到 WSD 扫描服务供应商定义的扩展的标识部分。</p></td>
</tr>
<tr class="even">
<td><p><strong><strong>有效</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p></p>
<p>必需。 一个布尔值，必须为 0，为 false，1 或 true。</p></td>
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

在客户端调用[ **GetScannerElementsRequest** ](getscannerelementsrequest.md)来确定扫描程序相关的元素的值。 WSD 扫描服务将返回此信息**ElementData**通过元素[ **GetScannerElementsResponse** ](getscannerelementsresponse.md)操作。

QName 值**名称**属性必须为架构关键字，表示为其客户端请求的信息在 WSD 扫描服务中的顶级节。 命名空间前缀和冒号分隔的有效元素名称，必须指定扫描服务。

**有效**属性指示客户端提供的架构关键字是否有效。 WSD 扫描服务将此属性设置为 **，则返回 true**如果它可以将请求的架构关键字映射到有效部分的架构; 否则，它必须将此属性设置**false**。

## <a name="see-also"></a>另请参阅


[**DefaultScanTicket**](defaultscanticket.md)

[**GetScannerElementsRequest**](getscannerelementsrequest.md)

[**GetScannerElementsResponse**](getscannerelementsresponse.md)

[**ScannerConfiguration**](scannerconfiguration.md)

[**ScannerDescription**](scannerdescription.md)

[**ScannerElements**](scannerelements.md)

[**ScannerStatus**](scannerstatus.md)

 

 






