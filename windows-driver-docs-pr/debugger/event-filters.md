---
title: 事件筛选器
description: 事件筛选器
ms.assetid: 91f2a483-8971-42de-a6c5-cc25409279a5
keywords:
- 调试器引擎 API，事件筛选器
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6a3d129db21d7bcde1bdc53f3099f66963c9a57
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216662"
---
# <a name="event-filters"></a>事件筛选器


*事件筛选器* 提供简单的事件筛选;它们影响调试器引擎在目标中发生事件后如何继续。 事件发生时，引擎会确定该事件是否与事件筛选器匹配。 如果是这样，则事件筛选器的中断状态将影响调试器是否会中断到目标。 如果事件是异常事件，则处理状态确定是否应将异常视为已在目标中处理或未处理。

**注意**   如果需要更复杂的事件筛选，则可以使用事件回调。

 

事件筛选器分为三个类别。

1.  *特定的事件筛选器*。 这些是所有非异常事件的筛选器。 有关这些事件的列表，请参阅 [**调试 \_ 筛选器 \_ XXX**](./debug-filter-xxx.md) 。

2.  *特定异常筛选器*。 第一个特定的异常筛选器是 *默认的异常筛选*器。 其余的筛选器是针对其内置筛选器的异常的筛选器。 有关特定异常筛选器的列表，请参阅 [**特定异常**](./specific-exceptions.md) 。

3.  *任意异常筛选器*。 这些是手动添加的异常事件的筛选器。

类别1和2中的筛选器统称为 *特定筛选器*，类别2和3中的筛选器共同称为 *异常筛选器*。 [**GetNumberEventFilters**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getnumbereventfilters)返回每个类别中的筛选器数目。

如果事件的类型与筛选器的类型相同，则事件匹配特定的事件筛选器。 有些事件筛选器有一个额外的参数，该参数会进一步限制它们匹配的事件。

如果异常事件的异常代码与异常筛选器的异常代码相同，则异常事件会匹配异常筛选器。 如果没有异常筛选器与异常事件具有相同的异常代码，则会通过默认异常筛选器处理异常事件。

### <a name="span-idcommands_and_parametersspanspan-idcommands_and_parametersspancommands-and-parameters"></a><span id="commands_and_parameters"></span><span id="COMMANDS_AND_PARAMETERS"></span>命令和参数

事件筛选器可以有与之关联的调试器命令。 当与筛选器匹配的事件发生时，引擎将执行此命令。 [**GetEventFilterCommand**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-geteventfiltercommand) 和 [**SetEventFilterCommand**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-seteventfiltercommand) 可用于获取和设置此命令。 对于异常筛选器，此命令在第一次出现异常时执行。 可以在第二次异常事件时执行单独的第二次机会命令。 若要获取和设置第二个命令，请使用 [**GetExceptionFilterSecondCommand**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getexceptionfiltersecondcommand) 和 [**SetExceptionSecondChanceCommand**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-setexceptionfiltersecondcommand)。

特定事件筛选器和异常筛选器的参数由 [**GetSpecificFilterParameters**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getspecificfilterparameters) 和 [**GetExceptionFilterParameters**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-setexceptionfilterparameters)返回。 可以使用 [**SetSpecificFilterParameters**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-setspecificfilterparameters) 和 **SetExceptionFilterParameters**设置事件筛选器的中断状态和处理状态。

**SetExceptionFilterParameters** 也可用于添加和删除任意异常筛选器。

[**GetEventFilterText**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-geteventfiltertext)返回了特定筛选器的简短说明。

某些特定筛选器采用限制筛选器匹配的事件的参数。 [**GetSpecificFilterArgument**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getspecificfilterargument) 和 [**SetSpecificFilterArgument**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-setspecificfilterargument) 将获取并设置支持参数的特定筛选器的参数。 如果某个特定筛选器没有参数，则不会限制它匹配的事件。 下表列出了采用参数的事件筛选器，以及这些筛选器如何限制与它们匹配的事件：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">事件</th>
<th align="left">匹配条件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>创建进程</p></td>
<td align="left"><p>所创建进程的名称必须与参数匹配。1</p></td>
</tr>
<tr class="even">
<td align="left"><p>退出进程</p></td>
<td align="left"><p>退出的进程的名称必须与参数匹配。1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>加载模块</p></td>
<td align="left"><p>加载的模块的名称必须与参数匹配。1</p></td>
</tr>
<tr class="even">
<td align="left"><p>卸载模块</p></td>
<td align="left"><p>卸载的模块的基址必须与参数相同。2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>目标输出</p></td>
<td align="left"><p>目标的调试输出必须与参数匹配。3</p></td>
</tr>
</tbody>
</table>

 

**注意**  
1.  参数使用 [字符串通配符语法](string-wildcard-syntax.md) ，并与图像名称进行比较 (在发生事件时忽略路径) 。 如果模块或进程的名称不可用，则将其视为匹配项。

2.  参数是一个表达式，在设置参数时，引擎将计算该表达式。

3.  参数使用字符串通配符语法，并与目标中的调试输出进行比较。 如果输出未知，则视为匹配。

 

### <a name="span-idindex_and_exception_codespanspan-idindex_and_exception_codespanindex-and-exception-code"></a><span id="index_and_exception_code"></span><span id="INDEX_AND_EXCEPTION_CODE"></span>索引和异常代码

每个事件筛选器都有一个索引。 索引是一个介于0和1之间的数字，该数字小于筛选器总数 (包含) 。 可以从[**GetNumberEventFilters**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getnumbereventfilters)返回的*SpecificEvents*、 *SpecificExceptions*和*ArbitraryExceptions*值中找到每个筛选器类别的索引范围，如下表所述：

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
<th align="left">筛选器数</th>
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

 

特定事件筛选器的索引位于主题 " [**调试 \_ 筛选器 \_ XXX**](./debug-filter-xxx.md)" 中的第一个表中。 默认异常筛选器的索引 (第一个特定异常筛选器) 为 *SpecificEvents*。 删除任意异常筛选器后，其他任意异常筛选器的索引可能会更改。

异常筛选器通常由异常代码指定。 但是，某些方法需要异常的索引。 若要查找给定异常的异常筛选器的索引，请使用 [**GetExceptionFilterParameters**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getexceptionfilterparameters) 循环访问所有异常筛选器，直到找到具有与异常相同的异常代码的筛选器。 特定异常筛选器的异常代码可在主题 [**特定异常**](./specific-exceptions.md)中找到。

### <a name="span-idsystem_errorsspanspan-idsystem_errorsspansystem-errors"></a><span id="system_errors"></span><span id="SYSTEM_ERRORS"></span>系统错误

出现系统错误时，如果错误发生在指定级别或指定级别，则引擎将中断调试器或将错误输出到输出流。 这些级别由 [**GetSystemErrorControl**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getsystemerrorcontrol) 返回，可使用 [**SetSystemErrorControl**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-setsystemerrorcontrol)进行更改。

 

