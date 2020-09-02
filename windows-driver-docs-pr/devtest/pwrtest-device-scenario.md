---
title: PwrTest 设备方案
description: PwrTest 设备方案监视设备空闲统计信息。
ms.assetid: 75C53B6E-3D1F-4E9D-A99E-3060A9CC37BC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bbbb52f427722680c1936ee270b3901b55a21a7d
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382969"
---
# <a name="pwrtest-device-scenario"></a>PwrTest 设备方案


PwrTest 设备方案监视设备空闲统计信息。

此方案主要用于 Windows 7 设备电源活动，后续版本的 Windows 使用不同的机制来跟踪目前不受 Pwrtest 支持的设备空闲。 对于比 Windows 7 更新的 Windows 版本，请使用 [Windows 性能工具包 (WPT) ](/windows-hardware/test/wpt/windows-performance-toolkit-technical-reference)。 WPT 包括 Windows 性能记录器 (") ，可用于跟踪内核模式电源提供程序和 Windows 性能分析器 (WPA) ，该程序可显示 power framework (PoFx) 设备统计信息，并可以在以后图形转换。

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>语法


```
pwrtest /device  [/t:n] [/?] 
```

<span id="_t_n"></span><span id="_T_N"></span>**/t：**<em>n</em>  
指定运行该方案 (默认 *值为 30* 分钟) )  (的总时间（分钟）。

**示例**

```
pwrtest /device /t:60
```

```
pwrtest /device
```

### <a name="span-idxml_log_file_outputspanspan-idxml_log_file_outputspanspan-idxml_log_file_outputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML 日志文件输出

```XML
<PwrTestLog>
  <SystemInformation>
  </SystemInformation>
  <DeviceIdleEvents> 
    <DeviceIdleChangeEvent>
        <Timestamp></TimeStamp>
        <InstancePath></InstancePath>
        <Description></Description>
    </DeviceIdleChangeEvent>
    <DeviceIdleEvent>
        <Timestamp></TimeStamp>
        <InstancePath></InstancePath>
        <Device></Device>
        <Pdo></Pdo>
        <ConservationTimeout></ConservationTimeout>
        <PerformanceTimeout></PerformanceTimeout>
        <AccruedIdleTime></AccruedIdleTime>
        <BusyCount></BusyCount>
        <AccruedBusyCount></AccruedBusyCount>
        <IdlePowerState></IdlePowerState>
        <CurrentPowerState></CurrentPowerState>
        <Analysis></Analysis>
    </DeviceIdleEvent>
  </DeviceIdleEvents>
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
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>&lt;DeviceIdleEvents&gt;</strong></td>
<td align="left"><p>包含所有不同的设备空闲事件。 每个 PwrTest 日志文件只能有一个<strong> &lt; DeviceIdleEvents</strong>元素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;时间戳&gt;</strong></td>
<td align="left"><p>任何给定事件的时间戳。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;InstancePath&gt;</strong></td>
<td align="left"><p>设备实例路径。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;DeviceIdleChangeEvent&gt;</strong></td>
<td align="left"><p>设备添加或删除事件。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;说明&gt;</strong></td>
<td align="left"><p>DeviceRemoved 或 DeviceDetected。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;DeviceIdleEvent&gt;</strong></td>
<td align="left"><p>Device idle statistics 事件。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;设备&gt;</strong></td>
<td align="left"><p>功能设备对象。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;Pdo&gt;</strong></td>
<td align="left"><p>物理设备对象</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;ConservationTimeout&gt;</strong></td>
<td align="left"><p>保守超时 (通常在 DC power) 上使用。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;PerformanceTimeout&gt;</strong></td>
<td align="left"><p>性能超时 (通常在 AC power) 上使用。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;AccruedIdleTime&gt;</strong></td>
<td align="left"><p>期间内的空闲时间。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;BusyCount&gt;</strong></td>
<td align="left"><p>一段时间内设备驱动程序调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer" data-raw-source="[&lt;strong&gt;PoSetDeviceBusy&lt;/strong&gt;](../kernel/mm-bad-pointer.md)"><strong>PoSetDeviceBusy</strong></a> 的次数。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;AccruedBusyCount&gt;</strong></td>
<td align="left"><p>设备驱动程序调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer" data-raw-source="[&lt;strong&gt;PoSetDeviceBusy&lt;/strong&gt;](../kernel/mm-bad-pointer.md)"><strong>PoSetDeviceBusy</strong></a>的总次数。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;IdlePowerState&gt;</strong></td>
<td align="left"><p>显示处于空闲状态的数字状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;CurrentPowerState&gt;</strong></td>
<td align="left"><p>当前数字的电源状态。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;分析&gt;</strong></td>
<td align="left"><p>描述期间发生的情况的字符串。</p></td>
</tr>
</tbody>
</table>



## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[PwrTest 语法](pwrtest-syntax.md)