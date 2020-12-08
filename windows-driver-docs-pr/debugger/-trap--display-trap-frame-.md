---
title: .trap（显示陷阱帧）
description: Trap 命令显示陷阱帧寄存器状态，并还设置注册上下文。
keywords:
- 显示 ( 陷阱帧) 命令
- 捕获帧
- 陷井 (显示捕获帧) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .trap (Display Trap Frame)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 54bffa07cdcdc5735fd8199dcf062dc3d5d3904d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799829"
---
# <a name="trap-display-trap-frame"></a>.trap（显示陷阱帧）


**Trap** 命令显示陷阱帧寄存器状态，并还设置注册上下文。

```dbgcmd
.trap [Address]
```

## <a name="span-idddk_meta_display_trap_frame_dbgspanspan-idddk_meta_display_trap_frame_dbgspanparameters"></a><span id="ddk_meta_display_trap_frame_dbg"></span><span id="DDK_META_DISPLAY_TRAP_FRAME_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
目标系统上的陷阱帧的十六进制地址。 省略地址不会显示任何陷阱帧信息，但会重置注册上下文。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>仅限内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关注册上下文和其他上下文设置的详细信息，请参阅 [更改上下文](changing-contexts.md)。

<a name="remarks"></a>备注
-------

**Trap** 命令显示指定捕获帧的重要寄存器。

此命令还指示内核调试器使用指定的上下文记录作为寄存器上下文。 执行此命令后，调试器将有权访问此线程的最重要寄存器和堆栈跟踪。 此注册上下文会一直保留，直到你允许目标执行或使用另一个寄存器上下文 [**.thread**](-thread--set-register-context-.md)命令 (。 [**.cxr**](-cxr--display-context-record-.md)**或) 。** 有关完整详细信息，请参阅 [注册上下文](changing-contexts.md#register-context) 。

调试 bug 检查0xA 和0x7F 时，通常使用此扩展。 有关详细信息和示例，请参阅 [**Bug 检查 0xA**](bug-check-0xa--irql-not-less-or-equal.md) (IRQL \_ 不 \_ 小于 \_ 或 \_ 等于) 。

 

 





