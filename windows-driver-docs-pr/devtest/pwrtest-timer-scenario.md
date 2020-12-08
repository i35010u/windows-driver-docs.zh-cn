---
title: PwrTest 计时器方案
description: PwrTest Timer 方案记录系统计时器解析更改发生的情况。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a98e90e1f6c212efcc028f6f43634eb307f5e8cd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837315"
---
# <a name="pwrtest-timer-scenario"></a>PwrTest 计时器方案


PwrTest Timer 方案记录系统计时器解析更改发生的情况。

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>语法


```
pwrtest /timer /?  [/t:n]  [/?] 
```

<span id="_t_n"></span><span id="_T_N"></span>**/t：**<em>n</em>  
指定运行该方案 (默认 *值为 30* 分钟) )  (的总时间（分钟）。

**示例**

```
  pwrtest /timer
```

```
pwrtest /timer /t:5
```

### <a name="span-idxml_log_file_outputspanspan-idxml_log_file_outputspanspan-idxml_log_file_outputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML 日志文件输出

```XML
<PwrTestLog>
  <SystemInformation>
  </SystemInformation>
  <TimerEvents> 
    <TimerResolutionRundown>
      <Timestamp></Timestamp>
      <CurrentResolution></CurrentResolution>
      <MinimumResolution></MinimumResolution>
      <MaximumResolution></MaximumResolution>
      <KernelCount></KernelCount>
      <KernelResolution></KernelResolution>
    </TimerResolutionRundown>
    <TimerResolutionRequestRundown>
        <Timestamp></Timestamp>
        <AppName></AppName>
        <Resolution></Resolution>
        <ProcessID></ProcessID>
    </TimerResolutionRequestRundown>
    <NtSetTimerResolution>
      <Timestamp></Timestamp>
      <AppName></AppName>
      <ServiceName></ServiceName>
      <Resolution></Resolution>
      <ProcessID></ProcessID>
    </NtSetTimerResolution>
    <UpdateTimerResolution>
      <Timestamp></Timestamp>
      <Resolution></Resolution>
    </UpdateTimerResolution>
    <ExSetTimerResolution>
      <Timestamp></Timestamp>
      <Resolution></Resolution>
    </ExSetTimerResolution>  
  </TimerEvents>
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
<td align="left"><strong>&lt;TimerEvents&gt;</strong></td>
<td align="left"><p>包含所有不同的计时器事件。 PwrTest 日志文件中只能出现一个<strong> &lt; TimerEvents &gt; </strong>元素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;标志&gt;</strong></td>
<td align="left"><p>任何给定事件的时间戳。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;TimerResolutionRundown&gt;</strong></td>
<td align="left"><p>用于显示当前计时器分辨率统计信息的事件。 将仅记录这些事件中的一个。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;CurrentResolution&gt;</strong></td>
<td align="left"><p>当前分辨率（以毫秒为单位）。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;MinimumResolution&gt;</strong></td>
<td align="left"><p>最小分辨率。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;MaximumResolution&gt;</strong></td>
<td align="left"><p>最大分辨率。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;KernelCount&gt;</strong></td>
<td align="left"><p>内核模式下的解析请求数。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;KernelResolution&gt;</strong></td>
<td align="left"><p>当前内核计时器分辨率。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;TimerResolutionRequestRundown&gt;</strong></td>
<td align="left"><p>用于显示当前解析请求的事件。 可能会记录多个事件。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;AppName&gt;</strong></td>
<td align="left"><p>请求者的进程名称。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;解决方法&gt;</strong></td>
<td align="left"><p>请求的解析（以毫秒为单位）。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ProcessID&gt;</strong></td>
<td align="left"><p>请求者的进程 ID。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;NtSetTimerResolution&gt;</strong></td>
<td align="left"><p>事件表示发出计时器解析请求的进程。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ServiceName&gt;</strong></td>
<td align="left"><p>请求者的服务名称（如果适用）。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;UpdateTimerResolution&gt;</strong></td>
<td align="left"><p>事件指示系统已更新计时器分辨率。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ExSetTimerResolution&gt;</strong></td>
<td align="left"><p>事件表示内核组件发出计时器解析请求。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[PwrTest 语法](pwrtest-syntax.md)

 

 






