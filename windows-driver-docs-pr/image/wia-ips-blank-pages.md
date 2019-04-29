---
title: WIA\_IPS\_空白\_页
description: WIA\_IPS\_空白\_页属性用于配置空白页检测。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: FB2EBC0D-6F09-4B64-9B79-7EE20CAF7023
keywords:
- WIA_IPS_BLANK_PAGES 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_BLANK_PAGES
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f8a3ab871c0188a73a86caa7078a7c1b332ac38
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370619"
---
# <a name="wiaipsblankpages"></a>WIA\_IPS\_空白\_页


**WIA\_IPS\_空白\_页**属性用于配置空白页检测。 WIA 微型驱动程序创建并维护此属性。




属性类型：VT\_I4

有效值：WIA\_PROP\_列表

访问权限：读/写

<a name="remarks"></a>备注
-------

下表描述了的有效值**WIA\_IPS\_空白\_页**属性。

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
<td><p>WIA_BLANK_PAGE_DETECTION_DISABLED</p></td>
<td><p>禁用空白页检测。 如果支持该属性，这是所需的默认值。</p></td>
</tr>
<tr class="even">
<td><p>WIA_BLANK_PAGE_DISCARD</p></td>
<td><p>设备检测空白页，并自动将跳过对其进行扫描 （如果有放弃扫描数据），并继续扫描。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BLANK_PAGE_JOB_SEPARATOR</p></td>
<td><p>设备检测到的空白页，并通过配置充当<a href="wia-ips-job-separators.md" data-raw-source="[&lt;strong&gt;WIA_IPS_JOB_SEPARATORS&lt;/strong&gt;](wia-ips-job-separators.md)"> <strong>WIA_IPS_JOB_SEPARATORS</strong> </a>属性。 仅当送纸器项支持时，此值才有效<strong>WIA_IPS_JOB_SEPARATORS</strong>属性。</p></td>
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

 

 





