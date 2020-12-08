---
title: WIA \_ IPS \_ 长 \_ 文档
description: '\_ \_ Wia 微型驱动程序使用 "wia ip 长 \_ 文档" 属性来报告是否支持长文档扫描，以及 wia 客户端应用程序是否支持此功能。 WIA 微型驱动程序创建并维护此属性。'
keywords:
- WIA_IPS_LONG_DOCUMENT 图像设备
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
ms.openlocfilehash: 5f2edfed654b1e1b8b5d9593ce8d7fb6abbf0974
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825961"
---
# <a name="wia_ips_long_document"></a>WIA \_ IPS \_ 长 \_ 文档


WIA 微型驱动程序使用 " **wia \_ ip \_ 长 \_ 文档** " 属性来报告是否支持长文档扫描，以及 wia 客户端应用程序是否支持此功能。 WIA 微型驱动程序创建并维护此属性。




属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表

访问权限：读/写

<a name="remarks"></a>备注
-------

下表描述了 " **WIA \_ ip \_ 长 \_ 文档** " 属性的有效值。

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
<td><p>WIA_LONG_DOCUMENT_DISABLED</p></td>
<td><p>已禁用长文档扫描。 如果支持该属性，则这是所需的默认值。</p></td>
</tr>
<tr class="even">
<td><p>WIA_LONG_DOCUMENT_ENABLED</p></td>
<td><p>设备会扫描长文档，直到达到设备的最大可能长度。 <a href="wia-ips-page-size.md" data-raw-source="[&lt;strong&gt;WIA_IPS_PAGE_SIZE&lt;/strong&gt;](wia-ips-page-size.md)"><strong>WIA_IPS_PAGE_SIZE</strong></a>属性必须设置为 WIA_PAGE_AUTO 才能接受此值。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_LONG_DOCUMENT_SPLIT</p></td>
<td><p>长文档将自动拆分 (，并作为) 当前 <a href="wia-ips-page-size.md" data-raw-source="[&lt;strong&gt;WIA_IPS_PAGE_SIZE&lt;/strong&gt;](wia-ips-page-size.md)"><strong>WIA_IPS_PAGE_SIZE</strong></a> 长度的单独图像传输。 最后扫描的页面可能更短。</p></td>
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

 

 





