---
title: PwrTest 设备方案
description: PwrTest 设备方案监视设备空闲统计信息。
ms.assetid: 75C53B6E-3D1F-4E9D-A99E-3060A9CC37BC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 043c1ee4dc230dd9c075e48356cc15a4c391d64c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345789"
---
# <a name="pwrtest-device-scenario"></a>PwrTest 设备方案


PwrTest 设备方案监视设备空闲统计信息。

此方案主要用于 Windows 7 设备电源活动，后续版本的 Windows 用于跟踪设备空闲的 Pwrtest 目前不支持使用不同的机制。 对于 Windows 7 比更高版本的 Windows 版本，使用[Windows 性能工具包 (WPT)](https://go.microsoft.com/fwlink/p/?linkid=294280)。 WPT 包括 Windows 性能记录器 (WPR) 可用于跟踪的内核模式电源提供程序和 Windows Performance Analyzer (WPA)，可以显示电源框架 (PoFx) 设备统计信息，之后可以以图形转换。

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>语法


```
pwrtest /device  [/t:n] [/?] 
```

<span id="_t_n"></span><span id="_T_N"></span>**/t:**<em>n</em>  
为方案运行指定的总时间 （以分钟为单位） (默认值*n*为 30 分钟)。

**示例**

```
pwrtest /device /t:60
```

```
pwrtest /device
```

### <a name="span-idxmllogfileoutputspanspan-idxmllogfileoutputspanspan-idxmllogfileoutputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML 日志文件输出

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
<td align="left"><strong>&lt;DeviceIdleEvents&gt;</strong></td>
<td align="left"><p>包含所有不同的设备空闲事件。 只有一个 <strong>&lt;DeviceIdleEvents</strong>每个 PwrTest 日志文件的元素。</p></td>
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
<td align="left"><p>设备空闲状态的统计信息事件。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;设备&gt;</strong></td>
<td align="left"><p>功能的设备对象。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;Pdo&gt;</strong></td>
<td align="left"><p>物理设备对象</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;ConservationTimeout&gt;</strong></td>
<td align="left"><p>保守超时值 （通常使用直流电源）。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;PerformanceTimeout&gt;</strong></td>
<td align="left"><p>性能 （通常使用交流电源） 的超时值。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;AccruedIdleTime&gt;</strong></td>
<td align="left"><p>时间段内所产生的空闲时间。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;BusyCount&gt;</strong></td>
<td align="left"><p>设备驱动程序调用的次数<a href="https://msdn.microsoft.com/library/windows/hardware/ff559755" data-raw-source="[&lt;strong&gt;PoSetDeviceBusy&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559755)"> <strong>PoSetDeviceBusy</strong> </a>期间。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;AccruedBusyCount&gt;</strong></td>
<td align="left"><p>设备驱动程序调用的次数总数<a href="https://msdn.microsoft.com/library/windows/hardware/ff559755" data-raw-source="[&lt;strong&gt;PoSetDeviceBusy&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559755)"> <strong>PoSetDeviceBusy</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;IdlePowerState&gt;</strong></td>
<td align="left"><p>显示的数字的状态为空闲状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;CurrentPowerState&gt;</strong></td>
<td align="left"><p>当前的数值的电源状态。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;分析&gt;</strong></td>
<td align="left"><p>字符串，描述在期间发生的情况。</p></td>
</tr>
</tbody>
</table>



## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[PwrTest 语法](pwrtest-syntax.md)










