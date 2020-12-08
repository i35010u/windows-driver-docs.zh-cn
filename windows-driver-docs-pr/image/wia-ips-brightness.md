---
title: WIA \_ IPS \_ 亮度
description: WIA \_ IPS \_ 亮度属性包含设备的当前硬件亮度设置。
keywords:
- WIA_IPS_BRIGHTNESS 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_BRIGHTNESS
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: be70a8e8a2a0672d87c432a685efd474826f111b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826843"
---
# <a name="wia_ips_brightness"></a>WIA \_ IPS \_ 亮度


WIA \_ IPS \_ 亮度属性包含设备的当前硬件亮度设置。

## <span id="ddk_wia_ips_brightness_si"></span><span id="DDK_WIA_IPS_BRIGHTNESS_SI"></span>


属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 范围

访问权限：读/写

<a name="remarks"></a>备注
-------

应用程序将 WIA \_ IPS \_ 亮度属性设置为硬件的亮度值。 WIA 微型驱动程序创建并维护此属性。

WIA \_ IPS 亮度的值 \_ 应映射到从−1000到1000的范围，其中1000对应于最大亮度，0对应于一般亮度，−1000对应于最小亮度。

\_ \_ 所有图像获取项都需要 WIA IPS 亮度。

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

 

 





