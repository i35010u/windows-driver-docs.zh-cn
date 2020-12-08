---
title: wdmaud
description: 显示各种 WDM 音频 (WDMAud) 结构。
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
ms.openlocfilehash: 4a3e2798e97833479f65a1850cc47d7120ac50cb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823587"
---
# <a name="wdmaud"></a>!wdmaud


显示各种 WDM 音频 (WDMAud) 结构。

```dbgcmd
!wdmaud Address Flags
```

## <a name="span-idddk__wdmaud_dbgspanspan-idddk__wdmaud_dbgspanparameters"></a><span id="ddk__wdmaud_dbg"></span><span id="DDK__WDMAUD_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定要显示的结构的地址。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
指定要显示的信息。 这必须只包含其中一个位0x1、0x2、0x4 和0x8。 可以将0x100 位添加到其中任何一个。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)   
显示已发送到 wdmaud.sys 的所有 IOCTLs 的列表。 使用此时， *Address* 应指定 **WdmaIoctlHistoryListHead** 的地址。 如果设置了0x100 位，则显示内容还包括每个 IOCTL 发送时所用的 **pContext** 。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)   
显示 WDMAud 标记为 "挂起" 的所有 Irp 的列表。 使用此时， *Address* 应指定 **WdmaPendingIrpListHead** 的地址。 如果设置了0x100 位，则显示还会包括分配了每个 IRP 的上下文。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)   
显示 WDMAud 分配的所有 MDLs 的列表。 使用此时， *Address* 应指定 **WdmaAllocatedMdlListHead** 的地址。 如果设置了0x100 位，则显示内容还包含分配了每个 MDL 的上下文。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>第 3 (0x8)   
显示附加到 wdmaud.sys 的所有活动上下文的列表。 使用此时， *Address* 应指定 **WdmaContextListHead** 的地址。 如果设置了0x100 位，则显示也包括每个上下文结构的数据成员。

<span id="Bit_8__0x100_"></span><span id="bit_8__0x100_"></span><span id="BIT_8__0X100_"></span>位 8 (0x100)   
使显示内容包含详细信息。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关 WDM 音频体系结构和音频驱动程序的信息，请参阅 Windows 驱动程序工具包 (WDK) 文档。

<a name="remarks"></a>备注
-------

附加到 wdmaud.sys (**pContext**) 的上下文包含每个设备的大多数状态数据。 每当 winspool.drv 加载到新进程时，wdmaud.sys 就会收到通知。 在卸载 wdmaud 时，wdmaud.sys 会清理在该上下文中进行的任何分配。

 

 





