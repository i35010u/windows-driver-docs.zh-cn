---
title: gh（转到已处理的异常）
description: Gh 命令将标记为已处理的给定的线程的异常，并允许重新启动导致异常的指令处执行的线程。
ms.assetid: 3e06a3ff-b57d-435f-9625-011f38d7b26a
keywords:
- gh （转到异常处理） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- gh (Go with Exception Handled)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f42e7c2a2f07a925fe63a662f7de3350ade490d1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562536"
---
# <a name="gh-go-with-exception-handled"></a>gh（转到已处理的异常）


**Gh**命令将标记为已处理的给定的线程的异常，并允许重新启动导致异常的指令处执行的线程。

用户模式语法

```dbgcmd
[~Thread] gh[a] [= StartAddress] [BreakAddress ... [; BreakCommands]] 
```

内核模式语法

```dbgcmd
gh[a] [= StartAddress] [BreakAddress ... [; BreakCommands]] 
```

## <a name="span-idddkcmdgowithexceptionhandleddbgspanspan-idddkcmdgowithexceptionhandleddbgspanparameters"></a><span id="ddk_cmd_go_with_exception_handled_dbg"></span><span id="DDK_CMD_GO_WITH_EXCEPTION_HANDLED_DBG"></span>参数


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *线程*   
（仅限用户模式）指定要执行的线程。 此线程必须被异常停止。 有关语法的详细信息，请参阅[线程语法](thread-syntax.md)。

<span id="_______a______"></span><span id="_______A______"></span> **a**   
导致此命令为处理器断点创建任何断点 (如创建的[ **ba**](ba--break-on-access-.md)) 而不是软件断点 (如那些通过[**最佳实践** ](bp--bu--bm--set-breakpoint-.md)并**bm**)。 如果*BreakAddress*未指定，则不创建任何断点并标志不起作用。

<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span> *StartAddress*   
指定应开始执行的地址。 如果不指定此选项，调试器将通过执行到的地址发生了异常。 有关语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。

<span id="_______BreakAddress______"></span><span id="_______breakaddress______"></span><span id="_______BREAKADDRESS______"></span> *BreakAddress*   
指定断点的地址。 如果*BreakAddress*指定，则它必须指定指令地址 （也即，地址必须包含一条指令的第一个字节）。 最多十个中断可以一次指定地址，按任意顺序。 如果*BreakAddress*无法解析，它将被视为[未解析的断点](unresolved-breakpoints---bu-breakpoints-.md)。 有关语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。

<span id="_______BreakCommands______"></span><span id="_______breakcommands______"></span><span id="_______BREAKCOMMANDS______"></span> *BreakCommands*   
指定一个或多个命令要自动执行由指定的断点*BreakAddress*命中。 *BreakCommands*参数前面必须带有一个分号。 如果多个*BreakAddress*指定的值*BreakCommands*适用于所有这些。

**请注意**   *BreakCommands*参数时要嵌入由另一个命令-例如，在另一个断点命令内或在命令字符串中的此命令才可用除或事件设置。 分号将终止命令行上**gh**命令和任何其他命令列出后分号将执行后立即**gh**完成命令。

 

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

如果您使用*BreakAddress*参数来设置断点，此新断点只能由当前线程触发。 将不会停止执行该位置处的代码的其他线程。

如果*线程*指定，则**gh**执行命令并指定的线程解冻和所有其他被冻结。 例如，如果 **~ 123gh**，  **~ \#gh**，或者 **~ \*gh**指定命令，则指定的线程是未冻结和所有其他用户均已冻结。

 

 





