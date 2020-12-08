---
title: .bpsync（同步断点处的线程）
description: 当线程到达断点时，bpsync 命令将冻结所有其他线程，直至断点应用到的线程通过该断点。
keywords:
- bpsync (在断点) Windows 调试时同步线程
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .bpsync (Synchronize Threads at Breakpoint)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b35b5d58015c3aa5c8aef75502ce2bdf8cdb2876
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799959"
---
# <a name="bpsync-synchronize-threads-at-breakpoint"></a>.bpsync（同步断点处的线程）


当线程到达断点时， **bpsync** 命令将冻结所有其他线程，直至断点应用到的线程通过该断点。

```dbgcmd
.bpsync 1
.bpsync 0
.bpsync 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______1______"></span>**1**   
导致所有线程在一个线程到达断点时冻结。 断点所应用到的线程通过该断点逐步完成后，其他线程会解冻。

<span id="_______0______"></span>**0**   
允许其他线程在一个线程到达断点时继续执行。 这是默认行为。

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
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

不带参数的。 **bpsync** 命令显示当前规则管理断点同步行为。

**Bpsync** 命令适用于 (通过 [**最佳实践**](bp--bu--bm--set-breakpoint-.md)、 **bu** 或 **bm.exe**) 设置的软件断点，以及 (用 [**ba**](ba--break-on-access-.md)) 设置的处理器断点。

如果有多个线程可以通过同一代码运行，则 **bpsync 1** 命令对于捕获所有断点事件都非常有用。 如果不使用此命令，则会丢失断点，因为到达断点的第一个线程始终导致调试器暂时删除该断点。 在删除断点的短时间内，其他线程可以到达代码中的同一位置，而不会按预期触发断点。

断点的临时删除是调试程序操作的一个正常环节。 当目标到达断点并且恢复时，调试器必须暂时删除断点，以便目标可以执行实际代码。 执行实际指令后，调试器重新插入中断。 要执行此操作，调试器会将代码还原 (或关闭数据中断) ，执行单步操作，然后将其放回。

请注意，如果使用 **bpsync 1**，则已冻结的线程之间存在死锁风险。

 

 





