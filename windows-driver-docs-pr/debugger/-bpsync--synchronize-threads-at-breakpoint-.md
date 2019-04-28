---
title: .bpsync（同步断点处的线程）
description: 当一个线程到达断点时，.bpsync 命令冻结所有其他线程，直到该断点适用的线程具有单步遍历该断点。
ms.assetid: 3e97ea97-77b8-4a22-b49c-c99739b42d59
keywords:
- .bpsync （同步在断点处的线程） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .bpsync (Synchronize Threads at Breakpoint)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6e646158b0e11a9cd337c7ab3a0973cc55d50b19
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336983"
---
# <a name="bpsync-synchronize-threads-at-breakpoint"></a>.bpsync（同步断点处的线程）


当线程到达一个断点 **.bpsync**命令冻结所有其他线程，直到该断点适用的线程具有单步遍历该断点。

```dbgcmd
.bpsync 1
.bpsync 0
.bpsync 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______1______"></span> **1**   
导致所有线程 freeze 时一个线程已到达断点。 断点适用的线程具有单步遍历该断点后，其他线程是未冻结。

<span id="_______0______"></span> **0**   
允许其他线程继续执行一个线程已到达断点时。 这是默认行为。

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

 

<a name="remarks"></a>备注
-------

不带任何参数。 **.bpsync**命令显示当前用于管理断点同步行为的规则。

**.Bpsync**命令同时适用于软件断点 (使用设置[ **bp**](bp--bu--bm--set-breakpoint-.md)， **bu**，或**bm**)和处理器的断点 (使用设置[ **ba**](ba--break-on-access-.md))。

如果存在相同的代码，通过运行多个线程的情况 **.bpsync 1**命令也可用于捕获所有断点匹配项。 而无需此命令中，因为要始终到达该断点的第一个线程会导致调试器，暂时删除断点，可能会错过断点匹配项。 删除断点的时间短时间，而在其他线程无法达到代码中的同一位置和不会按预期触发断点。

临时删除断点是调试器操作正常方面。 当目标达到断点并恢复时，调试器必须暂时删除的断点，以便目标可以执行的实际代码。 实际指令执行完毕后，调试器将构思中断。 若要执行此操作，调试器将还原代码 （或关闭数据分隔线），执行单步，并返回放入中断。

请注意，如果您使用 **.bpsync 1**，已被冻结的线程之间的死锁的风险。

 

 





