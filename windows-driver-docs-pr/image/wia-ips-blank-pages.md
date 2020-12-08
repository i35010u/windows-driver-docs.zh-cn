---
title: WIA \_ IP \_ 空白 \_ 页
description: "\"WIA \\_ ip \\_ 空白 \\_ 页\" 属性用于配置空白页检测。 WIA 微型驱动程序创建并维护此属性。"
keywords:
- WIA_IPS_BLANK_PAGES 图像设备
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
ms.openlocfilehash: ba0dbd2a0ba4137379a492526812b49591e66e6e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839909"
---
# <a name="wia_ips_blank_pages"></a>WIA \_ IP \_ 空白 \_ 页


" **WIA \_ ip \_ 空白 \_ 页** " 属性用于配置空白页检测。 WIA 微型驱动程序创建并维护此属性。




属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表

访问权限：读/写

<a name="remarks"></a>备注
-------

下表描述了 " **WIA \_ ip \_ 空白 \_ 页** " 属性的有效值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>值</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_BLANK_PAGE_DETECTION_DISABLED</p></td>
<td><p>禁用空白页检测。 如果支持该属性，则这是所需的默认值。</p></td>
</tr>
<tr class="even">
<td><p>WIA_BLANK_PAGE_DISCARD</p></td>
<td><p>设备会检测空白页面并自动跳过扫描， (如果任何) 并继续扫描，则会丢弃扫描的数据。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BLANK_PAGE_JOB_SEPARATOR</p></td>
<td><p>设备检测到空白页，并通过 <a href="wia-ips-job-separators.md" data-raw-source="[&lt;strong&gt;WIA_IPS_JOB_SEPARATORS&lt;/strong&gt;](wia-ips-job-separators.md)"><strong>WIA_IPS_JOB_SEPARATORS</strong></a> 属性进行配置。 仅当送纸器项支持 <strong>WIA_IPS_JOB_SEPARATORS</strong> 属性时，此值才有效。</p></td>
</tr>
</tbody>
</table>

 

此属性是可选的，仅对作为 WIA 类别送纸器) 在 [**wia \_ IPA \_ 项 \_ 类别**](wia-ipa-item-category.md) 属性中表示的送料器数据源 (项有效 \_ \_ 。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

 

 





