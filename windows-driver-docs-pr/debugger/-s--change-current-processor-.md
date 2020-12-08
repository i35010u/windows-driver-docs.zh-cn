---
title: ~s（更改当前处理器）
description: ~ S 命令设置在多处理器系统上调试的处理器。在内核模式下，~ s 会更改当前处理器。
keywords:
- 将当前处理器 (~ s) 命令更改
- 多处理器计算机，将当前处理器 (~ s) 命令
- 款
- ~ s (更改当前处理器) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ~s (Change Current Processor)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 32a8d83c0b4cbdd8dcb86de07914bb4077947c87
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805799"
---
# <a name="s-change-current-processor"></a>~s（更改当前处理器）


**~ S** 命令设置在多处理器系统上调试的处理器。

在内核模式下， **~ s** 会更改当前处理器。 不要将此命令与 [**~ s (设置 "当前线程)**](-s--set-current-thread-.md) " 命令 (该命令仅在用户模式下有效) ， [**| s ("设置当前进程)**](-s--set-current-process-.md) 命令" [**| |s (设置当前系统)**](--s--set-current-system-.md) 命令或 [**s (Search Memory)**](s--search-memory-.md) 命令。

```dbgcmd
~Processor s
```

## <a name="span-idddk_cmd_change_current_processor_dbgspanspan-idddk_cmd_change_current_processor_dbgspanparameters"></a><span id="ddk_cmd_change_current_processor_dbg"></span><span id="DDK_CMD_CHANGE_CURRENT_PROCESSOR_DBG"></span>参数


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span>*处理器*   
指定要调试的处理器的数目。

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
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

只能在内核模式下指定处理器。 在用户模式下，颚化 (~) 引用线程。

您可以通过内核调试提示符的形状立即告诉您何时使用多处理器系统。 在以下示例中，0：表示正在调试计算机中的第一个处理器。

```dbgcmd
0: kd>
```

使用以下命令在处理器之间切换：

```dbgcmd
0: kd> ~1s
1: kd>
```

现在，是正在调试的计算机中的第二个处理器。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[多处理器语法](multiprocessor-syntax.md)

 

 






