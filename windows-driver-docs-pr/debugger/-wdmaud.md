---
title: wdmaud
description: 将显示多种 WDM 音频 (WDMAud) 结构。
ms.assetid: fa41e3e2-a767-4c8c-9604-e3ea924ac571
keywords:
- wdmaud Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdmaud
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: aca91133acf2c075587b69fe8666b0d68be915c5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576776"
---
# <a name="wdmaud"></a>!wdmaud


将显示多种 WDM 音频 (WDMAud) 结构。

```dbgcmd
!wdmaud Address Flags
```

## <a name="span-idddkwdmauddbgspanspan-idddkwdmauddbgspanparameters"></a><span id="ddk__wdmaud_dbg"></span><span id="DDK__WDMAUD_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定要显示的结构的地址。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
指定要显示的信息。 这必须包括位 0x1、 0x2、 0x4 和 0x8 之一。 0x100 位可以添加到其中的任何。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)  
显示所有已发送到 wdmaud.sys 的 Ioctl 的列表。 这使用时，*地址*应指定的地址**WdmaIoctlHistoryListHead**。 如果设置 0x100 位，则显示内容还包括**pContext**每个 IOCTL 已发送。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)  
显示为挂起 WDMAud 已标记的所有 Irp 的列表。 这使用时，*地址*应指定的地址**WdmaPendingIrpListHead**。 如果设置 0x100 位，则显示内容还包括分配每个 IRP 的上下文。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)  
显示所有 MDLs WDMAud 已分配的列表。 这使用时，*地址*应指定的地址**WdmaAllocatedMdlListHead**。 如果设置 0x100 位，则显示还包括已分配每个 MDL 的上下文。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>位 3 (0x8)  
显示所有活动的上下文附加到 wdmaud.sys 的列表。 这使用时，*地址*应指定的地址**WdmaContextListHead**。 如果设置 0x100 位，则显示内容还包括数据结构的成员的每个上下文。

<span id="Bit_8__0x100_"></span><span id="bit_8__0x100_"></span><span id="BIT_8__0X100_"></span>位 8 (0x100)  
将导致显示以包括详细的信息。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

WDM 音频体系结构和音频驱动程序有关的信息，请参阅 Windows Driver Kit (WDK) 文档。

<a name="remarks"></a>备注
-------

上下文附加到 wdmaud.sys (**pContext**) 包含大部分的每个设备的状态数据。 每当 wdmaud.drv 加载到新进程，wdmaud.sys 通知到达。 每当 wdmaud.drv 被卸载，wdmaud.sys 清理在该上下文中执行任何分配。

 

 





