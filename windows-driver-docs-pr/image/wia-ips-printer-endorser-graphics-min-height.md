---
title: WIA\_IPS\_打印机\_印记签署器\_图形\_MIN\_高度
description: WIA\_IPS\_打印机\_印记签署器\_图形\_MIN\_高度属性以及 WIA\_IP\_打印机\_印记签署器\_图形\_最大\_高度，WIA\_IPS\_打印机\_印记签署器\_图形\_MIN\_宽度和 WIA\_IP\_打印机\_印记签署器\_图形\_最大\_用于报告的最小值和最大的维度，以像素为单位，可以上传到印刷器/印记签署器要呈现的图像的宽度。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: 377BEDCB-907E-4311-B0D6-CE06C3C14583
keywords:
- WIA_IPS_PRINTER_ENDORSER_GRAPHICS_MIN_HEIGHT 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_GRAPHICS_MIN_HEIGHT
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: c532922db525009f52f0059a20c0cdc490087018
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526740"
---
# <a name="wiaipsprinterendorsergraphicsminheight"></a>WIA\_IPS\_打印机\_印记签署器\_图形\_MIN\_高度


**WIA\_IPS\_打印机\_印记签署器\_图形\_MIN\_高度**属性连同[ **WIA\_IPS\_打印机\_印记签署器\_图形\_MAX\_高度**](wia-ips-printer-endorser-graphics-max-height.md)， [ **WIA\_IP\_打印机\_印记签署器\_图形\_MIN\_宽度**](wia-ips-printer-endorser-graphics-min-width.md)，并[ **WIA\_IP\_打印机\_印记签署器\_图形\_最大\_宽度**](wia-ips-printer-endorser-graphics-max-width.md)用于报告的最小值和最大的维度，以像素为单位，可以上传到印刷器的图像 /印记签署器呈现。 WIA 微型驱动程序创建并维护此属性。




属性类型：VT\_UI4

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

报告的值**WIA\_IPS\_打印机\_印记签署器\_图形\_MIN\_高度**必须小于或等于为报告的值[**WIA\_IPS\_打印机\_印记签署器\_图形\_最大值\_高度**](wia-ips-printer-endorser-graphics-max-height.md)。 报告的值[**WIA\_IPS\_打印机\_印记签署器\_图形\_MIN\_宽度**](wia-ips-printer-endorser-graphics-min-width.md)必须小于或报告的值相等[ **WIA\_IPS\_打印机\_印记签署器\_图形\_最大\_宽度**](wia-ips-printer-endorser-graphics-max-width.md). WIA 微型驱动程序可以报告所有这些属性以指示接受任意大小的图像的值为 0。

如果报告了非零值，WIA 应用程序客户端不应尝试，并且必须不需要成功上传的图像的最小值小于或大于这些属性通过 WIA 微型驱动程序报告的最大大小。 图像大小不匹配支持的范围时，WIA 微型驱动程序必须故障映像上传请求。

此属性是必需的和有效的所有印刷器/印记签署器项的报告非零值 (True)，以便[ **WIA\_IPS\_打印机\_印记签署器\_图形**](wia-ips-printer-endorser-graphics.md). 否则，这些属性均无效。

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

 

 





