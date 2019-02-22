---
title: WIA\_DPS\_GLOBAL\_标识
description: WIA\_DPS\_GLOBAL\_标识属性包含 web 服务扫描程序设备的 SOAP 地址。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: 4ee25eb9-eb5b-43b2-8b35-7bc8ac45c90a
keywords:
- WIA_DPS_GLOBAL_IDENTITY 成像设备
topic_type:
- apiref
api_name:
- WIA_DPS_GLOBAL_IDENTITY
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f32d8d372575835b8084f3ff61d6993538e952d9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554538"
---
# <a name="wiadpsglobalidentity"></a>WIA\_DPS\_GLOBAL\_标识


WIA\_DPS\_GLOBAL\_标识属性包含 web 服务扫描程序设备的 SOAP 地址。 WIA 微型驱动程序创建并维护此属性。

属性类型：VT\_BSTR

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

WIA 微型驱动程序将此属性在运行时初始化通过阅读主键\_PNPX\_GlobalIdentity 设备属性从函数实例对象。

这两个主键\_PNPX\_GlobalIdentity 和主键\_PNPX\_ID 包含 UPnP 设备的唯一 ID。 不同之处是该主键\_PNPX\_GlobalIdentity 始终包含在根设备的 UUID 对于所有的函数实例，而主键\_PNPX\_ID 包含的设备/子 Device UUID 的函数实例表示。

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

## <a name="see-also"></a>另请参阅


[**WIA\_DPS\_DEVICE\_ID**](wia-dps-device-id.md)

[**WIA\_DPS\_SERVICE\_ID**](wia-dps-service-id.md)

 

 






