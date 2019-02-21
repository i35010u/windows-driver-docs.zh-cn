---
title: g （转向）
description: G 命令开始执行给定的进程或线程。 BreakAddress 命中时，或另一个事件导致调试器停止时，执行将暂停程序，结尾处。
ms.assetid: 9b6aac94-6c53-40c2-a8de-2ad106678c65
keywords:
- g （转向） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- g (Go)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 42b9d7cd181a6c508374323b2ad877886a06c0d7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547540"
---
# <a name="g-go"></a>g （转向）


**G**命令开始执行给定的进程或线程。 执行该程序结束时都将停止时*BreakAddress*到达时，或导致调试器停止另一个事件。

用户模式语法

```dbgcmd
[~Thread] g[a] [= StartAddress] [BreakAddress ... [; BreakCommands]]
```

内核模式语法

```dbgcmd
g[a] [= StartAddress] [BreakAddress ... [; BreakCommands]] 
```

## <a name="span-idddkcmdgodbgspanspan-idddkcmdgodbgspanparameters"></a><span id="ddk_cmd_go_dbg"></span><span id="DDK_CMD_GO_DBG"></span>参数


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *线程*   
（仅限用户模式）指定要执行的线程。 有关语法的详细信息，请参阅[线程语法](thread-syntax.md)。

<span id="_______a______"></span><span id="_______A______"></span> **a**   
导致此命令为处理器断点创建任何断点 (如创建的[ **ba**](ba--break-on-access-.md)) 而不是软件断点 (如那些通过[**最佳实践** ](bp--bu--bm--set-breakpoint-.md)并**bm**)。 如果*BreakAddress*未指定，则不创建任何断点并标志不起作用。

<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span> *StartAddress*   
指定应开始执行的位置的地址。 如果不指定此选项，调试器将执行传递到由指令指针的当前值指定的地址。 有关语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。

<span id="_______BreakAddress______"></span><span id="_______breakaddress______"></span><span id="_______BREAKADDRESS______"></span> *BreakAddress*   
指定断点的地址。 如果*BreakAddress*指定，则它必须指定指令地址 （也即，地址必须包含一条指令的第一个字节）。 最多十个中断可以一次指定地址，按任意顺序。 如果*BreakAddress*无法解析，它将被视为[未解析的断点](unresolved-breakpoints---bu-breakpoints-.md)。 有关语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。

<span id="_______BreakCommands______"></span><span id="_______breakcommands______"></span><span id="_______BREAKCOMMANDS______"></span> *BreakCommands*   
指定一个或多个命令要自动执行由指定的断点*BreakAddress*命中。 *BreakCommands*参数前面必须带有一个分号。 如果多个*BreakAddress*指定的值*BreakCommands*适用于所有这些。

**请注意**   *BreakCommands*参数时要嵌入由另一个命令-例如，在另一个断点命令内或在命令字符串中的此命令才可用除或事件设置。 分号将终止命令行上**g**命令和任何其他命令列出后分号将执行后立即**g**完成命令。

 

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

发出此命令，并概述的相关命令的其他方法，请参阅[控制目标](controlling-the-target.md)。

<a name="remarks"></a>备注
-------

如果*线程*指定，则**g**执行命令并指定的线程解冻和所有其他被冻结。 例如，如果 **~ 123 g**，  **~ \#g**，或者 **~ \*g**指定命令时，指定线程未冻结和所有其他用户均已冻结。

 

 





