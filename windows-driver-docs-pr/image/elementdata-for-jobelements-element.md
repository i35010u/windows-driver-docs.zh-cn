---
title: JobElements 元素的 ElementData
description: 必需的 ElementData 元素包含为与作业相关的架构请求返回的数据。
keywords:
- ElementData for JobElements element Imaging 设备
topic_type:
- apiref
api_name:
- wscn ElementData Name "" Valid ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09f303aff4a64595b3a50abc7ae4b5295a344e16
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818969"
---
# <a name="elementdata-for-jobelements-element"></a>JobElements 元素的 ElementData


必需的 **ElementData** 元素包含为与作业相关的架构请求返回的数据。

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
<p>必需。 以下 QName 值之一： xmlns： JobStatusReturn 当前 JobStatusschema.xmlns： ScanTicketReturn ScanTicket element.xmlns： DocumentsReturn 文档 element.xmlns： VendorSectionGet 标识的供应商定义的扩展到 WSD 扫描服务的部分。</p></td>
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
<td><p>任何供应商定义的元素</p></td>
</tr>
<tr class="even">
<td><p><a href="documents.md" data-raw-source="[&lt;strong&gt;Documents&lt;/strong&gt;](documents.md)"><strong>文档</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="jobstatus.md" data-raw-source="[&lt;strong&gt;JobStatus&lt;/strong&gt;](jobstatus.md)"><strong>JobStatus</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="scanticket.md" data-raw-source="[&lt;strong&gt;ScanTicket&lt;/strong&gt;](scanticket.md)"><strong>ScanTicket</strong></a></p></td>
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
<td><p><a href="jobelements.md" data-raw-source="[&lt;strong&gt;JobElements&lt;/strong&gt;](jobelements.md)"><strong>JobElements</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

WSD 扫描服务返回 [**GetJobElementsResponse**](getjobelementsresponse.md)操作元素中的 **ElementData** 元素。

## <a name="see-also"></a>请参阅


[**文档**](documents.md)

[**GetJobElementsResponse**](getjobelementsresponse.md)

[**JobElements**](jobelements.md)

[**JobStatus**](jobstatus.md)

[**ScanTicket**](scanticket.md)

 

 






