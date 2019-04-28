---
title: WIA\_IP\_阈值
description: WIA\_IP\_阈值属性包含设备的当前硬件阈值设置。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: 1d315168-5434-4e99-9e54-cb6e279df3e7
keywords:
- WIA_IPS_THRESHOLD 成像设备
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
ms.openlocfilehash: 1f2575b6e5a51d65ad08d2e50e77b04d6fa7a70e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343833"
---
# <a name="wiaipsthreshold"></a>WIA\_IP\_阈值


WIA\_IP\_阈值属性包含设备的当前硬件阈值设置。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_ips_threshold_si"></span><span id="DDK_WIA_IPS_THRESHOLD_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_RANGE

访问权限：读取/写入

<a name="remarks"></a>备注
-------

应将值映射为 WIA\_IP\_阈值属性从 0 到 255 范围内的。 默认值为 128。

应用程序设置 WIA\_IP\_阈值，若要更改硬件阈值的值。 此值才有效才[ **WIA\_IPA\_数据类型**](wia-ipa-datatype.md)属性等于 WIA\_数据\_阈值。 如果设备不支持 WIA\_数据\_阈值来进行更改，它应该报告默认值为 128。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA\_IPA\_DATATYPE**](wia-ipa-datatype.md)

 

 






