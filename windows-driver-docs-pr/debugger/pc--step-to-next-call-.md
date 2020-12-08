---
title: pc（步进到下一个调用）
description: 在达到调用说明之前，pc 命令会执行程序。
keywords:
- pc (下一步调用) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pc (Step to Next Call)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: da81b26964d9037c0ec37090d32401351584664e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808483"
---
# <a name="pc-step-to-next-call"></a>pc（步进到下一个调用）


在达到调用说明之前， **pc** 命令会执行程序。

User-Mode

```dbgcmd
[~Thread] pc [r] [= StartAddress] [Count] 
```

Kernel-Mode

```dbgcmd
pc [r] [= StartAddress] [Count] 
```

## <a name="span-idddk_cmd_step_to_next_call_dbgspanspan-idddk_cmd_step_to_next_call_dbgspanparameters"></a><span id="ddk_cmd_step_to_next_call_dbg"></span><span id="DDK_CMD_STEP_TO_NEXT_CALL_DBG"></span>参数


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span>*Thread*   
指定要继续执行的线程。 所有其他线程均已冻结。 有关语法的详细信息，请参阅 [线程语法](thread-syntax.md)。 只能在用户模式下指定线程。

<span id="_______r______"></span><span id="_______R______"></span>**r**   
打开和关闭寄存器和标志的显示。 默认情况下，将显示寄存器和标志。 您可以通过使用 **pcr**、 [**pr**](p--step-.md)、 [**tr**](t--trace-.md)或提示禁止注册显示 \_ 。 所有这些命令都控制相同的设置，你可以使用其中任何一个命令来替代以前使用的这些命令。

你还可以使用 l os 命令禁用注册显示。 此设置与其他三个命令不同。 若要控制显示哪些寄存器和标志，请使用 [**rm (注册掩码)**](rm--register-mask-.md) 命令。

<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span>*StartAddress*   
指定调试器开始执行的地址。 否则，调试器会从指令指针指向的指令开始。 有关语法的详细信息，请参阅 [address 和 Address Range 语法](address-and-address-range-syntax.md)。

<span id="_______Count______"></span><span id="_______count______"></span><span id="_______COUNT______"></span>*计数*   
指定调试器在此命令停止时必须遇到的 **调用** 指令的数目。 默认值为一。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅限实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关相关命令的详细信息，请参阅 [控制目标](controlling-the-target.md)。

<a name="remarks"></a>备注
-------

**Pc** 命令导致目标开始执行。 此执行将继续，直到达到 **调用** 指令或遇到断点。

如果程序计数器已在 **调用** 指令上，则执行整个调用。 在此调用返回后，将继续执行，直到达到其他 **调用** 。 这种执行（而不是跟踪）调用是 **pc** 与 [**tc (Trace 之间唯一不同于下一个调用)**](tc--trace-to-next-call-.md)。

在源模式下，可以将一个源行与多个程序集指令相关联。 **Pc** 命令不会在与当前源行关联的 **调用** 指令处停止。

 

 





