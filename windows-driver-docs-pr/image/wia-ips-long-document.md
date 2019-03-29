---
title: WIA\_IPS\_长\_文档
description: WIA\_IPS\_长\_WIA 微型驱动程序报告是否支持长的文档扫描和 WIA 的客户端应用程序，若要启用此功能使用文档属性。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: FEFB77EE-8377-406C-A244-84E1BEF57808
keywords:
- WIA_IPS_LONG_DOCUMENT 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_LONG_DOCUMENT
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3be2ca4a9d3f5b1842507ad9a8c79f874ed8358d
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57348588"
---
# <a name="wiaipslongdocument"></a>WIA\_IPS\_长\_文档


**WIA\_IPS\_长\_文档**属性使用 WIA 微型驱动程序报告是否支持长的文档扫描以及 WIA 的客户端应用程序，若要启用此功能。 WIA 微型驱动程序创建并维护此属性。




属性类型：VT\_I4

有效值：WIA\_PROP\_列表

访问权限：读/写

<a name="remarks"></a>备注
-------

下表描述了的有效值**WIA\_IPS\_长\_文档**属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ReplTest1</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_LONG_DOCUMENT_DISABLED</p></td>
<td><p>长的文档扫描已禁用。 如果支持该属性，这是所需的默认值。</p></td>
</tr>
<tr class="even">
<td><p>WIA_LONG_DOCUMENT_ENABLED</p></td>
<td><p>设备扫描设备的最大可能长度最长的文档。 <a href="wia-ips-page-size.md" data-raw-source="[&lt;strong&gt;WIA_IPS_PAGE_SIZE&lt;/strong&gt;](wia-ips-page-size.md)"> <strong>WIA_IPS_PAGE_SIZE</strong> </a>属性必须设置为此值的 WIA_PAGE_AUTO 才能被接受。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_LONG_DOCUMENT_SPLIT</p></td>
<td><p>长的文档会自动拆分 （和作为单独的映像传输） 在当前<a href="wia-ips-page-size.md" data-raw-source="[&lt;strong&gt;WIA_IPS_PAGE_SIZE&lt;/strong&gt;](wia-ips-page-size.md)"> <strong>WIA_IPS_PAGE_SIZE</strong> </a>长度。 扫描生成的最后一页可以更短的时间。</p></td>
</tr>
</tbody>
</table>

 

此属性是可选的并且仅对送纸器数据源项有效 (以表示[ **WIA\_IPA\_项\_类别**](wia-ipa-item-category.md)属性作为 WIA\_类别\_送纸器)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

 

 





