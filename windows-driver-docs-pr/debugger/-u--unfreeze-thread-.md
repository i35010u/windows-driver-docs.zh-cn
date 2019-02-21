---
title: ~ u （取消冻结线程）
description: ~ U 命令取消冻结指定的线程。不要混淆此命令使用 U （反汇编） 命令。
ms.assetid: 6ac3c84a-3734-4b16-a239-4233e186c2df
keywords:
- ~ u （取消冻结线程） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ~u (Unfreeze Thread)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f1a6a3486589d110713195e82536b06ba07b7f68
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521559"
---
# <a name="u-unfreeze-thread"></a>~ u （取消冻结线程）


**~ U**命令取消冻结指定的线程。

不要将使用此命令相混淆[ **U （反汇编）** ](u--unassemble-.md)命令。

```dbgcmd
~Thread u 
```

## <a name="span-idddkcmdunfreezethreaddbgspanspan-idddkcmdunfreezethreaddbgspanparameters"></a><span id="ddk_cmd_unfreeze_thread_dbg"></span><span id="DDK_CMD_UNFREEZE_THREAD_DBG"></span>参数


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *线程*   
指定的线程或线程取消。 有关语法的详细信息，请参阅[线程语法](thread-syntax.md)。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>仅限用户模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

详细了解如何已冻结线程的行为和控制冻结的其他命令的列表，以及挂起的线程，请参阅[控制进程和线程](controlling-processes-and-threads.md)。

<a name="remarks"></a>备注
-------

仅在用户模式下，可以指定线程。 在内核模式下颚化符 （~） 是指一个处理器。

下面的示例显示如何使用 ~ 命令。

下面的命令显示所有线程的当前状态。

```dbgcmd
0:000> ~* k
```

以下命令冻结导致当前异常的线程。

```dbgcmd
0:000> ~# f
```

以下命令将检查挂起此线程的状态。

```dbgcmd
0:000> ~* k
```

以下命令取消冻结线程号 123。

```dbgcmd
0:000> ~123 u
```

 

 





