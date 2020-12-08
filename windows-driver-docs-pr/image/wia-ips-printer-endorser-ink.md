---
title: WIA \_ IPS \_ PRINTER \_ ENDORSER \_ INK
description: WIA \_ IPS \_ PRINTER \_ ENDORSER \_ INK 属性用于报告 Imprinter/ENDORSER 设备的当前墨水或碳粉状态。
keywords:
- WIA_IPS_PRINTER_ENDORSER_INK 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_INK
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9553781a3624e76041bca16b5794cacf744e0512
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798157"
---
# <a name="wia_ips_printer_endorser_ink"></a>WIA \_ IPS \_ PRINTER \_ ENDORSER \_ INK


**WIA \_ IPS \_ PRINTER \_ ENDORSER \_ INK** 属性用于报告 Imprinter/ENDORSER 设备的当前墨水或碳粉状态。 属性值指示剩余的可用墨迹，以占总容量的百分比表示。 例如，如果值为50，则表示剩余的墨水为半或50%。 此属性由 WIA 迷你驱动程序初始化和维护。 此功能适用于 windows 8 和更高版本的 Windows。

属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表

访问权限： Read-Write

<a name="remarks"></a>备注
-------

对于 Imprinter/Endorser 项， **WIA \_ IPS \_ PRINTER \_ ENDORSER \_ INK** 属性是可选的。 此属性的有效值介于0和100（含）之间。

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

 

 





