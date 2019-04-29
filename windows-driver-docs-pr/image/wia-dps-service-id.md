---
title: WIA\_DPS\_SERVICE\_ID
description: WIA\_DPS\_服务\_ID 属性包含 web 服务扫描程序设备的服务 ID。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: ec77c2a6-0b9e-4c43-b189-7714257f3807
keywords:
- WIA_DPS_SERVICE_ID 成像设备
topic_type:
- apiref
api_name:
- WIA_DPS_SERVICE_ID
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f695e31a9a1b937d7c5e09e675548a4c8fbb273
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366987"
---
# <a name="wiadpsserviceid"></a>WIA\_DPS\_SERVICE\_ID


WIA\_DPS\_服务\_ID 属性包含 web 服务扫描程序设备的服务 ID。 WIA 微型驱动程序创建并维护此属性。

属性类型：VT\_BSTR

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

WIA 微型驱动程序将此属性在运行时初始化通过阅读主键\_PNPX\_函数实例对象中的 ServiceId 设备属性。

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


[**WIA\_DPS\_DEVICE\_ID**](wia-dps-device-id.md)

[**WIA\_DPS\_GLOBAL\_标识**](wia-dps-global-identity.md)

 

 






