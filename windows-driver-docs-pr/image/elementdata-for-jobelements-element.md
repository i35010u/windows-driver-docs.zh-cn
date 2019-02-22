---
title: ElementData JobElements 元素
description: 所需的 ElementData 元素包含为作业相关架构请求返回的数据。
ms.assetid: 6d9724cd-c076-4c87-9c01-ec2c16cd2aac
keywords:
- ElementData JobElements 元素成像设备
topic_type:
- apiref
api_name:
- wscn ElementData Name "" Valid ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34b2dbef96920aacc59fe924cd3b73b633eeb8fb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522288"
---
# <a name="elementdata-for-jobelements-element"></a>ElementData JobElements 元素


所需**ElementData**元素包含为作业相关架构请求返回的数据。

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
<p>必需。 以下 QName 值： xmlns:JobStatusReturn 当前 JobStatusschema.xmlns:ScanTicketReturn ScanTicket element.xmlns:DocumentsReturn 文档 element.xmlns:VendorSectionGet 供应商定义的标识部分之一对 WSD 扫描服务扩展。</p></td>
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
<td><p>供应商定义的任何元素</p></td>
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

WSD 扫描服务将返回**ElementData**中的元素[ **GetJobElementsResponse** ](getjobelementsresponse.md)操作元素。

## <a name="see-also"></a>另请参阅


[**文档**](documents.md)

[**GetJobElementsResponse**](getjobelementsresponse.md)

[**JobElements**](jobelements.md)

[**JobStatus**](jobstatus.md)

[**ScanTicket**](scanticket.md)

 

 






