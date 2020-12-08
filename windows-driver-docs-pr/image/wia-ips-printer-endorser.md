---
title: WIA \_ IPS \_ PRINTER \_ ENDORSER
description: '\_ \_ \_ WIA 微型驱动程序使用 wia IPS PRINTER ENDORSER 属性列出打印机/ENDORSER 设备的可用位置，并由应用程序用来选择其中一个位置以启用 imprinting/认可。'
keywords:
- WIA_IPS_PRINTER_ENDORSER 图像设备
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
ms.openlocfilehash: edbdf8fc436e5e1355e5333ed73679b322b738f3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783209"
---
# <a name="wia_ips_printer_endorser"></a>WIA \_ IPS \_ PRINTER \_ ENDORSER


WIA 微型驱动程序使用 **wia \_ IPS \_ PRINTER \_ ENDORSER** 属性列出打印机/ENDORSER 设备的可用位置，并由应用程序用来选择其中一个位置以启用 imprinting/认可。 WIA 微型驱动程序创建并维护此属性。




属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表

访问权限：读/写

<a name="remarks"></a>备注
-------

下表描述了 **WIA \_ IPS \_ PRINTER \_ ENDORSER** 属性的必需值。

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
<td><p>禁用打印/认可。 这是属性的必需默认值。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINTER_ENDORSER_AUTO</p></td>
<td><p>启用打印/认可。 如果此 imprinter/endorser 有多个位置可用于此/) ，则在运行时，设备会根据活动的扫描输入源自动选择一个位置 (。</p></td>
</tr>
</tbody>
</table>

 

允许 WIA 微型驱动程序接受属性配置，但在扫描时，它将忽略为非活动扫描输入源启用打印/认可的请求。

下表描述了 **WIA \_ IPS \_ PRINTER \_ ENDORSER** 属性的可选值。

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
<td><p>对于在平板扫描仪上扫描的文档，会启用打印/认可。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINTER_ENDORSER_FEEDER_FRONT</p></td>
<td><p>为通过送纸器扫描的文档的正面启用打印/签署 (在单面或双工图像扫描模式) 。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PRINTER_ENDORSER_FEEDER_BACK</p></td>
<td><p>为通过送纸器扫描的文档的背面启用打印/认可 (在单面或双工图像扫描模式) 。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINTER_ENDORSER_FEEDER_DUPLEX</p></td>
<td><p>为通过送纸器扫描的文档两侧启用打印/认可 (在单面或双工图像扫描模式) 。</p></td>
</tr>
</tbody>
</table>

 

此属性必须受所有 Imprinter/Endorser 数据源项支持。 所需的默认值为 " **WIA \_ PRINTER \_ ENDORSER \_ DISABLED**"。

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

 

 





