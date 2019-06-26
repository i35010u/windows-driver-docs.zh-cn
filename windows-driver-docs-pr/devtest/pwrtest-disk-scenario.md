---
title: PwrTest 磁盘方案
description: PwrTest 磁盘的情况下监视磁盘空闲的统计信息和向下数值调节钮的事件。
ms.assetid: E54AA721-27C6-4E42-B42A-77AC70711A26
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da12a7c265694dd3d4bfd73525088ba8f2d2af2e
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393501"
---
# <a name="pwrtest-disk-scenario"></a>PwrTest 磁盘方案


PwrTest 磁盘的情况下监视磁盘空闲的统计信息和向下数值调节钮的事件。

此方案主要用于 Windows 7 硬盘电源活动，后续版本的 Windows 跟踪磁盘空闲的 Pwrtest 目前不支持使用不同的机制。 对于 Windows 7 比更高版本的 Windows 版本，使用[Windows 性能工具包 (WPT)](https://go.microsoft.com/fwlink/p/?linkid=294280)。 WPT 包括 Windows 性能记录器 (WPR) 可用于跟踪的内核模式电源提供程序和 Windows Performance Analyzer (WPA)，可以显示电源框架 (PoFx) 设备统计信息，之后可以以图形转换。

**请注意**  由于并非所有存储驱动程序都注册为空闲检测，这种情况下不适合所有类型的磁盘或控制器。 请参阅[存储类驱动程序中处理即插即用启动](https://docs.microsoft.com/windows-hardware/drivers/storage/handling-pnp-start-in-a-storage-class-driver)有关详细信息。

 

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>语法


```
pwrtest /disk  [/t:n] [/?] 
```

<span id="_t_n"></span><span id="_T_N"></span> **/t:** <em>n</em>  
为方案运行指定的总时间 （以分钟为单位） (默认值*n*为 30 分钟)。

**示例**

```
pwrtest /disk /t:60
```

```
pwrtest /disk
```

### <a name="span-idxmllogfileoutputspanspan-idxmllogfileoutputspanspan-idxmllogfileoutputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML 日志文件输出

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
<td align="left"><strong>&lt;DiskIdleEvents&gt;</strong></td>
<td align="left"><p>包含所有不同的磁盘空闲事件。 只有一个&lt;DeviceIdleEvents&gt;每个 PwrTest 日志文件的元素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;时间戳&gt;</strong></td>
<td align="left"><p>任何给定事件的时间戳。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;DiskNumber&gt;</strong></td>
<td align="left"><p>标识的物理磁盘是此事件的。</p></td>
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
<td align="left"><strong>&lt;Timeout&gt;</strong></td>
<td align="left"><p>新磁盘驱动器关闭超时值。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;IgnoreThreshold&gt;</strong></td>
<td align="left"><p>新磁盘空闲忽略阈值。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;设备&gt;</strong></td>
<td align="left"><p>功能的设备对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;Pdo&gt;</strong></td>
<td align="left"><p>物理设备对象</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;BusyCount&gt;</strong></td>
<td align="left"><p>设备驱动程序调用的次数<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer" data-raw-source="[&lt;strong&gt;PoSetDeviceBusy&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)"> <strong>PoSetDeviceBusy</strong> </a>期间。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;AccruedBusyCount&gt;</strong></td>
<td align="left"><p>数乘以设备驱动程序调用<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer" data-raw-source="[&lt;strong&gt;PoSetDeviceBusy&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)"> <strong>PoSetDeviceBusy</strong> </a>总数。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;IdlePowerState&gt;</strong></td>
<td align="left"><p>哪些数值状态为空闲状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;CurrentPowerState&gt;</strong></td>
<td align="left"><p>当前的数值的电源状态。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;Timeout&gt;</strong></td>
<td align="left"><p>超时 （以秒为单位）。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;IgnoreThreshold&gt;</strong></td>
<td align="left"><p>忽略非空闲时间的秒数</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;AccruedIdleTime&gt;</strong></td>
<td align="left"><p>时间段内应计空闲的时间。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;AccruedNonIdleTime&gt;</strong></td>
<td align="left"><p>已计入总空闲时间。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;分析&gt;</strong></td>
<td align="left"><p>字符串，描述在期间发生的情况。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[PwrTest 语法](pwrtest-syntax.md)

 

 






