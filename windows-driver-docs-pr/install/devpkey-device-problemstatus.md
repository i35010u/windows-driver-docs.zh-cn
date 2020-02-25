---
title: DEVPKEY_Device_ProblemStatus
description: DEVPKEY_Device_ProblemStatus
ms.assetid: 477f835c-6094-4fba-80af-f6032bca7f85
keywords:
- DEVPKEY_Device_ProblemStatus 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_ProblemStatus
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 02/14/2020
ms.openlocfilehash: 914ee5cc10659ac458f0f79064612dfaf8742f05
ms.sourcegitcommit: aa7083b10b34a29a348f4950ced21a8a67a44a0f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/22/2020
ms.locfileid: "77558711"
---
# <a name="devpkey_device_problemstatus"></a>DEVPKEY_Device_ProblemStatus


DEVPKEY_Device_ProblemStatus 设备属性是在生成问题代码时设置的 NTSTATUS 值。 它提供了有关设置问题代码的原因的更多上下文。 如果没有其他上下文可用，ProblemStatus 将显示为 STATUS_SUCCESS （0x00000000）。


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_Device_ProblemStatus</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-int32.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_NTSTATUS&lt;/strong&gt;](devprop-type-ntstatus.md)"><strong>DEVPROP_TYPE_NTSTATUS</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>属性访问</strong></p></td>
<td align="left"><p>安装应用程序和安装程序的只读访问</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>是</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

当 devnode 出现问题时，"**问题状态**" 属性将显示在设备管理器中设备的 "**详细信息**" 选项卡上的 "**属性**" 下拉列表中。

有关 NTSTATUS 值的详细信息，请参阅[使用 Ntstatus 值](../kernel/using-ntstatus-values.md)。

可以调用[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)来检索 DEVPKEY_Device_ProblemStatus 的值。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>在 windows 8 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Devpkey （包括 Devpkey）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**CM_Get_DevNode_Status**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_devnode_status)

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






