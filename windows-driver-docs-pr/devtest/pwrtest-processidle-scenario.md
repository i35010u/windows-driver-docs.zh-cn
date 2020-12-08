---
title: PwrTest ProcessIdle 方案
description: PwrTest ProcessIdle 方案强制后台维护任务 (立即运行，而不是在计划时间) 运行，并监视其进度。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f4c87ecf160064fe1fd07d705a57e5f70b0ff64
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824599"
---
# <a name="pwrtest-processidle-scenario"></a>PwrTest ProcessIdle 方案


PwrTest ProcessIdle 方案强制后台维护任务 (立即运行，而不是在计划时间) 运行，并监视其进度。

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>语法


```
pwrtest /processidle [/t:n] [/?] 
```

<span id="_t_n"></span><span id="_T_N"></span>**/t：**<em>n</em>  
指定运行方案) 的最长时间 (，在此时间之后等待将中止（即使空闲任务继续运行） (默认情况下将运行，直到所有任务都已完成) 。

**示例**

```
pwrtest /processidle  
```

```
pwrtest /processidle  /t:30
```

### <a name="span-idxml_log_file_outputspanspan-idxml_log_file_outputspanspan-idxml_log_file_outputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML 日志文件输出

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

下表描述了日志文件中显示的 XML 元素。

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
<td align="left"><p>包含所有不同的进程空闲事件。 PwrTest 日志文件中仅有一个<strong> &lt; ProcessIdle &gt; </strong>元素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;标志&gt;</strong></td>
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
<td align="left"><p>事件表示作业已启动。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;JobEndSuccess&gt;</strong></td>
<td align="left"><p>事件表明作业已成功完成。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;JobEndFailure&gt;</strong></td>
<td align="left"><p>事件指示作业失败。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;JobEndTermination&gt;</strong></td>
<td align="left"><p>事件表明作业提前终止。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;JobCompletionPending&gt;</strong></td>
<td align="left"><p>事件指示作业完成仍处于挂起状态。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;IdleTaskRegister&gt;</strong></td>
<td align="left"><p>事件表明空闲任务已注册。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;IdleTaskUnregister&gt;</strong></td>
<td align="left"><p>事件表明空闲任务已取消注册。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;IdleTaskStart&gt;</strong></td>
<td align="left"><p>事件表明空闲任务已启动。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;IdleTaskStop&gt;</strong></td>
<td align="left"><p>事件表明空闲任务已停止。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;IdleTaskNotifyStart&gt;</strong></td>
<td align="left"><p>事件表示进程已调用空闲任务。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;IdleTaskNotifyComplete&gt;</strong></td>
<td align="left"><p>事件表示处理空闲任务的过程已完成。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;OtherProcessIdleTasksCallsInProgress&gt;</strong></td>
<td align="left"><p>事件表示在后台调用了另一个名为 <strong>ProcessIdleTasks</strong> 的进程。 请注意，Pwrtest 会调用 advapi32.dll 导出的 <strong>ProcessIdleTasks</strong> 函数。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[PwrTest 语法](pwrtest-syntax.md)

 

 






