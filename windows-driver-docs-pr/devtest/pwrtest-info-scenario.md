---
title: PwrTest 信息方案
description: PwrTest Info 方案从各种类别捕获和记录当前系统电源信息。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 678bb94553710bcfb601daf23fa8d703b2f7a742
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823367"
---
# <a name="pwrtest-info-scenario"></a>PwrTest 信息方案


PwrTest Info 方案从各种类别捕获和记录当前系统电源信息。

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>语法


```
pwrtest /info:option [/p:{n|a|*}] [/w:n]  [/?] 
```

<span id="_info_option"></span><span id="_INFO_OPTION"></span>**/info：**<em>选项</em>  

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><em>option</em></th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="all"></span><span id="ALL"></span><strong>一切</strong></p></td>
<td align="left"><p>显示所有系统信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="powercap"></span><span id="POWERCAP"></span><strong>powercap</strong></p></td>
<td align="left"><p>显示 SYSTEM_POWER_CAPABILITIES。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="powerinfo"></span><span id="POWERINFO"></span><strong>powerinfo</strong></p></td>
<td align="left"><p>显示 SYSTEM_POWER_CAPABILITIES。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="battery"></span><span id="BATTERY"></span><strong>电池</strong></p></td>
<td align="left"><p>显示 SYSTEM_BATTERY_STATE。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="ppm"></span><span id="PPM"></span><strong>黑白</strong></p></td>
<td align="left"><p>显示所有处理器信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="ppmidle"></span><span id="PPMIDLE"></span><strong>ppmidle</strong></p></td>
<td align="left"><p>显示处理器空闲状态信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="ppmperf"></span><span id="PPMPERF"></span><strong>ppmperf</strong></p></td>
<td align="left"><p>显示处理器性能状态信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="ppmperfverbose"></span><span id="PPMPERFVERBOSE"></span><strong>ppmperfverbose</strong></p></td>
<td align="left"><p>以详细格式显示处理器性能状态信息。</p></td>
</tr>
</tbody>
</table>

 

<span id="_p_na_"></span><span id="_P_NA_"></span>**/p：**{*n* \| **a** \| **\\** \* }  

为 **/info： ppm/info： ppmidle** 或 **/info： ppmperf** 选项指定逻辑处理器编号。

<span id="a_or__"></span><span id="A_OR__"></span>**或****\\**\*  
指定 (默认) )  (的所有逻辑处理器。

<span id="_w_yn"></span><span id="_W_YN"></span>**/w：**{**y** | **n**}  
指定等待 PPM 断开事件的时间（以秒为单位） (默认值为10秒) 。

**示例**

```
pwrtest /info:all
```

```
  pwrtest /info:battery
```

```
  pwrtest /info:ppm
```

```
  pwrtest /info:ppm /p:1
```

```
 pwrtest /info:ppmidle
```

```
  pwrtest /info:ppmperf /p:2
```

### <a name="span-idxml_log_file_outputspanspan-idxml_log_file_outputspanspan-idxml_log_file_outputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML 日志文件输出

```XML
<PwrTestLog>
  <SystemInformation>
  </SystemInformation>
  <InfoScenario>
    <SYSTEM_POWER_CAPABILITIES> 
      <SystemS1StateSupported></SystemS1StateSupported>
      <SystemS2StateSupported></SystemS2StateSupported>
      <SystemS3StateSupported></SystemS3StateSupported>
      <SystemS4StateSupported></SystemS4StateSupported>
      <SystemS5StateSupported></SystemS5StateSupported>
      <RtcWakeSupported></RtcWakeSupported>
      <FastSystemS4></FastSystemS4>
    </SYSTEM_POWER_CAPABILITIES> 
    <SYSTEM_POWER_INFORMATION> 
      <MaxIdlenessAllowed></MaxIdlenessAllowed>
      <Idleness></Idleness>
      <TimeRemaining></TimeRemaining>
      <CoolingMode></CoolingMode>
    </SYSTEM_POWER_INFORMATION> 
    <SYSTEM_BATTERY_STATE> 
      <AcOnLine></AcOnLine>
      <BatteryPresent></BatteryPresent>
      <Charging></Charging>
      <Discharging></Discharging>
      <MaxCapacity></MaxCapacity>
      <RemainingCapacity></RemainingCapacity>
      <RateOfDrain></RateOfDrain>
      <EstimatedTime></EstimatedTime>
      <DefaultAlert1></DefaultAlert1>
      <DefaultAlert2></DefaultAlert2>
    </SYSTEM_BATTERY_STATE> 
    <PROCESSOR_POWER_INFORMATION> 
      <CPUNumber></CPUNumber>
      <MaxMhz></MaxMhz>
      <CurrentMhz></CurrentMhz>
      <MhzLimit></MhzLimit>
      <MaxIdleState></MaxIdleState>
      <CurrentIdleState></CurrentIdleState>
    </PROCESSOR_POWER_INFORMATION> 
    </InfoScenario>
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
<td align="left"><strong>&lt;InfoScenario&gt;</strong></td>
<td align="left"><p>包含与信息方案相关的信息。 PwrTest 日志文件中只有一个<strong> &lt; InfoScenario &gt; </strong>元素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;SYSTEM_POWER_CAPABILITIES&gt;</strong></td>
<td align="left"><p>包含有关系统电源功能的信息。 将从 SYSTEM_POWER_CAPABILITIES 结构检索此信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;SystemSxStateSupported&gt;</strong></td>
<td align="left"><p>指示系统是否支持给定的系统 ACPI 睡眠状态。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;RtcWakeSupported&gt;</strong></td>
<td align="left"><p>指示支持 RTC 唤醒 (唤醒) 的最小睡眠状态。 值为 SYSTEM_POWER_STATE 枚举。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;FastSystemS4&gt;</strong></td>
<td align="left"><p>指示混合睡眠在系统上是否可用。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;SYSTEM_POWER_INFORMATION&gt;</strong></td>
<td align="left"><p>包含与系统空闲相关的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;MaxIdlenessAllowed&gt;</strong></td>
<td align="left"><p>指示当系统被视为处于空闲状态且空闲超时开始计数时) 的空闲 (（以百分比表示）。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;空闲&gt;</strong></td>
<td align="left"><p>当前空闲级别，以百分比表示。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;TimeRemaining&gt;</strong></td>
<td align="left"><p>指示系统待机空闲计时器中的剩余时间（秒）。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;CoolingMode&gt;</strong></td>
<td align="left"><p>指示当前系统冷却模式： (0) 活动， (1) ，被动， (2) 无效。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;SYSTEM_BATTERY_STATE&gt;</strong></td>
<td align="left"><p>包含与系统电池的当前状态相关的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;AcOnLine&gt;</strong></td>
<td align="left"><p>指示系统当前是否正在进行 AC 电源。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;BatteryPresent&gt;</strong></td>
<td align="left"><p>指示系统中是否至少有一个电池。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;收取&gt;</strong></td>
<td align="left"><p>指示是否至少有一个电池正在充电。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;放电&gt;</strong></td>
<td align="left"><p>指示是否至少有一个电池当前正在放电。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;MaxCapacity&gt;</strong></td>
<td align="left"><p>新时的电池最大容量，以毫瓦 mw-h 小时 (mW-h) 。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;RemainingCapacity&gt;</strong></td>
<td align="left"><p>电池的预计剩余容量 (mW-h) ，以毫瓦 mw-h 小时为单位。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;RateOfDrain&gt;</strong></td>
<td align="left"><p>指示毫瓦 (mW) 中电池的当前放电速率。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;EstimatedTime&gt;</strong></td>
<td align="left"><p>电池剩余时间（秒）。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;DefaultAlert1&gt;</strong></td>
<td align="left"><p>指示在出现电池电量不足警报时电池制造商建议的容量。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;DefaultAlert2&gt;</strong></td>
<td align="left"><p>指示出现警告电池警报时电池制造商建议的容量。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;PROCESSOR_POWER_INFORMATION&gt;</strong></td>
<td align="left"><p>包含有关系统处理器及其电源管理功能的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;CPUNumber&gt;</strong></td>
<td align="left"><p>指示当前 &lt; PROCESSOR_POWER_INFORMATION &gt; 元素描述的处理器。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;MaxMhz&gt;</strong></td>
<td align="left"><p>指示处理器的最大频率。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;CurrentMhz&gt;</strong></td>
<td align="left"><p>指示处理器的当前频率。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;MhzLimit&gt;</strong></td>
<td align="left"><p>指示处理器时钟频率的当前限制。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;MaxIdleState&gt;</strong></td>
<td align="left"><p>指示处理器的最大空闲状态。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;CurrentIdleState&gt;</strong></td>
<td align="left"><p>指示处理器的当前空闲状态。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[PwrTest 语法](pwrtest-syntax.md)

 

 






