---
title: PwrTest 电池方案
description: PwrTest 电池方案旨在促进自动的检查电池和电源源信息。
ms.assetid: e0bad871-a826-4951-9a84-93c9b1aa0653
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37c7323d6b3ff4a5cb1b299ebc0acade9cd1707f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523136"
---
# <a name="pwrtest-battery-scenario"></a>PwrTest 电池方案


PwrTest 电池方案旨在促进自动的检查电池和电源源信息。

PwrTest 是能够记录电池容量、 电压、 排出、 和任意多个电池，如系统中的常规状态的速率。 电池数据按指定时间间隔记录指定的周期数。

### <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>语法

```
pwrtest /battery [/c:n] [/i:n] [/?] 
```

<span id="_c_n"></span><span id="_C_N"></span>**/c:**<em>n</em>  
指定了多少个周期 （100 是默认值） 运行。

<span id="_i_n"></span><span id="_I_N"></span>**/i:**<em>n</em>  
指定轮询间隔 （毫秒） （默认值为 5000）。

**示例**

```
pwrtest /battery 
```

```
pwrtest /battery /c:4 /i:1000
```

### <a name="span-idxmllogfileoutputspanspan-idxmllogfileoutputspanspan-idxmllogfileoutputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML 日志文件输出

```XML
<PwrTestLog>
  <SystemInformation>
  </SystemInformation>
  <BatteryScenario>
    <Batteries>
      <Battery id="" shortterm="" rechargable="" >
        <Name></Name>
        <UniqueID></UniqueID>
        <Chemistry></Chemistry>
        <Manufacturer></Manufacturer>
        <DesignedCapacity></DesignedCapacity>
        <FullChargeCapacity></FullChargeCapacity>
        <CriticalBias></CriticalBias>
        <CycleCount></CycleCount>
        <ManufactureDate></ManufactureDate>
        <FullLifeTime Units=""></FullLifeTime>
      </Battery> 
    </Batteries>
    <BatteryTraces interval="">
      <Trace>
        <ElapsedT></ElapsedT>
        <ACStatus></ACStatus>
        <Capacity id=""></Capacity>
        <TimeRemaining></TimeRemaining>
        <Capacity id=""></Capacity>
        <RateOfDrain id=””></RateOfDrain>
        <Voltage id=””></Voltage>
        <Capacity id=""></Capacity>
        <RateOfDrain id=””></RateOfDrain>
        <Voltage id=””> </Voltage>
      </Trace>
    </BatteryTraces> 
  </BatteryScenario>
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
<td align="left"><strong>&lt;UniqueID&gt;</strong></td>
<td align="left"><p>指示电池的唯一 ID。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;Chemistry&gt;</strong></td>
<td align="left"><p>指示电池化学。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;制造商&gt;</strong></td>
<td align="left"><p>指示电池制造商联系。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;DesignedCapacity&gt;</strong></td>
<td align="left"><p>以小时为毫瓦时单位 (mW-h) 指示电池的设计的容量。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;FullChargeCapacity&gt;</strong></td>
<td align="left"><p>指示在毫瓦时小时 (mW-h) 中的电池完全充电的容量。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;CriticalBias&gt;</strong></td>
<td align="left"><p>指示从零开始，在 mW-h，应用于电池 reporting 偏差。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;CycleCount&gt;</strong></td>
<td align="left"><p>指示电池电量/放电周期数。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ManufactureDate&gt;</strong></td>
<td align="left"><p>指示电池的制造日期。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;FullLifeTime&gt;</strong></td>
<td align="left"><p>指示以秒为单位的电池完全生存时间。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;BatteryTraces&gt;</strong></td>
<td align="left"><p>包含一系列<strong>&lt;跟踪&gt;</strong>元素。 具有一个属性，该值指示电池信息轮询间隔。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;Trace&gt;</strong></td>
<td align="left"><p>包含有关电池状态，如电压、 容量和消耗率的给定间隔的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ElapsedT&gt;</strong></td>
<td align="left"><p>自启动 PwrTest 指明的持续时间</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;ACStatus&gt;</strong></td>
<td align="left"><p>指示是否 AC (1) 或电量 (0) 上运行系统。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;TimeRemaining&gt;</strong></td>
<td align="left"><p>指示以秒为单位的所有系统电池，剩余的电池生存时间。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;容量&gt;</strong></td>
<td align="left"><p>以小时为毫瓦时单位 (mW-h) 指示电池容量。 具有 id 属性以指示正在为其报告的容量的电池。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;RateOfDrain&gt;</strong></td>
<td align="left"><p>表示为毫瓦 (mW) 上的电池消耗的速率。 具有 ID 属性以指示用于报告的流失率，则的电池。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;电压&gt;</strong></td>
<td align="left"><p>指示电池电压毫伏表示 (mV) 中。 具有 ID 属性以指示电压报告的电池。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[PwrTest 语法](pwrtest-syntax.md)

 

 






