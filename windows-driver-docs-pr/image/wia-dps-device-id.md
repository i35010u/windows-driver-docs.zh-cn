---
title: WIA\_DPS\_DEVICE\_ID
description: WIA\_DPS\_设备\_ID 属性包含唯一的函数实例标识符，对 web 服务扫描程序设备。
ms.assetid: 48c45b94-86b1-41b5-89bc-e3270ad56d7e
keywords:
- WIA_DPS_DEVICE_ID 成像设备
topic_type:
- apiref
api_name:
- WIA_DPS_DEVICE_ID
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6dd5c51d593d8fcf3604b9d1fdfe2c3cf5c96778
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382275"
---
# <a name="wiadpsdeviceid"></a>WIA\_DPS\_DEVICE\_ID


WIA\_DPS\_设备\_ID 属性包含唯一的函数实例标识符，对 web 服务扫描程序设备。 此标识符表示与通信 WIA 微型驱动程序在扫描程序设备上的 web 服务。 应不进行任何假设此标识符的形式。 WIA 微型驱动程序创建并维护此属性。

WIA 应用程序可以使用的值 WIA\_DPS\_设备\_ID 以查找，请使用函数发现 API，该函数实例对象，表示当前 WIA 会话中使用的 web 服务扫描程序设备。

属性类型：VT\_BSTR

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

WIA 微型驱动程序将此属性在运行时初始化通过阅读主键\_PNPX\_从函数实例对象的 ID 设备属性。

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


[**WIA\_DPS\_GLOBAL\_标识**](wia-dps-global-identity.md)

[**WIA\_DPS\_SERVICE\_ID**](wia-dps-service-id.md)

 

 






