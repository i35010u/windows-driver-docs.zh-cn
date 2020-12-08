---
title: PwrTest 电池方案
description: PwrTest 电池方案旨在促进自动检查电池和电源源信息。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39dbe8880e59f59a057f37ddb25e086c0652bf0f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805719"
---
# <a name="pwrtest-battery-scenario"></a>PwrTest 电池方案


PwrTest 电池方案旨在促进自动检查电池和电源源信息。

PwrTest 可以记录电池容量、电压、排出速率以及系统中任意数量的电池的一般状态。 以指定的时间间隔按指定的时间间隔记录电池数据。

### <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>语法

```
pwrtest /battery [/c:n] [/i:n] [/?] 
```

<span id="_c_n"></span><span id="_C_N"></span>**/c：**<em>n</em>  
指定要运行的默认)  (100 的周期数。

<span id="_i_n"></span><span id="_I_N"></span>**/i：**<em>n</em>  
指定默认 (为 5000) 的轮询间隔（以毫秒为单位）。

**示例**

```
pwrtest /battery 
```

```
pwrtest /battery /c:4 /i:1000
```

### <a name="span-idxml_log_file_outputspanspan-idxml_log_file_outputspanspan-idxml_log_file_outputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML 日志文件输出

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
<td align="left"><strong>&lt;UniqueID&gt;</strong></td>
<td align="left"><p>指示电池的唯一 ID。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;化学&gt;</strong></td>
<td align="left"><p>指示电池化学。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;提供&gt;</strong></td>
<td align="left"><p>指示电池制造商。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;DesignedCapacity&gt;</strong></td>
<td align="left"><p>表示在毫瓦 mw-h 小时 (mW-h) 设计的电池容量。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;FullChargeCapacity&gt;</strong></td>
<td align="left"><p>指示 (mW-h) ，以毫瓦 mw-h 小时表示的电池完全充电容量。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;CriticalBias&gt;</strong></td>
<td align="left"><p>指示从零开始的偏移，以 mW-h 表示，适用于电池报告。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;CycleCount&gt;</strong></td>
<td align="left"><p>指示电池所经历的充电/放电周期数。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ManufactureDate&gt;</strong></td>
<td align="left"><p>指示电池的制造日期。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;FullLifeTime&gt;</strong></td>
<td align="left"><p>指示电池的全速使用时间（秒）。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;BatteryTraces&gt;</strong></td>
<td align="left"><p>包含<strong> &lt; 跟踪 &gt; </strong>元素的列表。 具有一个指示电池信息轮询间隔的属性。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;跟踪&gt;</strong></td>
<td align="left"><p>包含有关电池状态的信息，例如给定间隔内的电压、容量和排出速率。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ElapsedT&gt;</strong></td>
<td align="left"><p>指示自启动 PwrTest 以来经过的时间</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;ACStatus&gt;</strong></td>
<td align="left"><p>指示系统是在 AC (1) 还是电池 (0) 电源上运行。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;TimeRemaining&gt;</strong></td>
<td align="left"><p>指示所有系统电池的电池寿命（以秒为单位）。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;功能&gt;</strong></td>
<td align="left"><p>指示电池的容量 (mW-h) ，以毫瓦 mw-h 小时为单位。 具有一个 id 属性，用于指示要报告容量的电池。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;RateOfDrain&gt;</strong></td>
<td align="left"><p>指示毫瓦 (mW) 电池的电量消耗率。 具有一个 ID 属性，用于指示报告排出电量的电池。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;电压&gt;</strong></td>
<td align="left"><p>指示以毫伏 (mV) 的电池电压。 具有一个 ID 属性，用于指示报告电压的电池。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[PwrTest 语法](pwrtest-syntax.md)

 

 






