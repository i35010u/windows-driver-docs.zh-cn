---
title: PwrTest 空闲方案
description: PwrTest 空闲方案监视用户和 CPU 空闲统计信息显示空闲内核每隔 15 秒收集的统计信息。
ms.assetid: 7E40DD91-D236-41B3-BC3A-DEB6DDD76139
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2d7606d97a1bb410b7920b26e1b485193e08985
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561455"
---
# <a name="pwrtest-idle-scenario"></a>PwrTest 空闲方案


PwrTest 空闲方案监视用户和 CPU 空闲统计信息显示空闲内核每隔 15 秒收集的统计信息。

你可以组合使用这种情况下[PwrTest 执行状态的情况](pwrtest-execution-state-scenario.md)(**/es**) 同时监视旧的执行状态更改，它可帮助你诊断系统到不空闲的原因进入睡眠状态。

**请注意**  这是旧方案，其建议的更换过程已[PwrTest PPM 方案](pwrtest-ppm-scenario.md)(**/ppm**) 用于监视 CPU 空闲统计信息和[PwrTest 监视器方案](pwrtest-monitor-scenario.md)(**/监视**) 用于监视用户空闲。

 

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>语法


```
pwrtest /idle  [/t:n] [/?] [/es [es_options]
```

<span id="_t_n"></span><span id="_T_N"></span>**/t:**<em>n</em>  
为方案运行指定的总时间 （以分钟为单位） (默认值*n*为 30 分钟)。

<span id="_es___es_options_"></span><span id="_ES___ES_OPTIONS_"></span>**/es \[**  <em>es\_选项</em>**\]**  
运行[PwrTest 执行状态 (ES) 方案](pwrtest-execution-state-scenario.md)。

**示例**

```
pwrtest /idle /t:60
```

```
pwrtest /idle /es /user
```

```
pwrtest /idle /es /kernel
```

### <a name="span-idxmllogfileoutputspanspan-idxmllogfileoutputspanspan-idxmllogfileoutputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML 日志文件输出

```XML
<PwrTestLog>
  <SystemInformation>
  </SystemInformation>
  <PowerIdleStatistics> 
    <IdleStats> 
      <Time></Time>
      <Threshold></Threshold>
      <LowestIdleness></LowestIdleness>
      <AverageIdleness></AverageIdleness>
      <AccruedIdleTime></AccruedIdleTime>
      <NonIdleIgnored></NonIdleIgnored>
      <IdleToSleep></IdleToSleep>
      <NonIdleReferences></NonIdleReferences>
    </IdleStats>
    <EsChange> 
      <Time>XX:XX:XX</Time>
      <Process></Process>
        <RawState></RawState>
        <Continuous></Continuous>
        <System></System>
        <Display></Display>
        <AwayMode></AwayMode>
    </EsChange> 
  </PowerIdleStatistics>
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
<td align="left"><strong>&lt;PowerIdleStatistics&gt;</strong></td>
<td align="left"><p>包含与空闲方案方案相关的信息。 只有一个<strong>&lt;PowerIdleStatistics&gt;</strong>元素可以出现在 PwrTest 日志文件中。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;IdleStats&gt;</strong></td>
<td align="left"><p>包含最后一个空闲周期的空闲统计的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;时间&gt;</strong></td>
<td align="left"><p>最新的空闲状态的统计信息事件的时间。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;阈值&gt;</strong></td>
<td align="left"><p>空闲忽略阈值。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;LowestIdleness&gt;</strong></td>
<td align="left"><p>时间段内的最小空闲时间百分比。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;AverageIdleness&gt;</strong></td>
<td align="left"><p>时间段内的平均空闲时间百分比。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;AccruedIdleTime&gt;</strong></td>
<td align="left"><p>时间段内的应计空闲时间。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;NonIdleIgnored&gt;</strong></td>
<td align="left"><p>已忽略时间段内的非空闲时间。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;IdleToSleep&gt;</strong></td>
<td align="left"><p>未在系统空闲时间段内进入睡眠状态？</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;NonIdleReferences&gt;</strong></td>
<td align="left"><p>非空闲的时间段内忽略引用。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;EsChange&gt;</strong></td>
<td align="left"><p>包含单个线程执行状态更改事件相关信息。 将一个<strong>&lt;EsChange&gt;</strong> PwrTest 日志文件中记录为每个线程执行状态更改事件的元素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;时间&gt;</strong></td>
<td align="left"><p>指示执行状态更改事件发生时的时间。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;Process&gt;</strong></td>
<td align="left"><p>指示请求的执行状态更改的进程的图像文件的路径。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;RawState&gt;</strong></td>
<td align="left"><p>指示请求执行状态。 这是类型 EXECUTION_STATE 的 32 位值 （请参阅 Windows.h）。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;Continuous&gt;</strong></td>
<td align="left"><p>如果进程请求执行状态更改或不是连续 (ES_CONTINUOUS) (TRUE) 指示 (FALSE)。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;System&gt;</strong></td>
<td align="left"><p>如果在过程请求或不是可用 (ES_SYSTEM_REQUIRED) 系统 (TRUE) 指示 (FALSE)。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;显示&gt;</strong></td>
<td align="left"><p>如果在过程请求显示为可用 (ES_DISPLAY_REQUIRED)，或不 (TRUE) 指示 (FALSE)。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;AwayMode&gt;</strong></td>
<td align="left"><p>如果为过程请求离开模式或未启用 (ES_AWAYMODE_REQUIRED) (TRUE) 指示 (FALSE)。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[PwrTest 语法](pwrtest-syntax.md)

 

 






