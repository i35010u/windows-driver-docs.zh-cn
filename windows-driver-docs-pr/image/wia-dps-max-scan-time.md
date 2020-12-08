---
title: WIA \_ DPS \_ 最长 \_ 扫描 \_ 时间
description: WIA \_ DPS \_ MAX \_ SCAN \_ TIME 属性包含使用当前属性设置扫描单个页面的最大时间（以毫秒为单位）。
keywords:
- WIA_DPS_MAX_SCAN_TIME 图像设备
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
ms.openlocfilehash: 2ed5c30ac7153e4c1da18f941e27eeebb206f70e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802401"
---
# <a name="wia_dps_max_scan_time"></a>WIA \_ DPS \_ 最长 \_ 扫描 \_ 时间


WIA \_ DPS \_ MAX \_ SCAN \_ TIME 属性包含使用当前属性设置扫描单个页面的最大时间（以毫秒为单位）。

## <span id="ddk_wia_dps_max_scan_time_si"></span><span id="DDK_WIA_DPS_MAX_SCAN_TIME_SI"></span>


属性类型： VT \_ I4

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

应用程序将读取 "WIA \_ DPS \_ 最大 \_ 扫描时间" \_ 属性，以估计扫描页面所需的时间。 在确定已停止响应的设备的条件时，此估算非常有用。 WIA 微型驱动程序创建并维护此属性。

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

 

 





