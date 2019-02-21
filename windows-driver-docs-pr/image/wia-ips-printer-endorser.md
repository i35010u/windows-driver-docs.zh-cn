---
title: WIA\_IPS\_打印机\_印记签署器
description: WIA\_IPS\_打印机\_WIA 微型驱动程序使用印记签署器属性来列出打印机/印记签署器设备不可用，并应用程序用于选择其中一个位置以便 imprinting 的位置/ 认可。
ms.assetid: A9BAC8D3-AB06-4600-9EF7-E9F4846B5215
keywords:
- WIA_IPS_PRINTER_ENDORSER 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ddbd707ae477f799c02d9a09f5cd30855b5f148
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526688"
---
# <a name="wiaipsprinterendorser"></a>WIA\_IPS\_打印机\_印记签署器


**WIA\_IPS\_打印机\_印记签署器**WIA 微型驱动程序使用属性来列出打印机/印记签署器设备不可用，并应用程序用于选择其中一个的位置若要启用 imprinting/认可这些位置。 WIA 微型驱动程序创建并维护此属性。




属性类型：VT\_I4

有效值：WIA\_PROP\_列表

访问权限：读/写

<a name="remarks"></a>备注
-------

下表描述了所需的值**WIA\_IPS\_打印机\_印记签署器**属性。

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
<td><p>WIA_PRINTER_ENDORSER_DISABLED</p></td>
<td><p>打印/认可处于禁用状态。 这是该属性所需的默认值。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINTER_ENDORSER_AUTO</p></td>
<td><p>启用打印/认可。 在运行时根据 active 扫描输入源位置 （如果有多个位置可用于此印刷器/印记签署器） 自动选择设备。</p></td>
</tr>
</tbody>
</table>

 

允许 WIA 微型驱动程序接受属性配置，但在扫描时它会忽略请求，以使打印/认可为非活动状态的扫描输入源。

下表描述的可选值**WIA\_IPS\_打印机\_印记签署器**属性。

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
<td><p>WIA_PRINTER_ENDORSER_FLATBED</p></td>
<td><p>打印/认可可用于在平板扫描仪上扫描的文档。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINTER_ENDORSER_FEEDER_FRONT</p></td>
<td><p>打印/认可可用于通过送纸器 （无论是在单工或双工映像扫描模式下） 已扫描文档的正面。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PRINTER_ENDORSER_FEEDER_BACK</p></td>
<td><p>打印/认可可用于通过送纸器 （无论是在单工或双工映像扫描模式下） 已扫描文档的后端。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINTER_ENDORSER_FEEDER_DUPLEX</p></td>
<td><p>打印/认可可用于通过送纸器 （无论是在单工或双工映像扫描模式下） 已扫描文档的双方。</p></td>
</tr>
</tbody>
</table>

 

此属性必须受所有印刷器/印记签署器数据源项。 所需的默认值是**WIA\_打印机\_印记签署器\_禁用**。

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
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

 

 





