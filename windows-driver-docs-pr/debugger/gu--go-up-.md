---
title: gu（向上）
description: Gu 命令导致目标执行到当前函数完成。
keywords:
- gu () Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- gu (Go Up)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 29d3b7e56ecc7a784c31e928a2e2f69b658e2ac5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828199"
---
# <a name="gu-go-up"></a>gu（向上）


**Gu** 命令导致目标执行到当前函数完成。

User-Mode 语法

```dbgcmd
[~Thread] gu 
```

Kernel-Mode 语法

```dbgcmd
gu
```

## <a name="span-idddk_cmd_go_up_dbgspanspan-idddk_cmd_go_up_dbgspanparameters"></a><span id="ddk_cmd_go_up_dbg"></span><span id="DDK_CMD_GO_UP_DBG"></span>参数


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span>*Thread*   
仅) 指定要执行的线程 (用户模式。 此线程必须已由异常停止。 有关语法的详细信息，请参阅 [线程语法](thread-syntax.md)。

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

如果当前函数调用返回，则 **gu** 命令会执行目标。

如果以递归方式调用当前函数，则 **在当前** 函数的 *当前实例* 返回之前，将不会暂停执行。 采用这种方式时， **gu** 不同于 **g @ $ra**，这会在每次命中此函数的返回地址时停止。

**注意**  **Gu** 命令通过测量调用堆栈深度来区分函数的不同实例。 在将参数推送到堆栈上并刚好调用之前，在程序集模式下执行此命令可能会导致此度量值不正确。 通过编译器优化的函数返回可能会导致此命令在此返回的错误实例处停止。 这些错误非常少见，只能在递归函数调用期间发生。

 

如果指定了 *thread* ，则会在指定的线程未冻结且所有其他线程冻结时执行 **gu** 命令。 例如，如果指定 **~ 123gu**， **~ \# gu**，或 **~ \* gu** 命令，指定的线程将处于解冻状态，并且所有其他线程都将被冻结。

 

 





