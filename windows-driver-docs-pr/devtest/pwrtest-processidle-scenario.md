---
title: PwrTest ProcessIdle 方案
description: PwrTest ProcessIdle 方案强制后台维护任务以运行 （现在而非在其计划的时间），并监视其进度。
ms.assetid: 14932191-C956-4623-AF62-5A6650D72164
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8768034c5c4dc1b1cd189d9489a141c1883979f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382665"
---
# <a name="pwrtest-processidle-scenario"></a>PwrTest ProcessIdle 方案


PwrTest ProcessIdle 方案强制后台维护任务以运行 （现在而非在其计划的时间），并监视其进度。

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>语法


```
pwrtest /processidle [/t:n] [/?] 
```

<span id="_t_n"></span><span id="_T_N"></span>**/t:**<em>n</em>  
为方案运行之后, 在等待被中止，指定的最大时间 （以分钟为单位），即使空闲任务继续运行 （默认值为运行，直到完成所有任务）。

**示例**

```
pwrtest /processidle  
```

```
pwrtest /processidle  /t:30
```

### <a name="span-idxmllogfileoutputspanspan-idxmllogfileoutputspanspan-idxmllogfileoutputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML 日志文件输出

```XML
<PwrTestLog>
  <SystemInformation>
  </SystemInformation>
  <ProcessIdle> 
    <JobStart>
      <Timestamp></Timestamp>
      <TaskName></TaskName>
    </JobStart>
    <JobEndSuccess>
      <Timestamp></Timestamp>
      <TaskName></TaskName>
    </JobEndSuccess>
    <JobEndFailure>
      <Timestamp></Timestamp>
      <TaskName></TaskName>
    </JobEndFailure>
    <JobEndTermination>
      <Timestamp></Timestamp>
      <TaskName></TaskName>
    </JobEndTermination>
    <JobCompletionPending>
      <Timestamp></Timestamp>
      <TaskName></TaskName>
    </JobCompletionPending>
    <IdleTaskRegister>
      <Timestamp></Timestamp>
      <TaskName></TaskName>
      <ProcessId></ProcessId>
    </IdleTaskRegister>
    <IdleTaskUnregister>
      <Timestamp></Timestamp>
      <TaskName></TaskName>
      <ProcessId></ProcessId>
    </IdleTaskUnregister>
    <IdleTaskStart>
      <Timestamp></Timestamp>
      <TaskName></TaskName>
      <ProcessId></ProcessId>
    </IdleTaskStart>
    <IdleTaskStop>
      <Timestamp></Timestamp>
      <TaskName></TaskName>
      <ProcessId></ProcessId>
    </IdleTaskStop>
    <IdleTaskNotifyStart>
      <Timestamp></Timestamp>
      <TaskName></TaskName>
      <ProcessId></ProcessId>
    </IdleTaskNotifyStart>
    <IdleTaskNotifyComplete>
      <Timestamp></Timestamp>
      <TaskName></TaskName>
      <ProcessId></ProcessId>
    </IdleTaskNotifyComplete>
    <OtherProcessIdleTasksCallsInProgress>
      <Timestamp></Timestamp>
    </OtherProcessIdleTasksCallsInProgress>
  </ProcessIdle>
</PwrTestLog> 
```

下表介绍日志文件中显示的 XML 元素。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">元素</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>&lt;ProcessIdle&gt;</strong></td>
<td align="left"><p>包含所有不同的进程空闲事件。 只有一个<strong>&lt;ProcessIdle&gt;</strong> PwrTest 日志文件中的元素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;时间戳&gt;</strong></td>
<td align="left"><p>任何给定事件的时间戳。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;TaskName&gt;</strong></td>
<td align="left"><p>空闲任务的名称。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ProcessID&gt;</strong></td>
<td align="left"><p>空闲任务的进程 ID。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;JobStart&gt;</strong></td>
<td align="left"><p>事件表示作业启动。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;JobEndSuccess&gt;</strong></td>
<td align="left"><p>事件表示已成功完成的作业。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;JobEndFailure&gt;</strong></td>
<td align="left"><p>事件指示作业失败。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;JobEndTermination&gt;</strong></td>
<td align="left"><p>事件指示作业已提前终止。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;JobCompletionPending&gt;</strong></td>
<td align="left"><p>事件指示完成作业仍为挂起。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;IdleTaskRegister&gt;</strong></td>
<td align="left"><p>事件表示已注册的空闲状态的任务。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;IdleTaskUnregister&gt;</strong></td>
<td align="left"><p>事件指示空闲任务已取消注册。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;IdleTaskStart&gt;</strong></td>
<td align="left"><p>事件指示空闲任务已开始。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;IdleTaskStop&gt;</strong></td>
<td align="left"><p>事件指示空闲任务已停止。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;IdleTaskNotifyStart&gt;</strong></td>
<td align="left"><p>事件指示进程已调用空闲任务。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;IdleTaskNotifyComplete&gt;</strong></td>
<td align="left"><p>事件指示进程已完成调用空闲任务。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;OtherProcessIdleTasksCallsInProgress&gt;</strong></td>
<td align="left"><p>事件指示调用的另一个进程<strong>ProcessIdleTasks</strong>背景中的函数。 请注意，调用 Pwrtest <strong>ProcessIdleTasks</strong> advapi32.dll 导出的函数。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[PwrTest 语法](pwrtest-syntax.md)

 

 






