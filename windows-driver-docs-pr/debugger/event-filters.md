---
title: 事件筛选器
description: 事件筛选器
ms.assetid: 91f2a483-8971-42de-a6c5-cc25409279a5
keywords:
- 调试器引擎 API，事件筛选器
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: c71c0ad01505a2831acc9de511406a7ff8289248
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366874"
---
# <a name="event-filters"></a>事件筛选器


*事件筛选器*提供简单的事件筛选; 它们影响调试器引擎如何在目标中的事件发生后继续执行。 事件发生时，引擎将确定该事件是否与事件筛选器相匹配。 如果是这样，事件筛选器的中断状态会影响是否调试器将中断到目标。 如果事件是一个异常事件，处理的状态决定是否应考虑该异常将已处理或不处理在目标中。

**请注意**  如果需要更复杂的事件筛选时，可以使用事件的回调。

 

事件筛选器划分为三个类别。

1.  *特定事件筛选器*。 这些是为所有非异常事件的筛选器。 请参阅[**调试\_筛选器\_XXX** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-filter-xxx)有关这些事件的列表。

2.  *特定异常筛选器*。 第一个特定的异常筛选器是*默认异常筛选器*。 其余部分是为这些异常，该引擎还具有内置筛选器的筛选器。 请参阅[**特定异常**](https://docs.microsoft.com/windows-hardware/drivers/debugger/specific-exceptions)为特定的异常筛选器的列表。

3.  *任意异常筛选器*。 这些是手动添加的异常事件的筛选器。

类别 1 和 2 中的筛选器统称为*特定筛选器*，和类别 2 和 3 中的筛选器统称为*异常筛选器*。 通过返回的每个类别中的筛选器数[ **GetNumberEventFilters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getnumbereventfilters)。

事件符合特定的事件筛选器的事件类型是否与筛选器的类型相同。 某些事件筛选器具有一个附加参数，其进一步限制它们匹配的事件。

如果异常事件的异常代码是异常筛选器的异常代码相同，则异常事件匹配异常筛选器。 如果存在具有相同的异常代码为异常事件的任何异常筛选器，默认的异常筛选器将处理的异常事件。

### <a name="span-idcommandsandparametersspanspan-idcommandsandparametersspancommands-and-parameters"></a><span id="commands_and_parameters"></span><span id="COMMANDS_AND_PARAMETERS"></span>命令和参数

事件筛选器可以有与之关联的调试器命令。 筛选器匹配的事件发生时，该引擎被执行此命令。 [**GetEventFilterCommand** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-geteventfiltercommand)并[ **SetEventFilterCommand** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-seteventfiltercommand)可用于获取和设置此命令。 异常筛选器，对异常的最可能执行此命令。 在第二个可能发生的异常事件时，可以执行单独的第二次命令。 若要获取和设置第二次命令，使用[ **GetExceptionFilterSecondCommand** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getexceptionfiltersecondcommand)并[ **SetExceptionSecondChanceCommand**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-setexceptionfiltersecondcommand)。

返回特定的事件筛选器和异常筛选器的参数[ **GetSpecificFilterParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getspecificfilterparameters)并[ **GetExceptionFilterParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-setexceptionfilterparameters). 可以使用将设置中断状态和事件筛选器的处理状态[ **SetSpecificFilterParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-setspecificfilterparameters)并**SetExceptionFilterParameters**。

**SetExceptionFilterParameters**还可用来添加和删除任意异常筛选器。

返回特定筛选器的简短说明[ **GetEventFilterText**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-geteventfiltertext)。

某些特定的筛选器都限制在筛选器匹配的事件的参数。 [**GetSpecificFilterArgument** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getspecificfilterargument)并[ **SetSpecificFilterArgument** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-setspecificfilterargument)将获取并设置这些特定的筛选器支持的参数的参数。 如果某个特定筛选器不具有任何自变量，则与匹配的事件没有限制。 下表列出了参数和它们如何限制也将其进行匹配的事件的事件筛选器：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Event</th>
<th align="left">匹配条件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>创建进程</p></td>
<td align="left"><p>创建的进程的名称必须匹配 argument.1</p></td>
</tr>
<tr class="even">
<td align="left"><p>退出进程</p></td>
<td align="left"><p>已退出进程的名称必须匹配 argument.1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>负载模块</p></td>
<td align="left"><p>已加载模块的名称必须匹配 argument.1</p></td>
</tr>
<tr class="even">
<td align="left"><p>卸载模块</p></td>
<td align="left"><p>卸载的基址必须是模块的与 argument.2 相同</p></td>
</tr>
<tr class="odd">
<td align="left"><p>目标输出</p></td>
<td align="left"><p>目标的调试输出必须匹配 argument.3</p></td>
</tr>
</tbody>
</table>

 

**注意**  
1.  参数使用了[字符串通配符语法](string-wildcard-syntax.md)进行比较 （忽略路径） 的映像名称与在事件发生时。 如果模块或进程的名称不可用，它被视为匹配项。

2.  参数是设置参数时由引擎计算的表达式。

3.  参数使用字符串通配符语法，与目标的调试输出进行比较。 如果不知道输出，它被视为匹配项。

 

### <a name="span-idindexandexceptioncodespanspan-idindexandexceptioncodespanindex-and-exception-code"></a><span id="index_and_exception_code"></span><span id="INDEX_AND_EXCEPTION_CODE"></span>索引和异常代码

每个事件筛选器的索引。 索引是介于零和一小于筛选器 （含） 的总数。 每个类别的筛选器的索引范围可从*SpecificEvents*， *SpecificExceptions*，并*ArbitraryExceptions* 返回值[ **GetNumberEventFilters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getnumbereventfilters)下, 表中所述：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">事件筛选器</th>
<th align="left">第一个筛选器的索引</th>
<th align="left">筛选器的数量</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>特定事件筛选器</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p><em>SpecificEvents</em></p></td>
</tr>
<tr class="even">
<td align="left"><p>特定异常筛选器</p></td>
<td align="left"><p><em>SpecificEvents</em></p></td>
<td align="left"><p><em>SpecificExceptions</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p>任意异常筛选器</p></td>
<td align="left"><p><em>SpecificEvents</em> + <em>SpecificExceptions</em></p></td>
<td align="left"><p><em>ArbitraryExceptions</em></p></td>
</tr>
</tbody>
</table>

 

本主题中的第一个表中找到特定的事件筛选器的索引[**调试\_筛选器\_XXX**](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-filter-xxx)。 默认异常筛选器 （第一个特定的异常筛选器） 的索引*SpecificEvents*。 删除任意异常筛选器后，可以更改的其他任意异常筛选器的索引。

由异常代码通常指定异常筛选器。 但是，某些方法要求使用异常的索引。 若要查找其索引的给定异常的异常筛选器，请使用[ **GetExceptionFilterParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getexceptionfilterparameters)要循环访问所有异常筛选器，直到找到一个与相同的异常代码异常。 主题中找不到特定的异常筛选器的异常代码[**特定异常**](https://docs.microsoft.com/windows-hardware/drivers/debugger/specific-exceptions)。

### <a name="span-idsystemerrorsspanspan-idsystemerrorsspansystem-errors"></a><span id="system_errors"></span><span id="SYSTEM_ERRORS"></span>系统错误

出现系统错误时，引擎将进入调试器或打印到输出流错误，如果保持为小于指定级别或发生错误。 这些级别返回的[ **GetSystemErrorControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getsystemerrorcontrol) ，可以使用更改[ **SetSystemErrorControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-setsystemerrorcontrol)。

 

 





