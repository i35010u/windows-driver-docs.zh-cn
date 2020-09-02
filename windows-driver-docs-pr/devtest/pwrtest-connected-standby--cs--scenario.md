---
title: PwrTest 连接待机方案
description: PwrTest 连接备用方案 (/cs) 有助于自动测试连接的备用转换。
ms.assetid: 2601603D-F9AF-4DEB-9A1B-F5A091A51B2B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b9261890c8e42a2f7b345f20b05a2ab0bafc120
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382967"
---
# <a name="pwrtest-connected-standby-scenario"></a>PwrTest 连接待机方案


PwrTest 连接备用方案 (**/cs**) 有助于自动测试连接的备用转换。

PwrTest 记录 PDC 阶段的进度，并尝试记录平台空闲转换计数（如果系统支持它们）。 这对于诊断系统是否进入深层平台空闲状态以及任何软件组件是否正在阻止转换很有用。

此方案要求测试系统 *支持 (AoAc*) 电源功能 (大多数 SOC 和 ARM 系统支持此) 。 此方案还要求 (WDTF) 的 Windows 驱动程序测试框架中包含的电源按钮驱动程序。 使用 Visual Studio 和 WDK 预配系统进行测试时，会自动安装 WDTF (和随附的电源按钮驱动程序) 。 有关详细信息，请参阅[设置计算机以进行驱动程序部署和测试 (wdk 8.1) ](../gettingstarted/provision-a-target-computer-wdk-8-1.md)，或 [预配用于驱动程序部署和测试 (WDK 8) ](/previous-versions/hh698272(v=vs.85))的计算机。 有关 WDTF 的信息，请参阅 [**Windows 设备测试框架 (WDTF)  (Windows 驱动程序) **](../wdtf/index.md)。

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>语法


```
pwrtest /cs [/c:n] [/d:n] [/p:n][/?] 
```

<span id="_c_n"></span><span id="_C_N"></span>**/c：**<em>n</em>  
指定运行)  (1 的周期数。

<span id="_d_n"></span><span id="_D_N"></span>**/d：**<em>n</em>  
指定连接备用转换之间)  (延迟时间（以秒为单位） (60 秒是默认) 。

<span id="_p_n"></span><span id="_P_N"></span>**/p：**<em>n</em>  
指定连接的备用退出时间 (（秒）;默认) 为60秒。

**示例**

```
pwrtest /cs /c:4 
```

```
pwrtest /cs /c:4 /p:120 /d:150
```

### <a name="span-idxml_log_file_outputspanspan-idxml_log_file_outputspanspan-idxml_log_file_outputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML 日志文件输出

```XML
<PwrTestLog>
  <SystemInformation>
  </SystemInformation>
  <CSTransitions>
    <EnteringCS Timestamp="XX/XX/XXXX:XX:XX:XX.XXX"/>
    <InputDisabled Timestamp="XX/XX/XXXX:XX:XX:XX.XXX"/>
    <PhaseEnter name="name" Timestamp="XX/XX/XXXX:XX:XX:XX.XXX"/>
    <PhaseExit name="name" Timestamp="XX/XX/XXXX:XX:XX:XX.XXX"/>
    <ExitingCS Timestamp="XX/XX/XXXX:XX:XX:XX.XXX"/> || 
        <AbortingCS Timestamp="XX/XX/XXXX:XX:XX:XX.XXX"/>
    <InputEnabled Timestamp="XX/XX/XXXX:XX:XX:XX.XXX"/>
    <ExitedCS Timestamp="XX/XX/XXXX:XX:XX:XX.XXX"/> || 
        <AbortedCS Timestamp="XX/XX/XXXX:XX:XX:XX.XXX"/>
    <ExecutionRequiredSet Caller="c:\folder\process.exe" 
        Timestamp="XX/XX/XXXX:XX:XX:XX.XXX"/> ||
        <ExecutionRequiredCleared Caller="c:\folder\process.exe" 
            Timestamp="XX/XX/XXXX:XX:XX:XX.XXX"/>
    <PlatformIdleStats StateCount="X" Timestamp="XX/XX/XXXX:XX:XX:XX.XXX">
        <State Index="X" SuccessCount="X" FailureCount="X" CancelCount="X"/>
    </PlatformIdleStats>
  </CSTransitions>
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
<td align="left"><strong>&lt;CSTransitions&gt;</strong></td>
<td align="left"><p>包含所有不同的连接备用事件。 PwrTest 日志文件中只能有一个<strong> &lt; CSTransitions &gt; </strong>元素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;时间戳&gt;</strong></td>
<td align="left"><p>任何给定事件的时间戳。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;TemperatureScale&gt;</strong></td>
<td align="left"><p>温度范围 (&gt; 任何给定事件的开氏度/摄氏温度计/华氏。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ThermalZoneDeviceInstance&gt;</strong></td>
<td align="left"><p>任何给定事件的热区的设备实例名称。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;_TMP&gt;</strong></td>
<td align="left"><p>任何给定事件中系统的当前温度。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;_PSV &gt; 、 &lt; _TCx &gt; 、 &lt; _TSP &gt; 、 &lt; _ACx &gt; 、 &lt; _HOT &gt; 、 &lt; _CRT 等 &gt; 。</strong></td>
<td align="left"><p>系统温度阈值与给定事件一起发送。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;PassiveCooling&gt;</strong></td>
<td align="left"><p>事件表明系统现在处于被动冷却区域。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ActiveCooling&gt;</strong></td>
<td align="left"><p>事件表明系统现在处于活动的冷却区域。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;热&gt;</strong></td>
<td align="left"><p>事件表明系统已达到热行程点。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;严重&gt;</strong></td>
<td align="left"><p>事件表明系统已达到关键行程点。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;ActiveCoolingDevicePower&gt;</strong></td>
<td align="left"><p>事件指示活动冷却设备已打开。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;FanDeviceInstance&gt;</strong></td>
<td align="left"><p>风扇的设备实例名称。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;PowerState&gt;</strong></td>
<td align="left"><p> (1) 或关闭 (0) 电源状态。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ActiveCoolingLevel&gt;</strong></td>
<td align="left"><p>活动冷却的数字级别。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;ActiveCoolingDeviceIndex&gt;</strong></td>
<td align="left"><p>冷却设备的数字索引。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[PwrTest 语法](pwrtest-syntax.md)

 

