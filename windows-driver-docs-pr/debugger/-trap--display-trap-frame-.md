---
title: .trap（显示陷阱帧）
description: .Trap 命令显示陷阱框架注册状态，并还会设置寄存器上下文。
ms.assetid: c53177ad-243c-4276-8602-2edc14b44251
keywords:
- 显示陷阱帧 (.trap) 命令
- 陷阱帧
- .trap （显示陷阱帧） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .trap (Display Trap Frame)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c4d8e6a82cdbcd316ec278da383ec8a5777645f0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339783"
---
# <a name="trap-display-trap-frame"></a>.trap（显示陷阱帧）


**.Trap**命令显示陷阱框架注册状态，并还会设置寄存器上下文。

```dbgcmd
.trap [Address]
```

## <a name="span-idddkmetadisplaytrapframedbgspanspan-idddkmetadisplaytrapframedbgspanparameters"></a><span id="ddk_meta_display_trap_frame_dbg"></span><span id="DDK_META_DISPLAY_TRAP_FRAME_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
在目标系统上的陷阱帧十六进制地址。 省略地址不显示任何陷阱帧信息，但它重置原理寄存器上下文。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>内核模式下</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关寄存器上下文和其他上下文设置的详细信息，请参阅[更改上下文](changing-contexts.md)。

<a name="remarks"></a>备注
-------

**.Trap**命令显示指定的陷阱帧的重要寄存器。

此命令也指示了内核调试程序，使用指定的上下文记录作为寄存器上下文。 执行此命令后，调试器将具有访问此线程的最重要的寄存器和堆栈跟踪。 允许目标以执行或使用另一个寄存器上下文命令之前将一直保留此寄存器上下文 ([**.thread**](-thread--set-register-context-.md)， [ **.cxr** ](-cxr--display-context-record-.md)，或 **.trap**)。 请参阅[注册上下文](changing-contexts.md#register-context)有关完整详细信息。

调试 0xA 和 0x7F 的 bug 检查时，通常使用此扩展。 有关详细信息和示例，请参阅[ **Bug 检查 0xA** ](bug-check-0xa--irql-not-less-or-equal.md) (IRQL\_不\_较少\_或\_相等)。

 

 





