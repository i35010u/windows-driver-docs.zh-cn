---
title: WIA \_ DPC \_ 曝光 \_ 时间
description: "\"WIA \\_ DPC \\_ 曝光 \\_ 时间\" 属性对应于10000缩放的快门速度，以秒为单位。"
keywords:
- WIA_DPC_EXPOSURE_TIME 图像设备
topic_type:
- apiref
api_name:
- WIA_DPC_EXPOSURE_TIME
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a7d5b336a2ef75f7a245351ce11712cf8492cf4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830457"
---
# <a name="wia_dpc_exposure_time"></a>WIA \_ DPC \_ 曝光 \_ 时间


"WIA \_ DPC \_ 曝光 \_ 时间" 属性对应于10000缩放的快门速度，以秒为单位。

## <span id="ddk_wia_dpc_exposure_time_si"></span><span id="DDK_WIA_DPC_EXPOSURE_TIME_SI"></span>


属性类型： VT \_ I4

有效值： WIA "内容范围" 或 "WIA 内容" \_ \_ \_ \_ 列表

访问权限：读/写

<a name="remarks"></a>备注
-------

通常， \_ \_ \_ 仅当 [**WIA \_ dpc \_ 曝露 \_ 模式**](wia-dpc-exposure-mode.md) 属性设置为 "EXPOSUREMODE \_ 手动" 或 "EXPOSUREMODE \_ 快门优先级" 时 \_ ，设备才使用 "wia dpc 曝光时间" 属性。

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

## <a name="see-also"></a>请参阅


[**WIA \_ DPC \_ 曝光 \_ 模式**](wia-dpc-exposure-mode.md)

 

 






