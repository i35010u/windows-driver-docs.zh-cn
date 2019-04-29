---
title: WIA\_DPA\_DEVICE\_TIME
description: WIA\_DPA\_设备\_时间属性包含当前存储在设备的时钟时间。 微型驱动程序创建并维护此属性。
ms.assetid: 5f903eb8-6a9e-4f06-ba70-5c02d8b332e5
keywords:
- WIA_DPA_DEVICE_TIME 成像设备
topic_type:
- apiref
api_name:
- WIA_DPA_DEVICE_TIME
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba4df830b50bebf7b832799734dcff4c7fed6424
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391111"
---
# <a name="wiadpadevicetime"></a>WIA\_DPA\_DEVICE\_TIME


WIA\_DPA\_设备\_时间属性包含当前存储在设备的时钟时间。 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_dpa_device_time_si"></span><span id="DDK_WIA_DPA_DEVICE_TIME_SI"></span>


属性类型：VT\_UI2 | VT\_VECTOR

有效值：WIA\_PROP\_NONE

访问权限：读/写或只读的

<a name="remarks"></a>备注
-------

当 WIA\_DPA\_设备\_时间属性为只读时，微型驱动程序应检查设备的当前时钟时间，并应始终返回当前时间。 此属性仅受具有内部时钟的设备。 如果可以设置设备时钟，此属性为读/写;否则，它是只读的。 WIA 的设备将报告 SYSTEMTIME 结构 （它 Microsoft Windows SDK 文档中所述） 中的时间。

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

 

 





