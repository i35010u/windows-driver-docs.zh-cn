---
title: 's (设置当前系统) '
description: S 命令将设置或显示当前的系统编号。
keywords:
- s (设置当前系统) Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- s (Set Current System)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f7a34e102560a92f21178361067c9b891f21796a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800179"
---
# <a name="s-set-current-system"></a>||s（设置当前系统）

**| |s** 命令设置或显示当前的系统编号。

```dbgcmd
     ||System s 
     || s 
```

不要将此命令与 [**(搜索内存)**](s--search-memory-.md)、 [**~ s (更改当前处理器)**](-s--change-current-processor-.md)、 [**~ s (设置为当前线程)**](-s--set-current-thread-.md)或 [**| s (设置当前进程)**](-s--set-current-process-.md) 命令混淆。


## <a name="span-idddk_cmd_set_current_system_dbgspanspan-idddk_cmd_set_current_system_dbgspanparameters"></a><span id="ddk_cmd_set_current_system_dbg"></span><span id="DDK_CMD_SET_CURRENT_SYSTEM_DBG"></span>参数


<span id="_______System______"></span><span id="_______system______"></span><span id="_______SYSTEM______"></span>*系统*   
指定要激活的系统编号。 有关语法的详细信息，请参阅 [系统语法](system-syntax.md)。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>多目标调试</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**| |** 在调试多个目标或使用多个转储文件时，s 命令很有用。  有关这些类型的会话的详细信息，请参阅 [调试多个目标](debugging-multiple-targets.md)。

如果使用 **| |s** 语法，调试器会显示当前系统的相关信息。

此命令还将反汇编当前系统、进程和线程的当前指令。

 
**注意**   在调试实时目标并将目标转储到一起时，有一些复杂的问题，因为每种调试类型的命令的行为有所不同。 例如，如果在当前系统为转储文件时使用 **g (中转)** 命令，则调试器将开始执行，但无法中断到调试器中，因为 break 命令未被识别为对转储文件调试无效。









