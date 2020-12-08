---
title: WIA \_ DPS \_ 全局 \_ 标识
description: WIA \_ DPS \_ 全局 \_ 标识属性包含 web 服务扫描程序设备的 SOAP 地址。 WIA 微型驱动程序创建并维护此属性。
keywords:
- WIA_DPS_GLOBAL_IDENTITY 图像设备
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
ms.openlocfilehash: f4557594627a539b17c73dbec7286d3d535fcaa2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836987"
---
# <a name="wia_dps_global_identity"></a>WIA \_ DPS \_ 全局 \_ 标识


WIA \_ DPS \_ 全局 \_ 标识属性包含 web 服务扫描程序设备的 SOAP 地址。 WIA 微型驱动程序创建并维护此属性。

属性类型： VT \_ BSTR

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

WIA 微型驱动程序通过 \_ \_ 从函数实例对象读取 PKEY PNPX GlobalIdentity 设备属性，在运行时初始化此属性。

PKEY \_ PNPX \_ GLOBALIDENTITY 和 PKEY \_ PNPX Id 都 \_ 包含 UPNP 设备的唯一 ID。 不同之处在于，PKEY \_ PNPX \_ GlobalIdentity 始终包含所有函数实例的根设备的 uuid，而 PKEY \_ PNPX \_ ID 包含函数实例表示的设备/子设备的 uuid。

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


[**WIA \_ DPS \_ 设备 \_ ID**](wia-dps-device-id.md)

[**WIA \_ DPS \_ 服务 \_ ID**](wia-dps-service-id.md)

 

 






