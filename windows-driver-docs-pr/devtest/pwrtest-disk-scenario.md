---
title: PwrTest 磁盘方案
description: PwrTest 磁盘方案监视磁盘空闲统计信息和降速事件。
ms.assetid: E54AA721-27C6-4E42-B42A-77AC70711A26
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d617380aadafbec455186289ba558f9a0c201da
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384777"
---
# <a name="pwrtest-disk-scenario"></a>PwrTest 磁盘方案


PwrTest 磁盘方案监视磁盘空闲统计信息和降速事件。

此方案主要用于 Windows 7 硬盘电源活动，后续版本的 Windows 将使用不同的机制跟踪磁盘空闲，而 Pwrtest 当前不支持此功能。 对于比 Windows 7 更新的 Windows 版本，请使用 [Windows 性能工具包 (WPT) ](/windows-hardware/test/wpt/windows-performance-toolkit-technical-reference)。 WPT 包括 Windows 性能记录器 (") ，可用于跟踪内核模式电源提供程序和 Windows 性能分析器 (WPA) ，该程序可显示 power framework (PoFx) 设备统计信息，并可以在以后图形转换。

**注意**   此方案不适用于所有类型的磁盘或控制器，因为并非所有存储驱动程序都注册了空闲检测。 有关详细信息，请参阅 [在存储类驱动程序中处理 PnP 启动](../storage/handling-pnp-start-in-a-storage-class-driver.md) 。

 

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>语法


```
pwrtest /disk  [/t:n] [/?] 
```

<span id="_t_n"></span><span id="_T_N"></span>**/t：**<em>n</em>  
指定运行该方案 (默认 *值为 30* 分钟) )  (的总时间（分钟）。

**示例**

```
pwrtest /disk /t:60
```

```
pwrtest /disk
```

### <a name="span-idxml_log_file_outputspanspan-idxml_log_file_outputspanspan-idxml_log_file_outputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML 日志文件输出

```XML
<PwrTestLog>
  <SystemInformation>
  </SystemInformation>
  <DiskIdleEvents> 
    <DiskIdleChangeEvent>
        <Timestamp></TimeStamp>
        <DiskNumber></DiskNumber>
        <InstancePath></InstancePath>
        <Description></Description>
    </DiskIdleChangeEvent>
    <DiskIdlePolicyChange>
        <Timestamp></TimeStamp>
        <Timeout></Timeout>
        <IgnoreThreshold></IgnoreThreshold>
    </DiskIdlePolicyChange>
    <DiskIdleEvent>
        <Timestamp></TimeStamp>
        <DiskNumber></DiskNumber>
        <InstancePath></InstancePath>
        <Device></Device>
        <Pdo></Pdo>
        <BusyCount></BusyCount>
        <AccruedBusyCount></AccruedBusyCount>
        <IdlePowerState></IdlePowerState>
        <CurrentPowerState></CurrentPowerState>
        <Timeout></Timeout>
        <IgnoreThreshold></IgnoreThreshold>
        <AccruedIdleTime></AccruedIdleTime>
        <AccruedNonIdleTime></AccruedNonIdleTime>
        <Analysis></Analysis>
    </DiskIdleEvent>
  </DiskIdleEvents>
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
<td align="left"><strong>&lt;DiskIdleEvents&gt;</strong></td>
<td align="left"><p>包含所有不同的磁盘空闲事件。 &lt; &gt; 每个 PwrTest 日志文件只能有一个 DeviceIdleEvents 元素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;时间戳&gt;</strong></td>
<td align="left"><p>任何给定事件的时间戳。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;DiskNumber&gt;</strong></td>
<td align="left"><p>标识此事件所针对的物理磁盘。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;InstancePath&gt;</strong></td>
<td align="left"><p>设备实例路径。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;DeviceIdleChangeEvent&gt;</strong></td>
<td align="left"><p>设备添加或删除事件。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;说明&gt;</strong></td>
<td align="left"><p>DeviceRemoved 或 DeviceDetected。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;DiskIdlePolicyChange&gt;</strong></td>
<td align="left"><p>磁盘超时更改事件。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;超时&gt;</strong></td>
<td align="left"><p>新磁盘降速超时。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;IgnoreThreshold&gt;</strong></td>
<td align="left"><p>新磁盘空闲忽略阈值。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;设备&gt;</strong></td>
<td align="left"><p>功能设备对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;Pdo&gt;</strong></td>
<td align="left"><p>物理设备对象</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;BusyCount&gt;</strong></td>
<td align="left"><p>一段时间内设备驱动程序调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer" data-raw-source="[&lt;strong&gt;PoSetDeviceBusy&lt;/strong&gt;](../kernel/mm-bad-pointer.md)"><strong>PoSetDeviceBusy</strong></a> 的次数。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;AccruedBusyCount&gt;</strong></td>
<td align="left"><p>设备驱动程序调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer" data-raw-source="[&lt;strong&gt;PoSetDeviceBusy&lt;/strong&gt;](../kernel/mm-bad-pointer.md)"><strong>PoSetDeviceBusy</strong></a> 总数的次数。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;IdlePowerState&gt;</strong></td>
<td align="left"><p>什么是空闲状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;CurrentPowerState&gt;</strong></td>
<td align="left"><p>当前数字的电源状态。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;超时&gt;</strong></td>
<td align="left"><p>超时时间 () 。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;IgnoreThreshold&gt;</strong></td>
<td align="left"><p>要忽略的非空闲时间的秒数</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;AccruedIdleTime&gt;</strong></td>
<td align="left"><p>期间内的应计空闲时间。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;AccruedNonIdleTime&gt;</strong></td>
<td align="left"><p>已累积的总空闲时间。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;分析&gt;</strong></td>
<td align="left"><p>描述期间发生的情况的字符串。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[PwrTest 语法](pwrtest-syntax.md)

 

