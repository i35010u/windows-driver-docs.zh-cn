---
title: WIA \_ IPS \_ PRINTER \_ ENDORSER \_ 填充
description: WIA \_ IPS \_ PRINTER \_ ENDORSER \_ 填充属性配置打印或认可以填充计数器、数据和时间序列中空格的有效特殊空白字符。
keywords:
- WIA_IPS_PRINTER_ENDORSER_PADDING 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_PADDING
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 548dfed3f4f1f8c546242f05b14d6a4486ed5fe8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839525"
---
# <a name="wia_ips_printer_endorser_padding"></a>WIA \_ IPS \_ PRINTER \_ ENDORSER \_ 填充


**WIA \_ IPS \_ PRINTER \_ ENDORSER \_ 填充** 属性配置打印或认可以填充计数器、数据和时间序列中空格的有效特殊空白字符。 此属性由 WIA 迷你驱动程序初始化和维护，并且在 Windows 8 及更高版本的 Windows 中可用。

属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表

访问权限： Read-Write

<a name="remarks"></a>备注
-------

下表显示了此属性的有效值。

| Value                      | 描述                                        |
|----------------------------|----------------------------------------------------|
| WIA \_ 打印 \_ 填充 \_ 无  | 不填充。                                        |
| WIA \_ 打印 \_ 填充 \_ 零  | 零 (0) 数字用作填充字符。 |
| WIA \_ 打印 \_ 填充 \_ 空白 | 空格 (空白) 字符用于填充。   |

 

对于 Imprinter/Endorser 项， **WIA \_ IPS \_ PRINTER \_ ENDORSER \_ 填充** 属性是可选的。 如果此属性不受支持，则 printer/endorser 设备不支持填充。

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

 

 





