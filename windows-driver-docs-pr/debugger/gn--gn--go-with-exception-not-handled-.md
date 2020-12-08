---
title: gn、gN（转到未经处理的异常）
description: Gn 和 gN 命令继续执行给定线程，而不会将异常标记为已处理。 这允许应用程序的异常处理程序处理异常。
keywords:
- gn，gN (在未处理的异常) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- gn, gN (Go with Exception Not Handled)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 887d74a5eb6bad23ce1d8f942c461ce9f5ec9b93
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798375"
---
# <a name="gn-gn-go-with-exception-not-handled"></a>gn、gN（转到未经处理的异常）


**Gn** 和 **gn** 命令继续执行给定线程，而不会将异常标记为已处理。 这允许应用程序的异常处理程序处理异常。

User-Mode 语法

```dbgcmd
[~Thread] gn[a] [= StartAddress] [BreakAddress ... [; BreakCommands]] 
[~Thread] gN[a] [= StartAddress] [BreakAddress ... [; BreakCommands]] 
```

Kernel-Mode 语法

```dbgcmd
gn[a] [= StartAddress] [BreakAddress ... [; BreakCommands]] 
gN[a] [= StartAddress] [BreakAddress ... [; BreakCommands]] 
```

## <a name="span-idddk_cmd_go_with_exception_not_handled_dbgspanspan-idddk_cmd_go_with_exception_not_handled_dbgspanparameters"></a><span id="ddk_cmd_go_with_exception_not_handled_dbg"></span><span id="DDK_CMD_GO_WITH_EXCEPTION_NOT_HANDLED_DBG"></span>参数


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span>*Thread*   
仅) 指定要执行的线程 (用户模式。 此线程必须已由异常停止。 有关语法的详细信息，请参阅 [线程语法](thread-syntax.md)。

<span id="_______a______"></span><span id="_______A______"></span>**一个**   
使此命令创建的任何断点作为处理器断点 (例如，由 " [**ba**](ba--break-on-access-.md) " 创建的断点) 而不是软件断点 (类似于通过 [**bp**](bp--bu--bm--set-breakpoint-.md) 和 **bm.exe**) 创建的断点。 如果未指定 *BreakAddress* ，则不会创建任何断点并且 **标志不** 起作用。

<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span>*StartAddress*   
指定应开始执行的地址。 如果未指定此，则调试器将执行传递给发生异常的地址。 有关更多语法详细信息，请参阅 [地址和地址范围语法](address-and-address-range-syntax.md)。

<span id="_______BreakAddress______"></span><span id="_______breakaddress______"></span><span id="_______BREAKADDRESS______"></span>*BreakAddress*   
指定断点的地址。 如果指定了 *BreakAddress* ，则它必须指定一个指令地址 (即，该地址必须包含指令) 的第一个字节。 一次最多可指定10个中断地址（按任意顺序）。 如果无法解析 *BreakAddress* ，则会将其存储为 [无法解析的断点](unresolved-breakpoints---bu-breakpoints-.md)。 有关更多语法详细信息，请参阅 [地址和地址范围语法](address-and-address-range-syntax.md)。

<span id="_______BreakCommands______"></span><span id="_______breakcommands______"></span><span id="_______BREAKCOMMANDS______"></span>*BreakCommands*   
指定当命中 *BreakAddress* 指定的断点时，将自动执行的一个或多个命令。 *BreakCommands* 参数前面必须有一个分号。 如果指定多个 *BreakAddress* 值，则 *BreakCommands* 将应用于所有值。

**注意**   仅当要将此命令嵌入到另一个命令使用的命令字符串（例如，在另一个断点命令内或除了或事件设置中）时， *BreakCommands* 参数才可用。 在命令行上，分号将终止该命令，并在完成 **gn** 或 **gn** 命令后立即执行在分号后列出的任何其他命令。

 

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
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关发出此命令的其他方法以及相关命令的概述，请参阅 [控制目标](controlling-the-target.md)。

<a name="remarks"></a>备注
-------

如果在断点处未停止调试器， **gn** 和 **gn** 的行为会完全相同。 如果调试器在断点处停止， **gn** 将不起作用;若要执行此命令，必须大写 "N"。 这是一种安全预防措施，因为继续未处理断点的方法很少。

如果使用 *BreakAddress* 参数设置断点，此新断点将仅由当前线程触发。 不会停止在该位置执行代码的其他线程。

如果指定了 *thread* ，则会在指定的线程未冻结且所有其他线程冻结时执行 **gn** 命令。 例如，如果指定 **~ 123gn**， **~ \# gn**，或 **~ \* gn** 命令，指定的线程将处于解冻状态，并且所有其他线程都将被冻结。

 

 





