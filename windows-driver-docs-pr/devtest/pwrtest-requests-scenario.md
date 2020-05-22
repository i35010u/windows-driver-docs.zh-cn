---
title: PwrTest 请求方案
description: PwrTest 请求方案记录系统中正在运行的进程和服务的电源请求。
ms.assetid: 4B082680-5C43-45F6-9A0E-0C23E9B1F282
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2685134af91507fdf9b08bd69977825db0c9691a
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769657"
---
# <a name="pwrtest-requests-scenario"></a>PwrTest 请求方案


PwrTest 请求方案记录系统中正在运行的进程和服务的电源请求。

你可以使用 "PwrTest 请求" 方案诊断计算机不会进入睡眠状态的原因或监视器保持打开状态的原因。

你还可以使用管理员工具[PowerCfg](https://docs.microsoft.com/windows-hardware/design/device-experiences/powercfg-command-line-options) （powercfg）来实现此目的（**powercfg/requests**）。 PowerCfg 包含在 Windows 中（Windows \\ System32 目录）。 但是，Powercfg 仅捕获在运行该工具时处于活动状态的电源请求。 与此相反，PwrTest 请求方案在指定时间运行，并在创建和关闭时记录电源请求，因此在运行该工具时，请求无需处于活动状态。

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>语法


```
pwrtest /requests [/t:n] [/?] 
```

<span id="_t_n"></span><span id="_T_N"></span>**/t：**<em>n</em>  
指定应用场景运行的总时间（分钟）（ *n*的默认值为30分钟）。

**示例**

```
pwrtest /requests  
```

```
pwrtest /requests  /t:60
```

### <a name="span-idxml_log_file_outputspanspan-idxml_log_file_outputspanspan-idxml_log_file_outputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML 日志文件输出

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
<td align="left"><strong>&lt;PowerRequests&gt;</strong></td>
<td align="left"><p>包含所有不同的电源请求事件。 PwrTest 日志文件中只能有一个<strong> &lt; PowerRequests &gt; </strong>元素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;标志&gt;</strong></td>
<td align="left"><p>任何给定事件的时间戳。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;呼叫&gt;</strong></td>
<td align="left"><p>请求者的名称。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;上下文&gt;</strong></td>
<td align="left"><p>设备实例路径（如果适用）</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;RequestObject&gt;</strong></td>
<td align="left"><p>事件的请求对象。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;类型&gt;</strong></td>
<td align="left"><p>调用方的数值类型。</p>
<p>0 = 驱动程序</p>
<p>1 = 进程</p>
<p>2 = 共享服务</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;ProcessID&gt;</strong></td>
<td align="left"><p>调用方的进程 ID。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;SessionID&gt;</strong></td>
<td align="left"><p>调用方的会话 ID （如果为）。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;旧的&gt;</strong></td>
<td align="left"><p>如果调用方使用了旧的<a href="https://docs.microsoft.com/windows/desktop/api/winbase/nf-winbase-setthreadexecutionstate" data-raw-source="[&lt;strong&gt;SetThreadExecutionState function (Windows)&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winbase/nf-winbase-setthreadexecutionstate)"><strong>SetThreadExecutionState 函数（windows）</strong></a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-posetsystemstate" data-raw-source="[&lt;strong&gt;PoSetSystemState&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-posetsystemstate)"><strong>PoSetSystemState</strong></a> api 或较新的<a href="https://docs.microsoft.com/windows/desktop/api/winbase/nf-winbase-powersetrequest" data-raw-source="[&lt;strong&gt;PowerSetRequest function (Windows)&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winbase/nf-winbase-powersetrequest)"><strong>PowerSetRequest 函数（windows）</strong></a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerrequest" data-raw-source="[&lt;strong&gt;PoSetPowerRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerrequest)"><strong>PoSetPowerRequest</strong></a> api，则报告 True 或 False。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;SystemAllowed&gt;</strong></td>
<td align="left"><p>报告此调用方是否允许系统请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;DisplayAllowed&gt;</strong></td>
<td align="left"><p>报告此调用方是否允许显示请求。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;AwayModeAllowed&gt;</strong></td>
<td align="left"><p>报告此调用方是否允许离开模式请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;PerfBoostAllowed&gt;</strong></td>
<td align="left"><p>报告此调用方是否允许性能提升请求。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ExecutionRequiredAllowed&gt;</strong></td>
<td align="left"><p>报告此调用方是否允许执行所需的请求。</p></td>
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
<td align="left"><p>此调用方的远离模式请求数。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;PerfBoostCount&gt;</strong></td>
<td align="left"><p>此调用方的性能提升请求数。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;ExecutionRequiredCount&gt;</strong></td>
<td align="left"><p>此调用方所需的执行请求数。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;CreatePowerRequestEvent&gt;</strong></td>
<td align="left"><p>调用方已创建新的请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;ChangePowerRequestEvent&gt;</strong></td>
<td align="left"><p>调用方已更改请求计数。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ClosePowerRequestEvent&gt;</strong></td>
<td align="left"><p>调用方已关闭该请求。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[PwrTest 语法](pwrtest-syntax.md)

[PowerCfg](https://docs.microsoft.com/windows-hardware/design/device-experiences/powercfg-command-line-options)

 

 






