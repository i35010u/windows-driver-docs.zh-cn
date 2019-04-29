---
title: PwrTest 请求方案
description: PwrTest 请求方案记录电源请求从进程和系统发生时运行的服务。
ms.assetid: 4B082680-5C43-45F6-9A0E-0C23E9B1F282
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a75d6084b5e3650dd795892235105e2f6e81854
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382667"
---
# <a name="pwrtest-requests-scenario"></a>PwrTest 请求方案


PwrTest 请求方案记录电源请求从进程和系统发生时运行的服务。

PwrTest 请求方案可用于诊断计算机不能进入睡眠或为什么监视器都保留在的原因。

也可以使用管理器工具[PowerCfg](https://go.microsoft.com/fwlink/p/?linkid=294568) (powercfg.exe) 实现此目的 (**powercfg.exe /requests**)。 PowerCfg 随 Windows (Windows\\System32 目录)。 但是，Powercfg.exe 仅捕获在运行该工具时处于活动状态的电源请求。 与此相反，PwrTest 请求方案运行指定的时间和日志电源请求被创建并已关闭，因此无需请求时运行该工具时处于活动状态。

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>语法


```
pwrtest /requests [/t:n] [/?] 
```

<span id="_t_n"></span><span id="_T_N"></span>**/t:**<em>n</em>  
为方案运行指定的总时间 （以分钟为单位） (默认值*n*为 30 分钟)。

**示例**

```
pwrtest /requests  
```

```
pwrtest /requests  /t:60
```

### <a name="span-idxmllogfileoutputspanspan-idxmllogfileoutputspanspan-idxmllogfileoutputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML 日志文件输出

```XML
<PwrTestLog>
  <SystemInformation>
  </SystemInformation>
  <PowerRequests> 
    <CreatePowerRequestEvent>
        <Timestamp></TimeStamp>
        <Caller></Caller>
        <Context></Context>
        <RequestObject></RequestObject>
        <Type></Type>
        <ProcessID></ProcessID>
        <SessionID></SessionID>
        <Legacy></Legacy>
        <SystemAllowed></SystemAllowed>
        <DisplayAllowed></DisplayAllowed>
        <AwayModeAllowed></AwayModeAllowed>
        <PerfBoostAllowed></PerfBoostAllowed>
        <ExecutionRequiredAllowed></ExecutionRequiredAllowed>    
        <SystemCount></SystemCount>
        <DisplayCount></DisplayCount>
        <AwayModeCount></AwayModeCount>
        <PerfBoostCount></PerfBoostCount>
        <ExecutionRequiredCount></ExecutionRequiredCount>
    </CreatePowerRequestEvent>
    <ChangePowerRequestEvent>
        <Timestamp></TimeStamp>
        <Caller></Caller>
        <RequestObject></RequestObject>
        <SystemCount></SystemCount>
        <DisplayCount></DisplayCount>
        <AwayModeCount></AwayModeCount>
        <PerfBoostCount></PerfBoostCount>
        <ExecutionRequiredCount></ExecutionRequiredCount>
    </ChangePowerRequestEvent>
    <ClosePowerRequestEvent>
        <Timestamp></TimeStamp>
        <Caller></Caller>
        <RequestObject></RequestObject>
    </ClosePowerRequestEvent>
  </PowerRequests>
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
<td align="left"><strong>&lt;PowerRequests&gt;</strong></td>
<td align="left"><p>包含所有不同的电源请求事件。 可能只有一个<strong>&lt;PowerRequests&gt;</strong> PwrTest 日志文件中的元素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;时间戳&gt;</strong></td>
<td align="left"><p>任何给定事件的时间戳。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;Caller&gt;</strong></td>
<td align="left"><p>请求者的名称。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;上下文&gt;</strong></td>
<td align="left"><p>如果适用的设备实例路径</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;RequestObject&gt;</strong></td>
<td align="left"><p>事件的请求对象。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;Type&gt;</strong></td>
<td align="left"><p>调用方的数值类型。</p>
<p>0 = 驱动程序</p>
<p>1 = 进程</p>
<p>2 = 共享的服务</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;ProcessID&gt;</strong></td>
<td align="left"><p>调用方的进程 ID。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;SessionID&gt;</strong></td>
<td align="left"><p>如果进程调用方的会话 ID。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;Legacy&gt;</strong></td>
<td align="left"><p>报告 True 或 False，如果调用方使用旧版<a href="https://msdn.microsoft.com/library/windows/desktop/aa373208" data-raw-source="[&lt;strong&gt;SetThreadExecutionState function (Windows)&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa373208)"> <strong>SetThreadExecutionState 函数 (Windows)</strong> </a>或<a href="https://msdn.microsoft.com/library/windows/hardware/ff559768" data-raw-source="[&lt;strong&gt;PoSetSystemState&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559768)"> <strong>PoSetSystemState</strong> </a> Api 或较新<a href="https://msdn.microsoft.com/library/windows/desktop/dd405534" data-raw-source="[&lt;strong&gt;PowerSetRequest function (Windows)&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/dd405534)"> <strong>PowerSetRequest 函数 (Windows)</strong> </a>或<a href="https://msdn.microsoft.com/library/windows/hardware/ff559762" data-raw-source="[&lt;strong&gt;PoSetPowerRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559762)"> <strong>PoSetPowerRequest</strong> </a> Api。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;SystemAllowed&gt;</strong></td>
<td align="left"><p>报告的此调用方是否允许系统的请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;DisplayAllowed&gt;</strong></td>
<td align="left"><p>报告是否为此调用方允许显示请求。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;AwayModeAllowed&gt;</strong></td>
<td align="left"><p>报告是否为此调用方允许离开模式请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;PerfBoostAllowed&gt;</strong></td>
<td align="left"><p>报告性能提升请求是否允许为此调用方。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ExecutionRequiredAllowed&gt;</strong></td>
<td align="left"><p>报告是否执行所需的此调用方允许的请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;SystemCount&gt;</strong></td>
<td align="left"><p>此调用方的系统请求数。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;DisplayCount&gt;</strong></td>
<td align="left"><p>此调用方的显示请求数。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;AwayModeCount&gt;</strong></td>
<td align="left"><p>此调用方的离开模式请求数。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;PerfBoostCount&gt;</strong></td>
<td align="left"><p>此调用方的性能提升请求数。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;ExecutionRequiredCount&gt;</strong></td>
<td align="left"><p>执行数所需的此调用方的请求。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;CreatePowerRequestEvent&gt;</strong></td>
<td align="left"><p>调用方已创建新的请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;ChangePowerRequestEvent&gt;</strong></td>
<td align="left"><p>调用方已更改的请求计数。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ClosePowerRequestEvent&gt;</strong></td>
<td align="left"><p>调用方已关闭请求。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[PwrTest 语法](pwrtest-syntax.md)

[PowerCfg](https://go.microsoft.com/fwlink/p/?linkid=294568)

 

 






