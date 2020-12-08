---
title: WIA \_ IP \_ 阈值
description: WIA \_ ip \_ 阈值属性包含设备的当前硬件阈值设置。 WIA 微型驱动程序创建并维护此属性。
keywords:
- WIA_IPS_THRESHOLD 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_THRESHOLD
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f344e5dca1b97a989c7f00ca70880c800ed0f58
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814409"
---
# <a name="wia_ips_threshold"></a>WIA \_ IP \_ 阈值


WIA \_ ip \_ 阈值属性包含设备的当前硬件阈值设置。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_ips_threshold_si"></span><span id="DDK_WIA_IPS_THRESHOLD_SI"></span>


属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 范围

访问权限：读/写

<a name="remarks"></a>备注
-------

应 \_ \_ 在0到255范围内映射 "WIA ip 阈值" 属性的值。 默认值为128。

应用程序设置 WIA \_ ip \_ 阈值以更改硬件阈值。 仅当 [**wia \_ IPA \_ DATATYPE**](wia-ipa-datatype.md) 属性等于 wia 数据阈值时，此值才 \_ 有效 \_ 。 如果设备不允许 \_ 更改 WIA 数据 \_ 阈值，则它应报告默认值128。

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

## <a name="see-also"></a>请参阅


[**WIA \_ IPA \_ 数据类型**](wia-ipa-datatype.md)

 

 






