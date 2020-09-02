---
title: PwrTest 热量方案
description: PwrTest 散热方案监视 ACPI 热量区域信息和统计信息。
ms.assetid: C6941A50-EA0F-4C46-A290-8CAAD292E156
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d04a3ca0d9b4c4f4d889b62c59251d7ffc55407b
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89381933"
---
# <a name="pwrtest-thermal-scenario"></a>PwrTest 热量方案


PwrTest 散热方案监视 ACPI 热量区域信息和统计信息。 此方案仅在报告热量区域和温度变化的系统上受支持。

**注意**  此方案仅适用于向操作系统报告热量数据的系统。

 

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>语法


```
pwrtest /thermal [/t:n] [/?] 
```

<span id="_t_n"></span><span id="_T_N"></span>**/t：**<em>n</em>  
指定运行该方案 (默认 *值为 30* 分钟) )  (的总时间（分钟）。

<span id="_temp_kcf"></span><span id="_TEMP_KCF"></span>**/temp：**{**k** | **c** | **f**}  
指定温度刻度的开氏度 (**k**) ，摄氏温度 (**c**) ，华氏 (**f**) 用于所有输出和日志记录 (默认为 "开氏) "。

**示例**

```
pwrtest /thermal  
```

```
pwrtest /thermal  /t:30
```

```
pwrtest /thermal  /t:30 /temp:f
```

### <a name="span-idxml_log_file_outputspanspan-idxml_log_file_outputspanspan-idxml_log_file_outputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML 日志文件输出

```XML
<PwrTestLog>
  <SystemInformation>
  </SystemInformation>
  <ThermalEvents> 
    <PassiveCooling>
        <Timestamp></TimeStamp>
        <TemperatureScale></TemperatureScale>
        <ThermalZoneDeviceInstance></ThermalZoneDeviceInstance>
        <_TMP></_TMP>
        <_PSV></_PSV>
        <_TC1></_TC1>
        <_TC2></_TC2>
        <_TSP></_TSP>
    </PassiveCooling>
    <ActiveCooling>
        <Timestamp></TimeStamp>
        <TemperatureScale></TemperatureScale>
        <ThermalZoneDeviceInstance></ThermalZoneDeviceInstance>
        <_TMP></_TMP>
        <_AC0></_AC0>
        <_AC1></_AC1>
        <_AC2></_AC2>
        <_AC3></_AC3>
        <_AC4></_AC4>
        <_AC5></_AC5>
        <_AC6></_AC6>
        <_AC7></_AC7>
        <_AC8></_AC8>
        <_AC9></_AC9>
    </ActiveCooling>
    <Hot>
        <Timestamp></TimeStamp>
        <TemperatureScale></TemperatureScale>
        <ThermalZoneDeviceInstance></ThermalZoneDeviceInstance>
        <_HOT></_HOT>
    </Hot>
    <Critical>
        <Timestamp></TimeStamp>
        <TemperatureScale></TemperatureScale>
        <ThermalZoneDeviceInstance></ThermalZoneDeviceInstance>
        <_CRT></_CRT>
    </Critical>
    <ActiveCoolingDevicePower>
        <Timestamp></TimeStamp>
        <TemperatureScale></TemperatureScale>
        <ThermalZoneDeviceInstance></ThermalZoneDeviceInstance>
        <FanDeviceInstance></FanDeviceInstance>
        <PowerState></PowerState>
        <ActiveCoolingLevel></ActiveCoolingLevel>
        <ActiveCoolingDeviceIndex></ActiveCoolingDeviceIndex>
    </ActiveCoolingDevicePower>
  </ThermalEvents>
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
<td align="left"><strong>&lt;ThermalEvents&gt;</strong></td>
<td align="left"><p>包含所有不同的散热事件。 PwrTest 日志文件中只能有一个<strong> &lt; ThermalEvents &gt; </strong>元素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;EnteringCS&gt;</strong></td>
<td align="left"><p>连接备用 (CS) 条目开始，系统在 CS 中显示为 "已关闭"，并且 "输入" 处于禁用状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;ExitingCS&gt;</strong></td>
<td align="left"><p>CS 退出已经开始。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ExitedCS&gt;</strong></td>
<td align="left"><p>CS 退出已完成。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;AbortingCS&gt;</strong></td>
<td align="left"><p>进入最早阶段之前，将中止并退出 CS 条目。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;AbortedCS&gt;</strong></td>
<td align="left"><p>CS 退出在中止项后完成。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;InputDisabled&gt;</strong></td>
<td align="left"><p>已在本地控制台上禁用用户输入。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;InputEnabled&gt;</strong></td>
<td align="left"><p>已在本地控制台上启用用户输入。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;PhaseEnter&gt;</strong></td>
<td align="left"><p>输入 CS 阶段，name 属性是 CS 阶段的名称。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;PhaseExit&gt;</strong></td>
<td align="left"><p>CS 阶段退出，name 属性是 CS 阶段的名称。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;ExecutionRequiredSet&gt;</strong></td>
<td align="left"><p>执行了执行所需的请求，该请求将阻止 DAM 阶段完成。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ExecutionRequiredCleared&gt;</strong></td>
<td align="left"><p>进程清除了执行所需的请求，该请求将取消阻止 DAM 阶段完成。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;PlatformIdleStats&gt;</strong></td>
<td align="left"><p>平台空闲统计信息块。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;状态&gt;</strong></td>
<td align="left"><p>自上一个平台空闲统计信息块以来平台空闲状态的转换计数。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[PwrTest 语法](pwrtest-syntax.md)

[PowerCfg](/windows-hardware/design/device-experiences/powercfg-command-line-options)

 

