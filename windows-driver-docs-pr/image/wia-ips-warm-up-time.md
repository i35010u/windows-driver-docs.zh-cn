---
title: WIA \_ IP \_ 预热 \_ \_ 时间
description: "\"WIA \\_ ip \\_ 预热 \\_ \\_ 时间\" 属性包含设备在开始扫描操作之前需要的最大预热时间（以毫秒为单位）。 WIA 微型驱动程序创建并维护此属性。"
keywords:
- WIA_IPS_WARM_UP_TIME 图像设备
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
ms.openlocfilehash: b9664cd735eaa2e0f2b8bc199f99a90db0ff65fb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795509"
---
# <a name="wia_ips_warm_up_time"></a>WIA \_ IP \_ 预热 \_ \_ 时间


"WIA \_ ip \_ 预热 \_ \_ 时间" 属性包含设备在开始扫描操作之前需要的最大预热时间（以毫秒为单位）。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_ips_warm_up_time_si"></span><span id="DDK_WIA_IPS_WARM_UP_TIME_SI"></span>


属性类型： VT \_ I4

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

应用程序可以读取 "WIA \_ ip \_ 预热 \_ \_ 时间" 属性来确定设备的最大预热时间。 然后，应用程序可以显示 "等待设备预热" 对话框，以让用户知道在出现任何情况之前，可能会发生等待或暂停。

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

 

 





