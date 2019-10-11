---
title: sx、sxd、sxe、sxi、sxn、sxr、sx-（设置异常）
description: Sx * 命令控制调试器在要调试的应用程序中发生异常或发生某些事件时所执行的操作。
ms.assetid: fdb5059f-e7d9-4e14-aa3d-030e72c30732
keywords:
- sx、sxd、sxe、sxi、sxn、sxr、sx （设置异常） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- sx, sxd, sxe, sxi, sxn, sxr, sx- (Set Exceptions)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 844e14723f50a08759297f62d40ab5d283458634
ms.sourcegitcommit: 4bc550183bc403aee37e7aef2c38fecda1815bff
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/08/2019
ms.locfileid: "72038065"
---
# <a name="sx-sxd-sxe-sxi-sxn-sxr-sx--set-exceptions"></a>sx、sxd、sxe、sxi、sxn、sxr、sx-（设置异常）

**Sx**命令控制调试器在要调试的应用程序中发生异常或发生某些事件时所执行的操作。

```dbgcmd
sx

sx{e|d|i|n} [-c "Cmd1"] [-c2 "Cmd2"] [-h] {Exception|Event|*}

sx- [-c "Cmd1"] [-c2 "Cmd2"] {Exception|Event|*}

sxr
```

## <a name="span-idddk_cmd_set_exceptions_dbgspanspan-idddk_cmd_set_exceptions_dbgspanparameters"></a><span id="ddk_cmd_set_exceptions_dbg"></span><span id="DDK_CMD_SET_EXCEPTIONS_DBG"></span>Parameters

<span id="-c__Cmd1_"></span><span id="-c__cmd1_"></span><span id="-C__CMD1_"></span> **-c "** <em>Cmd1</em> **"**  
指定在发生异常或事件时执行的命令。 当处理此异常的第一次机会发生时，无论此异常是否中断调试器，都将执行此命令。 必须将*Cmd1*字符串用引号引起来。 此字符串可以包含用分号分隔的多个命令。 -C 和带引号的命令字符串之间的空格是可选的。

<span id="-c2_Cmd2_"></span><span id="-c2_cmd2_"></span><span id="-C2_CMD2_"></span> **-c2 "** <em>Cmd2</em> **"**  
指定在发生异常或事件并且在第一次机会未处理时执行的命令。 当第二次处理此异常时，会执行此命令，无论此异常是否中断调试器。 必须将*Cmd2*字符串用引号引起来。 此字符串可以包含用分号分隔的多个命令。 -C2 和带引号的命令字符串之间的空格是可选的。

<span id="_______-h______"></span><span id="_______-H______"></span> **-h**更改指定事件的处理状态，而不是其中断状态。 如果*事件*为**cc**、 **hc**、 **bpec**或**ssec**，则无需使用 **-h**选项。

<span id="_______Exception______"></span><span id="_______exception______"></span><span id="_______EXCEPTION______"></span>*异常*指定命令在当前基数中的作用。

<span id="_______Event______"></span><span id="_______event______"></span><span id="_______EVENT______"></span>*事件*指定命令操作的事件。 这些事件由缩写标识。 有关事件的列表，请参阅[控制异常和事件](controlling-exceptions-and-events.md)。

<span id="______________"></span> **\*** 影响不以其他方式为**sx**显式命名的所有异常。 有关显式命名异常的列表，请参阅[控制异常和事件](controlling-exceptions-and-events.md)。

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
<td align="left"><p><strong>适用</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关中断状态和处理状态的详细信息、所有事件代码的说明、所有事件的默认状态的列表以及控制此状态的其他方法的详细信息，请参阅[控制异常和事件](controlling-exceptions-and-events.md)。

<a name="remarks"></a>备注
-------

**Sx**命令显示当前进程的异常列表以及所有 nonexception 事件的列表，并显示每个异常和事件的调试器的默认行为。

**Sxe**、 **sxd**、 **sxn**和**sxi**命令控制每个异常和事件的调试器设置。

**Sxr**命令将所有异常和事件筛选器状态重置为默认设置。 命令已清除，中断和继续选项重置为其默认设置，依此类推。

**Sx**命令不会更改指定异常或事件的处理状态或中断状态。 如果要更改与特定事件相关联的第一条命令或第二次执行命令，但不希望更改其他任何内容，则可以使用此命令。

如果包括 **-h**选项（或者，如果指定了**cc**、 **hc**、 **bpec**或**ssec**事件）， **sxe**、 **sxd**、 **sxn**和**sxi**命令将控制异常的[处理状态](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-filter-xxx#handling-status)或事件。 在所有其他情况下，这些命令控制异常或事件的[中断状态](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-filter-xxx#break-status)。

设置中断状态时，这些命令具有以下效果：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Command</th>
<th align="left">状态名称</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>sxe</strong></p></td>
<td align="left"><p><strong>分</strong></p>
<p><strong>能够</strong></p></td>
<td align="left"><p>发生此异常时，目标会在激活任何其他错误处理程序之前立即中断调试器。 这种处理称为<em>第一次机会</em>处理。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>sxd</strong></p></td>
<td align="left"><p><strong>第二次中断</strong></p>
<p><strong>Disabled</strong></p></td>
<td align="left"><p>对于此类型的第一次异常，调试器不会中断（尽管显示了一条消息）。 如果其他错误处理程序未解决此异常，将停止执行，并将目标中断到调试器中。 这种处理称为<em>第二次机会</em>处理。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>sxn</strong></p></td>
<td align="left"><p><strong>输出</strong></p>
<p><strong>警告</strong></p></td>
<td align="left"><p>发生此异常时，目标应用程序根本不会中断调试器。 但是，会显示一条消息，通知用户此异常。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>sxi</strong></p></td>
<td align="left"><p><strong>暂且</strong></p></td>
<td align="left"><p>发生此异常时，目标应用程序根本不会中断调试器，而且不显示任何消息。</p></td>
</tr>
</tbody>
</table>

设置处理状态时，这些命令具有以下效果：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Command</th>
<th align="left">状态名称</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>sxe</strong></p></td>
<td align="left"><p><strong>妥善</strong></p></td>
<td align="left"><p>继续执行时，该事件被视为已处理。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>sxd、sxn、sxi</strong></p></td>
<td align="left"><p><strong>未处理</strong></p></td>
<td align="left"><p>继续执行时，该事件被视为未处理。</p></td>
</tr>
</tbody>
</table>

可以结合使用 **-h**选项和异常，而不是事件。 将此选项与**ch**、 **bpe**或**sse**一起使用将分别设置**hc**、 **bpec**或**ssec**的处理状态。 如果对任何其他事件使用-h 选项，则该选项不起作用。

将 **-c**或 **-c2**选项与**hc**、 **bpec**或**ssec**一起使用时，会将指定的命令分别与**ch**、 **bpe**或**sse**关联。

在下面的示例中， **sxe**命令用于将访问冲突事件的中断状态设置为在第一次机会时中断，并设置将在该点执行到**r eax**的第一条命令。 然后使用**sx**命令将第一条命令更改为**r ebx**，而无需更改处理状态。 最后，显示**sx**输出的一部分，指示访问冲突事件的当前设置：

```dbgcmd
0:000> sxe -c "r eax" av

0:000> sx- -c "r ebx" av

0:000> sx
 av - Access violation - break - not handled
       Command: "r ebx"
  . . .  
```
