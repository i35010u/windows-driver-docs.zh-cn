---
title: PwrTest 空闲方案
description: PwrTest Idle 方案监视用户和 CPU 空闲统计信息，显示内核每15秒收集的空闲统计信息。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5839090d82f3aa4bdab03ef5483d8d7b8d9d6e1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787625"
---
# <a name="pwrtest-idle-scenario"></a>PwrTest 空闲方案


PwrTest Idle 方案监视用户和 CPU 空闲统计信息，显示内核每15秒收集的空闲统计信息。

你可以将此方案与 [PwrTest 执行状态方案](pwrtest-execution-state-scenario.md) 组合 (**/es**) ，同时监视旧的执行状态更改，这有助于诊断系统不会置于空闲状态为睡眠状态的原因。

**注意**  这是一种旧方案，其建议的替换是 [PWRTEST PPM 方案](pwrtest-ppm-scenario.md) (**/ppm**) 用于监视 CPU 空闲统计信息，而 [PwrTest 监视器方案](pwrtest-monitor-scenario.md) 则用于监视用户空闲情况 (**/monitor**) 。

 

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>语法


```
pwrtest /idle  [/t:n] [/?] [/es [es_options]
```

<span id="_t_n"></span><span id="_T_N"></span>**/t：**<em>n</em>  
指定运行该方案 (默认 *值为 30* 分钟) )  (的总时间（分钟）。

<span id="_es___es_options_"></span><span id="_ES___ES_OPTIONS_"></span>**/es \[**<em>es \_ 选项</em>**\]**  
[ (ES) 方案中运行 PwrTest 执行状态](pwrtest-execution-state-scenario.md)。

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

### <a name="span-idxml_log_file_outputspanspan-idxml_log_file_outputspanspan-idxml_log_file_outputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML 日志文件输出

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
<td align="left"><strong>&lt;PowerIdleStatistics&gt;</strong></td>
<td align="left"><p>包含与空闲方案方案有关的信息。 PwrTest 日志文件中只能出现一个<strong> &lt; PowerIdleStatistics &gt; </strong>元素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;IdleStats&gt;</strong></td>
<td align="left"><p>包含上一个空闲时间段的空闲统计信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;时间&gt;</strong></td>
<td align="left"><p>最近空闲统计信息事件的时间。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;阈值&gt;</strong></td>
<td align="left"><p>空闲忽略阈值。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;LowestIdleness&gt;</strong></td>
<td align="left"><p>时间段内的最低空闲百分比。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;AverageIdleness&gt;</strong></td>
<td align="left"><p>期间中的平均空闲百分比。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;AccruedIdleTime&gt;</strong></td>
<td align="left"><p>时间段内的累计空闲时间。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;NonIdleIgnored&gt;</strong></td>
<td align="left"><p>在该时间段内被忽略的非空闲时间。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;IdleToSleep&gt;</strong></td>
<td align="left"><p>系统在一段时间内是否处于空闲状态？</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;NonIdleReferences&gt;</strong></td>
<td align="left"><p>期间内的非空闲忽略引用量。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;EsChange&gt;</strong></td>
<td align="left"><p>包含与单个线程执行状态更改事件相关的信息。 PwrTest 日志文件中记录的每个线程执行状态更改事件都将有一个<strong> &lt; EsChange &gt; </strong>元素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;时间&gt;</strong></td>
<td align="left"><p>指示执行状态更改事件发生的时间。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;正在&gt;</strong></td>
<td align="left"><p>指示请求执行状态更改的进程的映像文件的路径。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;RawState&gt;</strong></td>
<td align="left"><p>指示请求执行状态。 这是 EXECUTION_STATE (类型的32位值，请参阅 Windows) 。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;持续&gt;</strong></td>
<td align="left"><p>指示 (TRUE) 如果进程请求的执行状态更改为连续 (ES_CONTINUOUS) 或不 (FALSE) 。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;系统&gt;</strong></td>
<td align="left"><p>指示 () 如果进程请求提供系统 (ES_SYSTEM_REQUIRED)  (FALSE) 。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;显示&gt;</strong></td>
<td align="left"><p>指示 (TRUE) 如果该进程已请求显示可用 (ES_DISPLAY_REQUIRED) 或 (FALSE) 错误。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;AwayMode&gt;</strong></td>
<td align="left"><p>指示 (TRUE) 如果已 (ES_AWAYMODE_REQUIRED) ，则 () FALSE。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[PwrTest 语法](pwrtest-syntax.md)

 

 






