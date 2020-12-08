---
title: PwrTest 监视方案
description: PwrTest 监视器方案记录与监视器相关的用户空闲统计信息，或显示自动变暗和空白。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c84573477750d65b760e51ab230ef57d7555922e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823365"
---
# <a name="pwrtest-monitor-scenario"></a>PwrTest 监视方案

PwrTest 监视器方案记录与监视器相关的用户空闲统计信息，或显示自动变暗和空白。

当你运行 PwrTest 监视器方案时，你可能还想要在另一个窗口中 (**/requests**) 方案中运行 [PwrTest 请求方案](pwrtest-requests-scenario.md)。 即使用户的空闲时间足以使空闲计时器过期，PwrTest 请求方案也可能有助于了解监视器可能仍处于打开状态的原因或系统仍处于唤醒状态的原因。

如果运行这两种方案，请确保使用 **/ln：**<em>name</em> 参数，以便可以更改日志文件和 ETW 跟踪会话名称。 名称需要不同，以避免该工具的两个实例之间发生冲突。

## <a name="syntax"></a>语法

```command
pwrtest.exe /monitor  [/t:n] [/?] 
```

**/t：**<em>n</em>  
指定运行该方案 (默认 *值为 30* 分钟) )  (的总时间（分钟）。

## <a name="examples"></a>示例

```command
pwrtest.exe /device 
```

```command
pwrtest.exe /device /t:60
```

### <a name="xml-log-file-output"></a>XML 日志文件输出

```XML
<PwrTestLog>
  <SystemInformation>
  </SystemInformation>
  <MonitorPower> 
    <PhysicalMonitorBrightnessEvent>
        <Timestamp></TimeStamp>
        <PhysicalMonitorBrightnessPercent></PhysicalMonitorBrightnessPercent>
    </PhysicalMonitorBrightnessEvent>
    <MonitorIdleStatusEvent>
        <Timestamp></TimeStamp>
        <SessionId></SessionId>
        <AccruedIdleTimeMs></AccruedIdleTimeMs>
    </MonitorIdleStatusEvent>
    <MonitorTimeoutsChangeEvent>
        <Timestamp></TimeStamp>
        <SessionId></SessionId>
        <DisplayTimeoutValueMs></DisplayTimeoutValueMs>
        <ScreenSaverTimeoutValueMs></ScreenSaverTimeoutValueMs>
        <DimTimeoutValueMs></DimTimeoutValueMs>
        <DimBrightnessValue></DimBrightnessValue>
        <NormalBrightnessValue></NormalBrightnessValue>
    </MonitorTimeoutsChangeEvent>
    <MonitorIdleActionExpireEvent>
        <Timestamp></TimeStamp>
        <SessionId></SessionId>
        <IsConsoleSession></IsConsoleSession>
        <IdleAction></IdleAction>
        <IdleStartTime></IdleStartTime>
        <TimeoutValueMs></TimeoutValueMs>
    </MonitorIdleActionExpireEvent>
    <MonitorPowerEvent>
        <Timestamp></TimeStamp>
        <SessionId></SessionId>
        <IsConsoleSession></IsConsoleSession>
        <NewState></NewState>
        <PreviousState></PreviousState>
        <PreviousStateTime></PreviousStateTime>
    </MonitorPowerEvent>
    <MonitorAdaptiveDimTimeoutEvent>
        <Timestamp></TimeStamp>
        <Timeout></Timeout>
    </MonitorAdaptiveDimTimeoutEvent>
  </MonitorPower>
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
<td align="left"><strong>&lt;MonitorPower&gt;</strong></td>
<td align="left"><p>包含所有不同的监视器电源事件。 PwrTest 日志文件中只能有一个<strong> &lt; MonitorPower &gt; </strong>元素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;标志&gt;</strong></td>
<td align="left"><p>任何给定事件的时间戳。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;SessionId&gt;</strong></td>
<td align="left"><p>事件所针对的用户会话的名称。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;IsConsoleSession&gt;</strong></td>
<td align="left"><p>显示是否将物理控制台会话附加到物理监视器。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;PhysicalMonitorBrightnessEvent&gt;</strong></td>
<td align="left"><p>事件指示当前监视器亮度。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;MonitorIdleStatusEvent&gt;</strong></td>
<td align="left"><p>事件表明用户处于空闲状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;AccruedIdleTimeMs&gt;</strong></td>
<td align="left"><p>应计用户空闲时间（毫秒）。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;MonitorTimeoutsChangeEvent&gt;</strong></td>
<td align="left"><p>事件指示当前空闲超时。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;DisplayTimeoutValueMs&gt;</strong></td>
<td align="left"><p>显示空白超时值（以毫秒为单位）。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ScreenSaverTimeoutValueMs&gt;</strong></td>
<td align="left"><p>屏幕保护程序超时值（以毫秒为单位）。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;DimTimeoutValueMs&gt;</strong></td>
<td align="left"><p>显示 dim timeout 值（以毫秒为单位）</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;DimBrightnessValue&gt;</strong></td>
<td align="left"><p>处于 dim 状态时使用的亮度。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;NormalBrightnessValue&gt;</strong></td>
<td align="left"><p>处于开启状态时使用的亮度。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;MonitorIdleActionExpireEvent&gt;</strong></td>
<td align="left"><p>事件指示已命中空闲超时并执行了一个操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;IdleAction&gt;</strong></td>
<td align="left"><p>描述 (屏幕保护程序启动、控制台锁定、监视 dim、监视空) 所执行的操作。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;IdleStartTime&gt;</strong></td>
<td align="left"><p>此空闲状态的开始时间。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;TimeoutValueMs&gt;</strong></td>
<td align="left"><p>此空闲状态的超时值（以毫秒为单位）。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;MonitorPowerEvent&gt;</strong></td>
<td align="left"><p>事件表示点击了显示空闲超时，并采取了一种操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;NewState&gt;</strong></td>
<td align="left"><p>监视器 (的新状态/变暗/关闭) 。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;PreviousState&gt;</strong></td>
<td align="left"><p>监视器的先前状态 (打开/变暗/关闭) 。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;PreviousStateTime&gt;</strong></td>
<td align="left"><p>以前的状态所用的时间。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;MonitorAdaptiveDimTimeoutEvent&gt;</strong></td>
<td align="left"><p>事件指示自适应 dim timeout 已更改。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;超时&gt;</strong></td>
<td align="left"><p>新超时值（秒）。</p></td>
</tr>
</tbody>
</table>

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题

[PwrTest 语法](pwrtest-syntax.md)
