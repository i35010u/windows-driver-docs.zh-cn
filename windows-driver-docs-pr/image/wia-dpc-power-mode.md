---
title: WIA \_ DPC \_ 电源 \_ 模式
description: WIA \_ DPC \_ 电源 \_ 模式属性定义了照相机设备的当前电源。
keywords:
- WIA_DPC_POWER_MODE 图像设备
topic_type:
- apiref
api_name:
- WIA_DPC_POWER_MODE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59e6b8e83081c3eae425c49359d676f41d358c94
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785169"
---
# <a name="wia_dpc_power_mode"></a>WIA \_ DPC \_ 电源 \_ 模式


WIA \_ DPC \_ 电源 \_ 模式属性定义了照相机设备的当前电源。

## <span id="ddk_wia_dpc_power_mode_si"></span><span id="DDK_WIA_DPC_POWER_MODE_SI"></span>


属性类型： VT \_ I4

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

应用程序读取 WIA \_ DPC \_ 电源 \_ 模式属性来确定相机使用的电源。

下表介绍了在 WIA \_ DPC \_ 电源模式下有效的常量 \_ 。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>值</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>POWERMODE_BATTERY</p></td>
<td><p>照相机设备正在使用电池电源运行。</p></td>
</tr>
<tr class="even">
<td><p>POWERMODE_LINE</p></td>
<td><p>照相机设备在电源适配器上运行。</p></td>
</tr>
</tbody>
</table>

 

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

 

 





