---
title: g（转到）
description: G 命令开始执行给定的进程或线程。 当命中 BreakAddress 或其他事件导致调试器停止时，执行将在程序结束时停止。
keywords:
- g (开始) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- g (Go)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 75aef2eacfa97b817b56bf33730fb0743353c603
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838179"
---
# <a name="g-go"></a>g（转到）


**G** 命令开始执行给定的进程或线程。 当命中 *BreakAddress* 或其他事件导致调试器停止时，执行将在程序结束时停止。

User-Mode 语法

```dbgcmd
[~Thread] g[a] [= StartAddress] [BreakAddress ... [; BreakCommands]]
```

Kernel-Mode 语法

```dbgcmd
g[a] [= StartAddress] [BreakAddress ... [; BreakCommands]] 
```

## <a name="span-idddk_cmd_go_dbgspanspan-idddk_cmd_go_dbgspanparameters"></a><span id="ddk_cmd_go_dbg"></span><span id="DDK_CMD_GO_DBG"></span>参数


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span>*Thread*   
仅) 指定要执行的线程 (用户模式。 有关语法的详细信息，请参阅 [线程语法](thread-syntax.md)。

<span id="_______a______"></span><span id="_______A______"></span>**一个**   
使此命令创建的任何断点作为处理器断点 (例如，由 " [**ba**](ba--break-on-access-.md) " 创建的断点) 而不是软件断点 (类似于通过 [**bp**](bp--bu--bm--set-breakpoint-.md) 和 **bm.exe**) 创建的断点。 如果未指定 *BreakAddress* ，则不会创建任何断点并且 **标志不** 起作用。

<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span>*StartAddress*   
指定应开始执行的地址。 如果未指定此值，调试器会将执行传递给指令指针的当前值指定的地址。 有关更多语法详细信息，请参阅 [地址和地址范围语法](address-and-address-range-syntax.md)。

<span id="_______BreakAddress______"></span><span id="_______breakaddress______"></span><span id="_______BREAKADDRESS______"></span>*BreakAddress*   
指定断点的地址。 如果指定了 *BreakAddress* ，则它必须指定一个指令地址 (即，该地址必须包含指令) 的第一个字节。 一次最多可指定10个中断地址（按任意顺序）。 如果无法解析 *BreakAddress* ，则会将其存储为 [无法解析的断点](unresolved-breakpoints---bu-breakpoints-.md)。 有关更多语法详细信息，请参阅 [地址和地址范围语法](address-and-address-range-syntax.md)。

<span id="_______BreakCommands______"></span><span id="_______breakcommands______"></span><span id="_______BREAKCOMMANDS______"></span>*BreakCommands*   
指定当命中 *BreakAddress* 指定的断点时，将自动执行的一个或多个命令。 *BreakCommands* 参数前面必须有一个分号。 如果指定多个 *BreakAddress* 值，则 *BreakCommands* 将应用于所有值。

**注意**   仅当要将此命令嵌入到另一个命令使用的命令字符串（例如，在另一个断点命令内或除了或事件设置中）时， *BreakCommands* 参数才可用。 在命令行上，分号将终止 **g** 命令，在完成 **g** 命令后，将立即执行在分号后列出的任何其他命令。

 

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

如果指定了 *thread* ，则会在指定的线程未冻结的情况下执行 **g** 命令，并冻结所有其他线程。 例如，如果指定 **~ 123g**、 **~ \# g** 或 **~ \* g** 命令，则指定的线程将解冻，并冻结所有其他线程。

 

 





