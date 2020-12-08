---
title: WIA \_ IPS \_ 打印机 \_ ENDORSER \_ 图形 \_ 最小 \_ 宽度
description: WIA \_ ips \_ printer \_ ENDORSER \_ graphics \_ MIN \_ width 属性连同 wia \_ ips \_ printer \_ ENDORSER \_ 图形 \_ 最大 \_ 宽度、wia \_ ips \_ printer \_ ENDORSER \_ 图形 \_ 最小 \_ 高度和 Wia \_ Ips \_ 打印机 ENDORSER 的 \_ \_ \_ 最大 \_ 高度可用于报告可上传到要呈现的 Imprinter/ENDORSER 的图像的最小和最大尺寸（以像素为单位）。 WIA 微型驱动程序创建并维护此属性。
keywords:
- WIA_IPS_PRINTER_ENDORSER_GRAPHICS_MIN_WIDTH 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_GRAPHICS_MIN_WIDTH
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8d03534fdfa6f1c6aad55ff48f7553a08b4e5ada
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791479"
---
# <a name="wia_ips_printer_endorser_graphics_min_width"></a>WIA \_ IPS \_ 打印机 \_ ENDORSER \_ 图形 \_ 最小 \_ 宽度


**Wia \_ ips \_ printer \_ ENDORSER \_ Graphics \_ MIN \_ width** 属性连同 [**wia \_ ips \_ printer \_ ENDORSER \_ 图形 \_ 最大 \_ 宽度**](wia-ips-printer-endorser-graphics-max-width.md)、 [**wia \_ ips \_ printer \_ ENDORSER \_ 图形 \_ 最小 \_ 高度**](wia-ips-printer-endorser-graphics-min-height.md)和 [**wia \_ ips \_ 打印机 ENDORSER 的 \_ \_ \_ 最大 \_ 高度**](wia-ips-printer-endorser-graphics-max-height.md)可用于报告可上传到要呈现的 Imprinter/ENDORSER 的图像的最小和最大尺寸（以像素为单位）。 WIA 微型驱动程序创建并维护此属性。




属性类型： VT \_ UI4

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

为 **wia \_ ips \_ 打印机 \_ ENDORSER \_ 图形 \_ 最小 \_ 宽度** 报告的值必须小于或等于为 [**wia \_ ips \_ 打印机 \_ ENDORSER \_ 图形 \_ 最大 \_ 宽度**](wia-ips-printer-endorser-graphics-max-width.md)报告的值。 为 [**wia ips 打印机 ENDORSER 报告的值： \_ \_ \_ \_ 图形 \_ 最小 \_ 高度**](wia-ips-printer-endorser-graphics-min-height.md) 必须小于或等于为 [**wia \_ ips \_ 打印机 \_ ENDORSER \_ 图形 \_ 最大 \_ 高度**](wia-ips-printer-endorser-graphics-max-height.md)报告的值。 WIA 微型驱动程序可以报告所有这些属性的0值，以指示接受任意大小的图像。

如果报告了非零值，则 WIA 应用程序客户端不应尝试，并且在上传小于其最小值或大于 WIA 微型驱动程序通过这些属性报告的最大大小的图像时，不会成功。 当图像大小与受支持的范围不匹配时，WIA 微型驱动程序必须失败图像上传请求。

此属性是必需的，并且对) [**WIA \_ IPS \_ PRINTER \_ Endorser \_ 图形**](wia-ips-printer-endorser-graphics.md)报告非零 (值的所有 Imprinter/Endorser 项有效。 否则，这些属性无效。

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

 

 





