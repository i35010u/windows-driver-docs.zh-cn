---
title: WIA \_ IPS \_ 打印机 \_ ENDORSER \_ 最多 \_ 字符数
description: WIA \_ IPS \_ PRINTER \_ ENDORSER \_ MAX \_ 字符属性描述了 Imprinter/ENDORSER 项可以在每一页上打印或认可) 的最大字符数 (不包括 NULL 终止符。
keywords:
- WIA_IPS_PRINTER_ENDORSER_MAX_CHARACTERS 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_MAX_CHARACTERS
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ea80a8aca8f1a9acc82d1d7f03571a3d4504c58
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830445"
---
# <a name="wia_ips_printer_endorser_max_characters"></a>WIA \_ IPS \_ 打印机 \_ ENDORSER \_ 最多 \_ 字符数


**WIA \_ IPS \_ PRINTER \_ ENDORSER \_ MAX \_ 字符** 属性描述了 Imprinter/ENDORSER 项可以在每一页上打印或认可) 的最大字符数 (不包括 NULL 终止符。 此属性由 WIA 迷你驱动程序初始化和维护，并且在 Windows 8 及更高版本的 Windows 中可用。

属性类型： VT \_ UI4

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

**WIA \_ IPS \_ PRINTER \_ ENDORSER \_ MAX \_ 字符** 属性必须由所有 Imprinter/ENDORSER 项支持。 实现时，属性值 **必须** 大于零 (0) 。

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

 

 





