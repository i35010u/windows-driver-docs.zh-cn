---
title: RequestedElements 元素名称
description: 此必需的 Name 元素标识客户端希望数据为当调用 GetScannerElementsRequest 或 GetJobElementsRequest WSD 扫描服务架构的一部分。
ms.assetid: 1b2bc3b4-24de-4957-a72a-6788425dc3b9
keywords:
- RequestedElements 元素图像处理设备名称
topic_type:
- apiref
api_name:
- wscn Name
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4b37e6430ebba91062f593a6fc048a6d4f42264
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576507"
---
# <a name="name-for-requestedelements-element"></a>RequestedElements 元素名称


这需要**名称**元素标识客户端希望数据为当调用的 WSD 扫描服务架构的一部分[ **GetScannerElementsRequest** ](getscannerelementsrequest.md)或[**GetJobElementsRequest**](getjobelementsrequest.md)。

<a name="usage"></a>用法
-----

```xml
<wscn:Name>
  text
</wscn:Name>
```

<a name="attributes"></a>特性
----------

没有特性。

<a name="text-value"></a>文本值
----------

必需。

有关[ **GetScannerElementsRequest**](getscannerelementsrequest.md)，以下的 QName 值之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>QName</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><span id="wscn_ScannerDescription"></span><span id="wscn_scannerdescription"></span><span id="WSCN_SCANNERDESCRIPTION"></span>wscn:ScannerDescription</p></td>
<td><p>获取所有扫描设备的描述性信息。</p></td>
</tr>
<tr class="even">
<td><p><span id="wscn_ScannerConfiguration"></span><span id="wscn_scannerconfiguration"></span><span id="WSCN_SCANNERCONFIGURATION"></span>wscn:ScannerConfiguration</p></td>
<td><p>获取所有扫描设备的配置信息。</p></td>
</tr>
<tr class="odd">
<td><p><span id="wscn_ScannerStatus"></span><span id="wscn_scannerstatus"></span><span id="WSCN_SCANNERSTATUS"></span>wscn:ScannerStatus</p></td>
<td><p>获取整个状态部分中，包括<a href="activeconditions.md" data-raw-source="[&lt;strong&gt;ActiveConditions&lt;/strong&gt;](activeconditions.md)"> <strong>ActiveConditions</strong> </a>并<a href="conditionhistory.md" data-raw-source="[&lt;strong&gt;ConditionHistory&lt;/strong&gt;](conditionhistory.md)"> <strong>ConditionHistory</strong></a>。</p></td>
</tr>
<tr class="even">
<td><p><span id="xmlns_VendorSection"></span><span id="xmlns_vendorsection"></span><span id="XMLNS_VENDORSECTION"></span>xmlns:VendorSection</p></td>
<td><p>获取到 WSD 扫描服务供应商定义的扩展的标识部分。</p></td>
</tr>
</tbody>
</table>

 

有关[ **GetJobElementsRequest**](getjobelementsrequest.md)，以下的 QName 值之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>QName</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><span id="wscn_JobStatus"></span><span id="wscn_jobstatus"></span><span id="WSCN_JOBSTATUS"></span>wscn:JobStatus</p></td>
<td><p>获取当前<a href="jobstatus.md" data-raw-source="[&lt;strong&gt;JobStatus&lt;/strong&gt;](jobstatus.md)"> <strong>JobStatus</strong> </a>元素指定作业的数据。</p></td>
</tr>
<tr class="even">
<td><p><span id="wscn_ScanTicket"></span><span id="wscn_scanticket"></span><span id="WSCN_SCANTICKET"></span>wscn:ScanTicket</p></td>
<td><p>获取<a href="scanticket.md" data-raw-source="[&lt;strong&gt;ScanTicket&lt;/strong&gt;](scanticket.md)"> <strong>ScanTicket</strong> </a>元素指定作业的数据。</p></td>
</tr>
<tr class="odd">
<td><p><span id="wscn_Documents"></span><span id="wscn_documents"></span><span id="WSCN_DOCUMENTS"></span>wscn:Documents</p></td>
<td><p>获取<a href="documents.md" data-raw-source="[&lt;strong&gt;Documents&lt;/strong&gt;](documents.md)"><strong>文档</strong></a>元素指定作业的数据。</p></td>
</tr>
<tr class="even">
<td><p><span id="xmlns_VendorSection"></span><span id="xmlns_vendorsection"></span><span id="XMLNS_VENDORSECTION"></span>xmlns:VendorSection</p></td>
<td><p>获取到 WSD 扫描服务供应商定义的扩展的标识部分。</p></td>
</tr>
</tbody>
</table>

 

## <a name="child-elements"></a>子元素


没有子元素。

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
<td><p><a href="requestedelements.md" data-raw-source="[&lt;strong&gt;RequestedElements&lt;/strong&gt;](requestedelements.md)"><strong>RequestedElements</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

Qname 必须标识客户端希望获得有关的信息的 WSD 扫描服务架构中的顶级元素。 客户端必须指定架构命名空间和元素名称。

## <a name="see-also"></a>请参阅


[**GetJobElementsRequest**](getjobelementsrequest.md)

[**ActiveConditions**](activeconditions.md)

[**ConditionHistory**](conditionhistory.md)

[**文档**](documents.md)

**GetJobElementsRequest**
[**GetScannerElementsRequest**](getscannerelementsrequest.md)

[**JobStatus**](jobstatus.md)

[**RequestedElements**](requestedelements.md)

[**ScanTicket**](scanticket.md)

 

 






