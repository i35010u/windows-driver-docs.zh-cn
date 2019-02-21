---
title: WIA\_DPS\_MAX\_SCAN\_TIME
description: WIA\_DPS\_最大\_扫描\_时间属性包含要扫描的当前属性设置，以毫秒为单位的单个页面的最长时间。
ms.assetid: 28c24b1b-9318-46d2-86eb-f948247de8ab
keywords:
- WIA_DPS_MAX_SCAN_TIME 成像设备
topic_type:
- apiref
api_name:
- WIA_DPS_MAX_SCAN_TIME
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8dcd940aa7b479399ff08b6d50366cdcbf8a514
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526113"
---
# <a name="wiadpsmaxscantime"></a>WIA\_DPS\_MAX\_SCAN\_TIME


WIA\_DPS\_最大\_扫描\_时间属性包含要扫描的当前属性设置，以毫秒为单位的单个页面的最长时间。

## <span id="ddk_wia_dps_max_scan_time_si"></span><span id="DDK_WIA_DPS_MAX_SCAN_TIME_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

应用程序读取 WIA\_DPS\_最大\_扫描\_要多少估计所需扫描的页面的时间的时间属性。 如果您确定已停止响应的设备的条件，此估计值非常有用。 WIA 微型驱动程序创建并维护此属性。

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

 

 





