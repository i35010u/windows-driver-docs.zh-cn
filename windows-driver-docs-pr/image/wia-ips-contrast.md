---
title: WIA \_ IP \_ 对比
description: "\"WIA \\_ ip \\_ 对比度\" 属性包含设备的当前硬件对比度设置。"
keywords:
- WIA_IPS_CONTRAST 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_CONTRAST
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba7b27a6011f12a4b8966830afdfd3590d3c2a77
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796159"
---
# <a name="wia_ips_contrast"></a>WIA \_ IP \_ 对比


"WIA \_ ip \_ 对比度" 属性包含设备的当前硬件对比度设置。

## <span id="ddk_wia_ips_contrast_si"></span><span id="DDK_WIA_IPS_CONTRAST_SI"></span>


属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 范围

访问权限：读/写

<a name="remarks"></a>备注
-------

应用程序将 WIA \_ IPS \_ 对比度属性设置为硬件的对比度值。 WIA 微型驱动程序创建并维护此属性。

WIA \_ IPS 对比度的值 \_ 应映射到从−1000到1000的范围内，其中−1000对应于最小对比度，0对应于正常对比度，1000对应于最大对比度。

\_ \_ 所有映像获取项都需要 WIA IPS 对比度。

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

 

 





