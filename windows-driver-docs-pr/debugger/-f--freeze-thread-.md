---
title: ~ f （冻结线程）
description: ~ F 命令冻结给定的线程，使其停止，并等待，直到它是未冻结。不要混淆此命令使用 f （填充内存） 命令。
ms.assetid: 86fbbcee-c752-4425-a330-4d95a4069b0d
keywords:
- ~ f （冻结线程） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ~f (Freeze Thread)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fe2de154ad16c54c4a465491a19bccbad4bddd22
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544392"
---
# <a name="f-freeze-thread"></a>~ f （冻结线程）


**~ F**命令冻结给定的线程，使其停止，并等待，直到它是未冻结。

不要将使用此命令相混淆[ **f （填充内存）** ](f--fp--fill-memory-.md)命令。

```dbgcmd
~Thread f 
```

## <a name="span-idddkcmdfreezethreaddbgspanspan-idddkcmdfreezethreaddbgspanparameters"></a><span id="ddk_cmd_freeze_thread_dbg"></span><span id="DDK_CMD_FREEZE_THREAD_DBG"></span>参数


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *线程*   
指定要冻结的线程。 有关语法的详细信息，请参阅[线程语法](thread-syntax.md)。

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

**~ F**命令使指定的线程冻结。 当调试器，目标应用程序继续执行时，其他线程执行，因为此线程将一直处于停止按预期。

下面的示例显示如何使用此命令。 下面的命令显示所有线程的当前状态。

```dbgcmd
0:000> ~* k
```

以下命令会冻结，导致当前异常的线程。

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

 

 





