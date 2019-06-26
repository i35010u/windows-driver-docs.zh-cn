---
title: sx、sxd、sxe、sxi、sxn、sxr、sx-（设置异常）
description: Sx * 命令来控制调试程序会为正在调试的应用程序中发生异常时或发生某些事件时的操作。
ms.assetid: fdb5059f-e7d9-4e14-aa3d-030e72c30732
keywords:
- sx，sxd，sxe，sxi，sxn，sxr，sx-（设置异常） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- sx, sxd, sxe, sxi, sxn, sxr, sx- (Set Exceptions)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a7c29f87f569a5f921aa3fbea6955823bfc3c515
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366355"
---
# <a name="sx-sxd-sxe-sxi-sxn-sxr-sx--set-exceptions"></a>sx、sxd、sxe、sxi、sxn、sxr、sx-（设置异常）


**Sx * * *\** 命令控制则调试器会在应用程序正在调试的或发生某些事件时出现异常时的操作。

```dbgcmd
sx 

sx{e|d|i|n} [-c "Cmd1"] [-c2 "Cmd2"] [-h] {Exception|Event|*} 

sx- [-c "Cmd1"] [-c2 "Cmd2"] {Exception|Event|*} 

sxr
```

## <a name="span-idddkcmdsetexceptionsdbgspanspan-idddkcmdsetexceptionsdbgspanparameters"></a><span id="ddk_cmd_set_exceptions_dbg"></span><span id="DDK_CMD_SET_EXCEPTIONS_DBG"></span>参数


<span id="-c__Cmd1_"></span><span id="-c__cmd1_"></span><span id="-C__CMD1_"></span> **-c "** <em>Cmd1</em> **"**  
指定在出现异常或事件时执行的命令。 第一次的机会来处理此异常发生，而不考虑此异常是否进入调试器时执行此命令。 必须将*Cmd1*引号引起来的字符串。 此字符串可以包含多个命令，之间用分号分隔。 -C 和带引号的命令字符串之间的空间是可选的。

<span id="-c2_Cmd2_"></span><span id="-c2_cmd2_"></span><span id="-C2_CMD2_"></span> **-c2"** <em>Cmd2</em> **"**  
指定如果异常或事件发生，并且不处理第一次机会上执行的命令。 第二次机会来处理此异常发生，而不考虑此异常是否进入调试器时执行此命令。 必须将*Cmd2*引号引起来的字符串。 此字符串可以包含多个命令，之间用分号分隔。 空间-c2 之间和带引号的命令字符串是可选的。

<span id="_______-h______"></span><span id="_______-H______"></span> **-h**   
指定的事件的处理状态，而不是其中断状态更改。 如果*事件*是**cc**， **hc**， **bpec**，或**ssec**，无需使用 **-h**选项。

<span id="_______Exception______"></span><span id="_______exception______"></span><span id="_______EXCEPTION______"></span> *Exception*   
指定当前基数中的命令作用的异常编号。

<span id="_______Event______"></span><span id="_______event______"></span><span id="_______EVENT______"></span> *事件*   
指定命令作用的事件。 这些事件由短缩写标识。 有关事件的列表，请参阅[控制异常和事件](controlling-exceptions-and-events.md)。

<span id="______________"></span> **\\** *   
影响的不否则显式命名的所有异常**sx**。 显式命名的异常的列表，请参阅[控制异常和事件](controlling-exceptions-and-events.md)。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关中断状态和处理状态、 所有事件代码的说明、 所有事件的默认状态的列表，以及控制此状态的其他方法的详细信息，请参阅[控制异常和事件](controlling-exceptions-and-events.md)。

<a name="remarks"></a>备注
-------

**Sx**命令显示当前进程的异常的列表和所有 nonexception 事件的列表，并显示的每个异常和事件的调试器的默认行为。

**Sxe**， **sxd**， **sxn**，以及**sxi**命令控制每个异常和事件的调试器设置。

**Sxr**命令重置为默认设置的所有异常和事件筛选器状态。 命令已清除，break 和 continue 选项重置为默认设置时，依次类推。

**Sx-** 命令不会更改处理状态或指定的异常或事件的中断状态。 如果你想要更改的第一个 chance 命令或与特定事件关联的第二次命令，但不是希望更改任何其他内容，可以使用此命令。

如果包括 **-h**选项 (或者如果**cc**， **hc**， **bpec**，或**ssec**指定事件)，**sxe**， **sxd**， **sxn**，以及**sxi**命令控件[处理状态](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-filter-xxx#handling-status)的事件或异常。 在所有其他情况下，这些命令来控制[会中断状态](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-filter-xxx#break-status)的事件或异常。

当您在设置中断状态时，这些命令将产生以下影响。

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
<td align="left"><p><strong>中断</strong></p>
<p><strong>(Enabled)</strong></p></td>
<td align="left"><p>如果出现此异常，目标立即进入调试器之前激活任何其他错误处理程序。 处理此类称为<em>第一次机会</em>处理。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>sxd</strong></p></td>
<td align="left"><p><strong>第二个机会中断</strong></p>
<p><strong>（已禁用）</strong></p></td>
<td align="left"><p>（尽管显示一条消息） 调试器不会中断此类型的最可能的异常。 如果其他错误处理程序不能解决此异常，将停止执行，目标会中断到调试器。 处理此类称为<em>第二次机会</em>处理。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>sxn</strong></p></td>
<td align="left"><p><strong>Output</strong></p>
<p><strong>（通知）</strong></p></td>
<td align="left"><p>如果出现此异常，目标应用程序不会中断到调试器根本。 但是，将显示一条消息，告知用户此异常。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>sxi</strong></p></td>
<td align="left"><p><strong>Ignore</strong></p></td>
<td align="left"><p>如果出现此异常，目标应用程序不会在所有中断到调试器并不显示任何消息。</p></td>
</tr>
</tbody>
</table>

 

当您在设置的处理状态时，这些命令将产生以下影响：

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
<td align="left"><p><strong>处理</strong></p></td>
<td align="left"><p>该事件被视为已处理时继续执行。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>sxd,sxn,sxi</strong></p></td>
<td align="left"><p><strong>未处理</strong></p></td>
<td align="left"><p>该事件被视为未处理时继续执行。</p></td>
</tr>
</tbody>
</table>

 

可以使用 **-h**选项与异常，不是事件。 使用此选项与**ch**， **bpe**，或**sse**设置为处理状态**hc**， **bpec**，或**ssec**分别。 如果使用-h 选项与任何其他事件，它具有不起作用。

使用 **-c**或 **-c2**使用选项**hc**， **bpec**，或**ssec**将相关联的指定的命令与**ch**， **bpe**，或**sse**分别。

在以下示例中， **sxe**命令用于将中断状态的访问权限设置违规事件中断上第一次机会，并设置将为在该点执行的第一次机会命令**r eax**. 然后**sx-** 命令用于更改到的第一次机会命令**r ebx**，而无需更改处理状态。 最后，部分**sx**输出所示，该值指示访问冲突事件的当前设置：

```dbgcmd
0:000> sxe -c "r eax" av 

0:000> sx- -c "r ebx" av 

0:000> sx 
 av - Access violation - break - not handled
       Command: "r ebx"
  . . .  
```

 

 





