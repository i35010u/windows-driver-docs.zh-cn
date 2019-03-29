---
title: PwrTest 连接待机方案
description: PwrTest 连接备用方案 (/ cs) 同时还帮助自动测试的已连接的备用转换。
ms.assetid: 2601603D-F9AF-4DEB-9A1B-F5A091A51B2B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0dfd00a1637484860280ff137cfa8038d30af7d2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577464"
---
# <a name="pwrtest-connected-standby-scenario"></a>PwrTest 连接待机方案


PwrTest 连接备用方案 (**/cs**) 同时还帮助自动测试的已连接的备用转换。

PwrTest 记录通过 PDC 阶段进度，并尝试登录平台空闲转换计数，如果系统支持。 这可用于诊断如果系统正在进入空闲状态时深入的平台，和任何软件组件造成了阻碍转换。

此方案需要测试系统以支持*始终打开始终连接*(AoAc) 电源功能 （大多数 SoC 和 ARM 系统支持此）。 此方案还要求是一部分的 Windows 驱动程序测试框架 (WDTF) 的电源按钮驱动程序。 预配的系统，使用 Visual Studio 和 WDK 测试时，会自动安装 WDTF （和包含的电源按钮驱动程序）。 有关详细信息，请参阅[预配计算机，以使驱动程序部署和测试 (WDK 8.1)](https://msdn.microsoft.com/library/windows/hardware/dn745909)，或[预配计算机，以使驱动程序部署和测试 (WDK 8)](https://msdn.microsoft.com/library/windows/hardware/hh698272)。 WDTF 有关的信息，请参阅[ **Windows 设备测试框架 (WDTF) （Windows 驱动程序）**](https://msdn.microsoft.com/library/windows/hardware/ff539547)。

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>语法


```
pwrtest /cs [/c:n] [/d:n] [/p:n][/?] 
```

<span id="_c_n"></span><span id="_C_N"></span>**/c:**<em>n</em>  
指定了多少个周期 （1 为默认值） 运行。

<span id="_d_n"></span><span id="_D_N"></span>**/d:**<em>n</em>  
指定的延迟时间 （以秒为单位） 之间连接备用转换 （60 秒是默认值）。

<span id="_p_n"></span><span id="_P_N"></span>**/p:**<em>n</em>  
指定连接备用退出时间 （以秒为单位; 60 秒是默认值）。

**示例**

```
pwrtest /cs /c:4 
```

```
pwrtest /cs /c:4 /p:120 /d:150
```

### <a name="span-idxmllogfileoutputspanspan-idxmllogfileoutputspanspan-idxmllogfileoutputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML 日志文件输出

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
<td align="left"><strong>&lt;CSTransitions&gt;</strong></td>
<td align="left"><p>包含所有的不同连接备用事件。 可能只有一个<strong>&lt;CSTransitions&gt;</strong> PwrTest 日志文件中的元素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;时间戳&gt;</strong></td>
<td align="left"><p>任何给定事件的时间戳。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;TemperatureScale&gt;</strong></td>
<td align="left"><p>温标 (华氏温度 Kelvin/Celcius&gt;的任何给定的事件。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ThermalZoneDeviceInstance&gt;</strong></td>
<td align="left"><p>热感任何的区域给定事件的设备实例名称。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;_TMP&gt;</strong></td>
<td align="left"><p>在任何给定事件的系统的当前温度。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;_PSV&gt;， &lt;_TCx&gt;， &lt;_TSP&gt;， &lt;_ACx&gt;， &lt;_HOT&gt;， &lt;_CRT&gt;，等等。</strong></td>
<td align="left"><p>发送与给定事件的系统温度阈值。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;PassiveCooling&gt;</strong></td>
<td align="left"><p>事件表示系统现在已在被动冷却区域中。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ActiveCooling&gt;</strong></td>
<td align="left"><p>事件表示系统现在已在 active 冷却区域中。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;热&gt;</strong></td>
<td align="left"><p>事件表示系统已达到热行程点。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;Critical&gt;</strong></td>
<td align="left"><p>事件表示系统已达到严重错误点。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;ActiveCoolingDevicePower&gt;</strong></td>
<td align="left"><p>事件表示 active 的冷却设备已打开。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;FanDeviceInstance&gt;</strong></td>
<td align="left"><p>设备风扇的实例名称。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;PowerState&gt;</strong></td>
<td align="left"><p>(1) 或关闭 (0) 的电源状态。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ActiveCoolingLevel&gt;</strong></td>
<td align="left"><p>Active 冷却数字级别。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;ActiveCoolingDeviceIndex&gt;</strong></td>
<td align="left"><p>冷却设备数字索引。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[PwrTest 语法](pwrtest-syntax.md)

 

 






