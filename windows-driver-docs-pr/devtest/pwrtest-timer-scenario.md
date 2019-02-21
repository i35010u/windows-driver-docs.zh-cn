---
title: PwrTest 计时器方案
description: PwrTest 计时器方案记录系统计时器分辨率更改发生时。
ms.assetid: 842A827F-8046-4A31-938B-B1EA2119421A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a051682ae6582f6d3a91bffdafd85772848dc196
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524685"
---
# <a name="pwrtest-timer-scenario"></a>PwrTest 计时器方案


PwrTest 计时器方案记录系统计时器分辨率更改发生时。

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>语法


```
pwrtest /timer /?  [/t:n]  [/?] 
```

<span id="_t_n"></span><span id="_T_N"></span>**/t:**<em>n</em>  
为方案运行指定的总时间 （以分钟为单位） (默认值*n*为 30 分钟)。

**示例**

```
  pwrtest /timer
```

```
pwrtest /timer /t:5
```

### <a name="span-idxmllogfileoutputspanspan-idxmllogfileoutputspanspan-idxmllogfileoutputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML 日志文件输出

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
<td align="left"><strong>&lt;TimerEvents&gt;</strong></td>
<td align="left"><p>包含所有不同的计时器事件。 只有一个<strong>&lt;TimerEvents&gt;</strong>元素可以出现在 PwrTest 日志文件中。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;时间戳&gt;</strong></td>
<td align="left"><p>任何给定事件的时间戳。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;TimerResolutionRundown&gt;</strong></td>
<td align="left"><p>事件显示当前计时器分辨率统计信息。 将记录这些事件中的只有一个。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;CurrentResolution&gt;</strong></td>
<td align="left"><p>以毫秒为单位的当前分辨率。</p></td>
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
<td align="left"><p>从内核模式的解析请求数。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;KernelResolution&gt;</strong></td>
<td align="left"><p>当前内核计时器分辨率。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;TimerResolutionRequestRundown&gt;</strong></td>
<td align="left"><p>若要显示当前的解析请求的事件。 多个事件可能会记录。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;AppName&gt;</strong></td>
<td align="left"><p>请求者的进程名称。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;解决方法&gt;</strong></td>
<td align="left"><p>以毫秒为单位的请求的解决方法。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ProcessID&gt;</strong></td>
<td align="left"><p>请求者的进程 ID。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;NtSetTimerResolution&gt;</strong></td>
<td align="left"><p>事件指示进程所做的计时器分辨率请求。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ServiceName&gt;</strong></td>
<td align="left"><p>如果适用的请求者的服务名称。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;UpdateTimerResolution&gt;</strong></td>
<td align="left"><p>事件表示系统已更新计时器分辨率。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ExSetTimerResolution&gt;</strong></td>
<td align="left"><p>事件表示所做的内核组件计时器解析请求。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[PwrTest 语法](pwrtest-syntax.md)

 

 






