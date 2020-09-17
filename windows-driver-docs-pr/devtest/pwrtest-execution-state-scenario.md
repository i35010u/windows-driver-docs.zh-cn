---
title: PwrTest 执行状态方案
description: PwrTest 执行状态方案 (/es) 监视当前正在运行的进程和服务的线程执行状态更改。
ms.assetid: 5470c99b-5780-486f-b36a-922fb821b7f3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34e6e30ff25bd3bbbd3f06bff0fec30d420d6d05
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715716"
---
# <a name="pwrtest-execution-state-scenario"></a>PwrTest 执行状态方案


PwrTest 执行状态方案 (**/es**) 监视当前正在运行的进程和服务的线程执行状态更改。

**注意**   此 PwrTest 执行状态方案主要用于使用旧版 power request Api 的应用程序，例如[**SetThreadExecutionState 函数 (Windows) **](/windows/win32/api/winbase/nf-winbase-setthreadexecutionstate)) 。 若要监视使用较新的 power request Api 的应用程序（如 [**PowerSetRequest 函数） (Windows) **](/windows/win32/api/winbase/nf-winbase-powersetrequest) 改为使用 [PwrTest 请求方案](pwrtest-requests-scenario.md) 。

 

应用程序和服务可能会通过更改其线程执行状态来暂时覆盖电源管理设置，如监视器和睡眠空闲超时。 PwrTest 执行状态方案使用 Win32 [**SetThreadExecutionState 函数 (Windows) **](/windows/win32/api/winbase/nf-winbase-setthreadexecutionstate)监视线程执行状态和系统状态更改。

可以结合使用 **/es** 方案和 [PwrTest Idle 方案](pwrtest-idle-scenario.md) 来帮助识别阻止监视器或系统进入空闲状态的应用程序和服务。

### <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>语法

```
pwrtest /es  [/t:n] [/stes:{y|n}] [/rss:{y|n}] [/sss:{y|n}] [/all] [/user] [/kernel] [/idle] [/?] 
```

<span id="_t_n"></span><span id="_T_N"></span>**/t：**<em>n</em>  
指定运行该方案 (默认 *值为 30* 分钟) )  (的总时间（分钟）。

<span id="_stes_yn"></span><span id="_STES_YN"></span>**/stes：**{**y** | **n**}  
指定是否应 (**y**记录[**SetThreadExecutionState**](/windows/win32/api/winbase/nf-winbase-setthreadexecutionstate)事件 (是) 默认) 。

<span id="_rss_yn"></span><span id="_RSS_YN"></span>**/rss：**{**y** | **n**}  
指定是否应 (**y**记录**RegisterSystemState**事件 (是) 默认) 。

<span id="_sss_yn"></span><span id="_SSS_YN"></span>**/sss：**{**y** | **n**}  
指定是否应 (**y**记录**SetSystemState**事件 (是) 默认) 。

<span id="_all"></span><span id="_ALL"></span>**/all**  
指定应 ([**SetThreadExecutionState**](/windows/win32/api/winbase/nf-winbase-setthreadexecutionstate)， **RegisterSystemState**， **SetSystemState**) 记录所有事件。

<span id="_user"></span><span id="_USER"></span>**/user**  
指定应将所有用户事件记录 ([**SetThreadExecutionState**](/windows/win32/api/winbase/nf-winbase-setthreadexecutionstate)) 。

<span id="_kernel"></span><span id="_KERNEL"></span>**/kernel**  
指定仅应记录内核模式事件 (**RegisterSystemState**， **SetSystemState**) 。

<span id="_idle"></span><span id="_IDLE"></span>**/idle**  
日志空闲统计信息。

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

### <a name="span-idxml_log_file_outputspanspan-idxml_log_file_outputspanspan-idxml_log_file_outputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML 日志文件输出

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
<td align="left"><strong>&lt;ExecutionState&gt;</strong></td>
<td align="left"><p>包含与执行状态方案相关的信息。 PwrTest 日志文件中只能有一个<strong> &lt; executionstate& &gt; </strong>元素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;EsChange&gt;</strong></td>
<td align="left"><p>包含与单个线程执行状态更改事件相关的信息。 将有一个<strong> &lt; EsChange &gt; </strong>元素。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;阶段&gt;</strong></td>
<td align="left"><p>指示执行状态更改事件发生的时间。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;过程&gt;</strong></td>
<td align="left"><p>指示请求执行状态更改的进程的映像文件的路径。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;RawState&gt;</strong></td>
<td align="left"><p>指示请求执行状态。 这是 EXECUTION_STATE (类型的32位值，请参阅 Windows) 。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;连续&gt;</strong></td>
<td align="left"><p>指示进程是否请求的执行状态更改为连续 (ES_CONTINUOUS) 。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;System&gt;</strong></td>
<td align="left"><p>指示 () 如果进程请求提供系统 (ES_SYSTEM_REQUIRED)  (FALSE) 。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;显示&gt;</strong></td>
<td align="left"><p>指示 (TRUE) 如果该进程已请求显示可用 (ES_DISPLAY_REQUIRED) 或 (FALSE) 错误。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;AwayMode&gt;</strong></td>
<td align="left"><p>指示 (TRUE) 如果已 (ES_AWAYMODE_REQUIRED) ，则 () FALSE。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[PwrTest 语法](pwrtest-syntax.md)

 

