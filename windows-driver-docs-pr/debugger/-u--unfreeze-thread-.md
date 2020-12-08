---
title: ~u（解冻线程）
description: ~ U 命令 unfreezes 指定线程。请勿将此命令与 U (Unassemble) 命令混淆。
keywords:
- ~ u (解冻线程) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ~u (Unfreeze Thread)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4293e3c6786e7938ef5c1c78e044858de2f43a65
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795177"
---
# <a name="u-unfreeze-thread"></a>~u（解冻线程）


**~ U** 命令 unfreezes 指定线程。

请勿将此命令与 [**U (Unassemble)**](u--unassemble-.md) 命令混淆。

```dbgcmd
~Thread u 
```

## <a name="span-idddk_cmd_unfreeze_thread_dbgspanspan-idddk_cmd_unfreeze_thread_dbgspanparameters"></a><span id="ddk_cmd_unfreeze_thread_dbg"></span><span id="DDK_CMD_UNFREEZE_THREAD_DBG"></span>参数


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span>*Thread*   
指定要解冻的一个或一些线程。 有关语法的详细信息，请参阅 [线程语法](thread-syntax.md)。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>仅用户模式</p></td>
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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

若要详细了解冻结线程的行为方式和控制线程的冻结和挂起的其他命令的列表，请参阅 [控制进程和线程](controlling-processes-and-threads.md)。

<a name="remarks"></a>备注
-------

只能在用户模式下指定线程。 在内核模式下，颚化 (~) 引用处理器。

下面的示例演示如何使用 ~ 命令。

以下命令显示所有线程的当前状态。

```dbgcmd
0:000> ~* k
```

下面的命令冻结导致当前异常的线程。

```dbgcmd
0:000> ~# f
```

以下命令将检查此线程的状态是否为 "已挂起"。

```dbgcmd
0:000> ~* k
```

以下命令 unfreezes 线程号123。

```dbgcmd
0:000> ~123 u
```

 

 





