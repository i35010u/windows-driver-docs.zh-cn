---
title: PwrTest 信息方案
description: PwrTest 信息方案捕获和记录从各种类别的当前系统电源信息。
ms.assetid: 1d13d1dd-eb8d-434a-b994-e747a86f3457
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70d3d0534fe905a83648c6101631bab55169f347
ms.sourcegitcommit: 179f9119b6c7888ea18281f6d5d11d62ac45b58d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/22/2019
ms.locfileid: "66035119"
---
# <a name="pwrtest-info-scenario"></a>PwrTest 信息方案


PwrTest 信息方案捕获和记录从各种类别的当前系统电源信息。

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>语法


```
pwrtest /info:option [/p:{n|a|*}] [/w:n]  [/?] 
```

<span id="_info_option"></span><span id="_INFO_OPTION"></span>**/info:**<em>option</em>  

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
<td align="left"><p><span id="all"></span><span id="ALL"></span><strong>all</strong></p></td>
<td align="left"><p>显示所有的系统信息。</p></td>
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
<td align="left"><p><span id="battery"></span><span id="BATTERY"></span><strong>battery</strong></p></td>
<td align="left"><p>显示 SYSTEM_BATTERY_STATE。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="ppm"></span><span id="PPM"></span><strong>ppm</strong></p></td>
<td align="left"><p>显示所有处理器信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="ppmidle"></span><span id="PPMIDLE"></span><strong>ppmidle</strong></p></td>
<td align="left"><p>显示处理器空闲状态的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="ppmperf"></span><span id="PPMPERF"></span><strong>ppmperf</strong></p></td>
<td align="left"><p>显示处理器性能状态信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="ppmperfverbose"></span><span id="PPMPERFVERBOSE"></span><strong>ppmperfverbose</strong></p></td>
<td align="left"><p>显示详细格式中的处理器性能状态信息。</p></td>
</tr>
</tbody>
</table>

 

<span id="_p_na_"></span><span id="_P_NA_"></span>**/p:**{*n*\|**a**\|**\\**\*}  

指定的逻辑处理器编号 **/info:ppm / info: ppmidle**，或 **/info:ppmperf**选项。

<span id="a_or__"></span><span id="A_OR__"></span>或 **\\**\*  
指定所有逻辑处理器 （默认值）。

<span id="_w_yn"></span><span id="_W_YN"></span>**/w:**{**y**|**n**}  
在数秒内等待 PPM 断开事件指定的时间 （默认值为 10 秒）。

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

### <a name="span-idxmllogfileoutputspanspan-idxmllogfileoutputspanspan-idxmllogfileoutputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML 日志文件输出

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
<td align="left"><strong>&lt;InfoScenario&gt;</strong></td>
<td align="left"><p>包含有关信息方案的相关信息。 只有一个<strong>&lt;InfoScenario&gt;</strong> PwrTest 日志文件中的元素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;SYSTEM_POWER_CAPABILITIES&gt;</strong></td>
<td align="left"><p>包含与系统电源功能相关的信息。 从 SYSTEM_POWER_CAPABILITIES 结构检索此信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;SystemSxStateSupported&gt;</strong></td>
<td align="left"><p>指示在系统上是否支持给定的系统 ACPI 睡眠状态。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;RtcWakeSupported&gt;</strong></td>
<td align="left"><p>指示其中 RTC 唤醒 （计时器唤醒） 受支持的最低睡眠状态。 的值为 SYSTEM_POWER_STATE 枚举。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;FastSystemS4&gt;</strong></td>
<td align="left"><p>指示是否在系统上可用混合睡眠。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;SYSTEM_POWER_INFORMATION&gt;</strong></td>
<td align="left"><p>包含与系统的空闲时间相关的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;MaxIdlenessAllowed&gt;</strong></td>
<td align="left"><p>指示空闲时间 （以百分比表示） 时系统被视为空闲和空闲超时开始计数。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;空闲时间&gt;</strong></td>
<td align="left"><p>当前空闲级别，以百分比表示。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;TimeRemaining&gt;</strong></td>
<td align="left"><p>指示在系统待机空闲计时器，以秒为单位的剩余时间。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;CoolingMode&gt;</strong></td>
<td align="left"><p>指示当前系统冷却模式：(0) 的活动状态，(1)，被动，（2） 无效。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;SYSTEM_BATTERY_STATE&gt;</strong></td>
<td align="left"><p>包含与系统电池的当前状态相关的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;AcOnLine&gt;</strong></td>
<td align="left"><p>指示系统是否正在运行交流电源。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;BatteryPresent&gt;</strong></td>
<td align="left"><p>指示是否在系统中存在至少一个电池。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;收费&gt;</strong></td>
<td align="left"><p>指示是否至少一个电池当前正在充电。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;放电&gt;</strong></td>
<td align="left"><p>指示是否至少一个电池当前正在放电。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;MaxCapacity&gt;</strong></td>
<td align="left"><p>电池时，毫瓦时小时 (mW-h) 中的新增的最大容量。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;RemainingCapacity&gt;</strong></td>
<td align="left"><p>估计毫瓦时小时 (mW-h) 中的电池的剩余容量。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;RateOfDrain&gt;</strong></td>
<td align="left"><p>指示的毫瓦 (mW) 上的电池放电装置的当前速率。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;EstimatedTime&gt;</strong></td>
<td align="left"><p>估计剩余电池供电，以秒为单位的时间。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;DefaultAlert1&gt;</strong></td>
<td align="left"><p>指示电池制造商的建议的容量时应发生电池电量不足警告。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;DefaultAlert2&gt;</strong></td>
<td align="left"><p>指示电池制造商的建议的容量时应发生警告电池警报。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;PROCESSOR_POWER_INFORMATION&gt;</strong></td>
<td align="left"><p>包含与系统处理器和其电源管理功能相关的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;CPUNumber&gt;</strong></td>
<td align="left"><p>指示当前在哪个处理器&lt;PROCESSOR_POWER_INFORMATION&gt;描述元素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;MaxMhz&gt;</strong></td>
<td align="left"><p>指示处理器的最大频率。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;CurrentMhz&gt;</strong></td>
<td align="left"><p>指示当前处理器的频率。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;MhzLimit&gt;</strong></td>
<td align="left"><p>指示处理器的时钟频率的当前限制。</p></td>
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

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[PwrTest 语法](pwrtest-syntax.md)

 

 






