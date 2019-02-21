---
title: WIA\_IPS\_热\_向上\_时间
description: WIA\_IPS\_热\_向上\_时间属性包含的最大的预热时间，以毫秒为单位，设备需要在开始扫描操作之前。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: 081cdb91-d5d8-4458-9a78-72fcbb13c7da
keywords:
- WIA_IPS_WARM_UP_TIME 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_WARM_UP_TIME
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31c328a98905f5769e9881efa64da011d92088ae
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526758"
---
# <a name="wiaipswarmuptime"></a>WIA\_IPS\_热\_向上\_时间


WIA\_IPS\_热\_向上\_时间属性包含的最大的预热时间，以毫秒为单位，设备需要在开始扫描操作之前。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_ips_warm_up_time_si"></span><span id="DDK_WIA_IPS_WARM_UP_TIME_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

应用程序可以读取 WIA\_IPS\_热\_向上\_时间属性来确定设备的最大的预热时间。 然后，应用程序可以显示"正在等待设备预热"对话框中，让用户了解发生任何之前可能出现等待或暂停。

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

 

 





