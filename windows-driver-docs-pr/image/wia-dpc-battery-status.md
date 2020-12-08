---
title: WIA \_ DPC \_ 电池 \_ 状态
description: WIA \_ DPC \_ 电池 \_ 状态属性定义了用于操作照相机设备的电池电量的百分比。
keywords:
- WIA_DPC_BATTERY_STATUS 图像设备
topic_type:
- apiref
api_name:
- WIA_DPC_BATTERY_STATUS
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d47bcedba3e3674262e9768f52b6bd95d364e6dc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824477"
---
# <a name="wia_dpc_battery_status"></a>WIA \_ DPC \_ 电池 \_ 状态


WIA \_ DPC \_ 电池 \_ 状态属性定义了用于操作照相机设备的电池电量的百分比。

## <span id="ddk_wia_dpc_battery_status_si"></span><span id="DDK_WIA_DPC_BATTERY_STATUS_SI"></span>


属性类型： VT \_ I4

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

WIA \_ DPC \_ 电池状态属性的值 \_ 应为0到100之间的整数。 应用程序读取此属性以确定相机设备的剩余电池寿命。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>在 Windows Vista 和更高版本的操作系统中已过时，不应再使用。 但是，在 Windows Vista 中仍定义此属性，以与为 Windows Server 2003、Windows XP 和 windows 的早期版本设计的应用程序和设备兼容。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

 

 





