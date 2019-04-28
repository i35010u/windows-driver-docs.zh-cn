---
title: gu（向上）
description: Gu 命令会导致目标以执行，直到当前函数已完成。
ms.assetid: 10022292-92a4-4663-b277-26aa3c0d73a7
keywords:
- gu （向上转） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- gu (Go Up)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 840c33d31bc3bf7358d7fdda939a35d0f2a8bea6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342030"
---
# <a name="gu-go-up"></a>gu（向上）


**Gu**命令将导致目标以执行，直到当前函数已完成。

用户模式语法

```dbgcmd
[~Thread] gu 
```

内核模式语法

```dbgcmd
gu
```

## <a name="span-idddkcmdgoupdbgspanspan-idddkcmdgoupdbgspanparameters"></a><span id="ddk_cmd_go_up_dbg"></span><span id="DDK_CMD_GO_UP_DBG"></span>参数


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *线程*   
（仅限用户模式）指定要执行的线程。 此线程必须被异常停止。 有关语法的详细信息，请参阅[线程语法](thread-syntax.md)。

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

**Gu**命令执行目标，直到当前函数调用返回。

如果当前函数调用以递归方式， **gu**命令将不会暂停执行，直到*当前实例*当前函数的返回。 这样一来， **gu**区别**g @$ ra**，这将停止任何次命中此函数的返回地址。

**请注意**   **gu**命令通过测量的调用堆栈深度区分不同的函数实例。 在程序集模式下执行此命令后参数已推送到堆栈并进行调用之前可能会导致此测量值不正确的错误。 函数返回该编译器优化掉同样可能会导致此命令可在此返回了错误的实例停止。 这些错误很少见，并且只发生在递归函数调用的过程。

 

如果*线程*指定，则**gu**执行命令并指定的线程解冻和所有其他被冻结。 例如，如果 **~ 123gu**，  **~ \#gu**，或者 **~ \*gu**指定命令，则指定的线程是未冻结和所有其他用户均已冻结。

 

 





