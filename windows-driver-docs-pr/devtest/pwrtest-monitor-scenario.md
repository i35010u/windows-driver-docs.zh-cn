---
title: PwrTest 监视方案
description: PwrTest 监视器方案记录用户监视或显示自动变暗和消隐功能相关的空闲统计信息。
ms.assetid: 8B45C85A-01E8-4256-82F3-097871CB9021
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a9e3a9b439f3888e05ffcbdee460e10f80462c6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351789"
---
# <a name="pwrtest-monitor-scenario"></a>PwrTest 监视方案

PwrTest 监视器方案记录用户监视或显示自动变暗和消隐功能相关的空闲统计信息。

当您运行 PwrTest 显示器的情况下时，你可能想要还运行[PwrTest 请求方案](pwrtest-requests-scenario.md)(**请求**) 另一个窗口中的方案。 PwrTest 请求方案可能有助于了解为什么监视器仍可能在或仍唤醒系统，即使该用户已经过足够长的时间空闲的空闲计时器过期。

如果您运行这两种方案，请务必使用 **/ln:**<em>名称</em>参数，以便可以更改日志文件和 ETW 跟踪会话名称。 名称必须不同，才能避免该工具的两个实例之间存在冲突。

## <a name="syntax"></a>语法

```command
pwrtest.exe /monitor  [/t:n] [/?] 
```

**/t:**<em>n</em>  
为方案运行指定的总时间 （以分钟为单位） (默认值*n*为 30 分钟)。

### <a name="examples"></a>示例

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
<td align="left"><strong>&lt;MonitorPower&gt;</strong></td>
<td align="left"><p>包含所有不同的显示器电源事件。 可能只有一个<strong>&lt;MonitorPower&gt;</strong> PwrTest 日志文件中的元素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;时间戳&gt;</strong></td>
<td align="left"><p>任何给定事件的时间戳。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;SessionId&gt;</strong></td>
<td align="left"><p>此事件是为用户会话的名称。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;IsConsoleSession&gt;</strong></td>
<td align="left"><p>显示物理控制台会话已连接到物理显示器。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;PhysicalMonitorBrightnessEvent&gt;</strong></td>
<td align="left"><p>事件指示当前监视器的亮度。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;MonitorIdleStatusEvent&gt;</strong></td>
<td align="left"><p>事件表示用户处于空闲状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;AccruedIdleTimeMs&gt;</strong></td>
<td align="left"><p>应计的用户以毫秒为单位的空闲时间。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;MonitorTimeoutsChangeEvent&gt;</strong></td>
<td align="left"><p>事件指示当前的空闲超时。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;DisplayTimeoutValueMs&gt;</strong></td>
<td align="left"><p>显示为空白以毫秒为单位的超时值。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ScreenSaverTimeoutValueMs&gt;</strong></td>
<td align="left"><p>屏幕保护程序超时值以毫秒为单位。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;DimTimeoutValueMs&gt;</strong></td>
<td align="left"><p>以毫秒为单位显示 dim 超时值</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;DimBrightnessValue&gt;</strong></td>
<td align="left"><p>若要使用在 dim 状态中的亮度。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;NormalBrightnessValue&gt;</strong></td>
<td align="left"><p>若要在何时使用状态的亮度。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;MonitorIdleActionExpireEvent&gt;</strong></td>
<td align="left"><p>事件指示已达到空闲超时和执行操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;IdleAction&gt;</strong></td>
<td align="left"><p>描述执行的操作 （屏幕保护程序启动，控制台锁定，监视器 dim 监视器空白）。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;IdleStartTime&gt;</strong></td>
<td align="left"><p>这种空闲状态的开始时间。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;TimeoutValueMs&gt;</strong></td>
<td align="left"><p>这种空闲状态以毫秒为单位的超时值。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;MonitorPowerEvent&gt;</strong></td>
<td align="left"><p>事件表示已被点击的显示器空闲超时和执行操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;NewState&gt;</strong></td>
<td align="left"><p>新状态 （打开/dim/关闭） 监视器。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;PreviousState&gt;</strong></td>
<td align="left"><p>前一状态 （打开/dim/关闭） 监视器。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;PreviousStateTime&gt;</strong></td>
<td align="left"><p>在以前的状态所用的时间。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;MonitorAdaptiveDimTimeoutEvent&gt;</strong></td>
<td align="left"><p>事件指示已更改的自适应的 dim 超时值。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;Timeout&gt;</strong></td>
<td align="left"><p>新的超时值以秒为单位。</p></td>
</tr>
</tbody>
</table>

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题

[PwrTest 语法](pwrtest-syntax.md)
