---
title: WIA \_ IPS \_ 打印机 \_ ENDORSER \_ 图形
description: WIA \_ IPS \_ PRINTER \_ ENDORSER \_ GRAPHICS 属性用于报告 Imprinter/ENDORSER 项是否支持图形和图像数据以及文本。
keywords:
- WIA_IPS_PRINTER_ENDORSER_GRAPHICS 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_GRAPHICS
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8965f8b7332a65bbce0e5e2620a0c7ac59ae7ab
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798159"
---
# <a name="wia_ips_printer_endorser_graphics"></a>WIA \_ IPS \_ 打印机 \_ ENDORSER \_ 图形


**WIA \_ IPS \_ PRINTER \_ ENDORSER \_ GRAPHICS** 属性用于报告 Imprinter/ENDORSER 项是否支持图形和图像数据以及文本。 通常，设备使用图形在文本附近打印/签署文本，或使用图形作为背景图像。 WIA 微型驱动程序创建并维护此属性。




属性类型： VT \_ I4 (布尔) 

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

如果支持 **WIA \_ IPS \_ 打印机 \_ ENDORSER \_ 图形** ，并将其值设置为非零值 (True) ，则 Imprinter/ENDORSER 支持图形数据。

所有 Imprinter/Endorser 项都需要此属性，但可以实现此属性，以便始终报告值 0 (False) 。

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

 

 





