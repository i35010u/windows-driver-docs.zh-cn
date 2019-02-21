---
title: PwrTest 执行状态的情况
description: PwrTest 执行状态的情况 (/ es) 监视器线程当前正在运行的进程和服务的执行状态发生更改。
ms.assetid: 5470c99b-5780-486f-b36a-922fb821b7f3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6f321396beaddca43406e4c201840a24d5f29cd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540805"
---
# <a name="pwrtest-execution-state-scenario"></a>PwrTest 执行状态的情况


PwrTest 执行状态的情况 (**/es**) 监视器线程当前正在运行的进程和服务的执行状态发生更改。

**请注意**  此 PwrTest 执行状态的情况主要用于应用程序使用旧版 power 请求 Api，如[ **SetThreadExecutionState 函数 (Windows)** ](https://msdn.microsoft.com/library/windows/desktop/aa373208)). 若要监视的应用程序使用较新的 power 请求 Api，如[ **PowerSetRequest 函数 (Windows)** ](https://msdn.microsoft.com/library/windows/desktop/dd405534)使用[PwrTest 请求方案](pwrtest-requests-scenario.md)相反。

 

应用程序和服务可能会暂时替代监视器之类的电源管理设置和通过更改其线程执行状态睡眠空闲超时。 PwrTest 执行状态方案监视线程的执行状态和系统状态将更改该应用程序和服务使用 Win32 做[ **SetThreadExecutionState 函数 (Windows)** ](https://msdn.microsoft.com/library/windows/desktop/aa373208).

可以使用 **/es**一起使用的方案[PwrTest 空闲方案](pwrtest-idle-scenario.md)来帮助确定应用程序和服务，使监视器或系统无法进入空闲状态。

### <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>语法

```
pwrtest /es  [/t:n] [/stes:{y|n}] [/rss:{y|n}] [/sss:{y|n}] [/all] [/user] [/kernel] [/idle] [/?] 
```

<span id="_t_n"></span><span id="_T_N"></span>**/t:**<em>n</em>  
为方案运行指定的总时间 （以分钟为单位） (默认值*n*为 30 分钟)。

<span id="_stes_yn"></span><span id="_STES_YN"></span>**/stes:**{**y**|**n**}  
指定是否[ **SetThreadExecutionState** ](https://msdn.microsoft.com/library/windows/desktop/aa373208)应记录事件 (**y** (yes) 是默认值)。

<span id="_rss_yn"></span><span id="_RSS_YN"></span>**/rss:**{**y**|**n**}  
指定是否**RegisterSystemState**应记录事件 (**y** (yes) 是默认值)。

<span id="_sss_yn"></span><span id="_SSS_YN"></span>**/sss:**{**y**|**n**}  
指定是否**SetSystemState**应记录事件 (**y** (yes) 是默认值)。

<span id="_all"></span><span id="_ALL"></span>**/all**  
指定应记录所有事件 ([**SetThreadExecutionState**](https://msdn.microsoft.com/library/windows/desktop/aa373208)， **RegisterSystemState**， **SetSystemState**)。

<span id="_user"></span><span id="_USER"></span>**/user**  
指定应记录所有用户事件 ([**SetThreadExecutionState**](https://msdn.microsoft.com/library/windows/desktop/aa373208))。

<span id="_kernel"></span><span id="_KERNEL"></span>**/kernel**  
指定应记录仅内核模式事件 (**RegisterSystemState**， **SetSystemState**)。

<span id="_idle"></span><span id="_IDLE"></span>**/idle**  
日志空闲状态的统计信息。

**示例**

```
pwrtest /es /all
```

```
pwrtest /es /user
```

```
pwrtest /es /kernel
```

```
pwrtest /es /kernel /sss:n
```

```
pwrtest /es /kernel /rss:n
```

```
pwrtest /es /kernel /rss:y /sss:n
```

```
pwrtest /es /sss:n
```

```
pwrtest /es /rss:n /sss:n
```

```
pwrtest /es /stes:n 
```

```
pwrtest /es /all /idle 
```

### <a name="span-idxmllogfileoutputspanspan-idxmllogfileoutputspanspan-idxmllogfileoutputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML 日志文件输出

```XML
<PwrTestLog>
  <SystemInformation>
  </SystemInformation>
  <ExecutionState> 
    <EsChange> 
      <Time>XX:XX:XX</Time>
      <Process></Process>
        <RawState></RawState>
        <Continuous></Continuous>
        <System></System>
        <Display></Display>
        <AwayMode></AwayMode>
    </EsChange> 
    <EsChange> 
      <Time>XX:XX:XX</Time>
      <Process></Process>
        <RawState></RawState>
        <Continuous></Continuous>
        <System></System>
        <Display></Display>
        <AwayMode></AwayMode>
    </EsChange> 
  </ExecutionState>
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
<td align="left"><strong>&lt;ExecutionState&gt;</strong></td>
<td align="left"><p>包含与执行状态的情况相关的信息。 可能只有一个<strong>&lt;ExecutionState&gt;</strong> PwrTest 日志文件中的元素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;EsChange&gt;</strong></td>
<td align="left"><p>包含单个线程执行状态更改事件相关信息。 将一个<strong>&lt;EsChange&gt;</strong>元素。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;时间&gt;</strong></td>
<td align="left"><p>指示执行状态更改事件发生时的时间。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;Process&gt;</strong></td>
<td align="left"><p>指示请求的执行状态更改的进程的图像文件的路径。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;RawState&gt;</strong></td>
<td align="left"><p>指示请求执行状态。 这是类型 EXECUTION_STATE 的 32 位值 （请参阅 Windows.h）。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;Continuous&gt;</strong></td>
<td align="left"><p>指示是否进程请求执行状态更改为持续 (ES_CONTINUOUS)。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;System&gt;</strong></td>
<td align="left"><p>如果在过程请求或不是可用 (ES_SYSTEM_REQUIRED) 系统 (TRUE) 指示 (FALSE)。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;显示&gt;</strong></td>
<td align="left"><p>如果在过程请求显示为可用 (ES_DISPLAY_REQUIRED)，或不 (TRUE) 指示 (FALSE)。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;AwayMode&gt;</strong></td>
<td align="left"><p>如果为过程请求离开模式或未启用 (ES_AWAYMODE_REQUIRED) (TRUE) 指示 (FALSE)。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[PwrTest 语法](pwrtest-syntax.md)

 

 






