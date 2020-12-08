---
title: PwrTest 睡眠方案
description: PwrTest 睡眠方案有助于自动测试睡眠和恢复转换。
ms.date: 06/24/2020
ms.localizationpriority: medium
ms.openlocfilehash: f6e5432cdfd06a9a53706f0d87d78ed9323f65c9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824581"
---
# <a name="pwrtest-sleep-scenario"></a>PwrTest 睡眠方案


PwrTest 睡眠方案有助于自动测试睡眠和恢复转换。

PwrTest 能够以自动方式将平台定向到一个或多个睡眠状态，并记录睡眠状态性能信息，例如 BIOS 初始化和总恢复时间。

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>语法


```
pwrtest /sleep [/c:n] [/d:n] [/p:n] [/h:{y|n}] [/s:{1|3|4|all|rnd|hibernate|standby|dozes4}] [/unattend] [dt:n] [/e:n] [/?] 
```

<span id="_c_n"></span><span id="_C_N"></span>**/c：**<em>n</em>  
指定要运行的默认)  (1 的周期数。

<span id="_d_n"></span><span id="_D_N"></span>**/d：**<em>n</em>  
指定默认)  (90 的延迟时间（以秒为单位）。

<span id="_p_n"></span><span id="_P_N"></span>**/p：**<em>n</em>  
以秒为单位指定睡眠时间 (60) 。 如果休眠时不支持唤醒计时器，系统将重新启动并在写入休眠文件) 后立即恢复。

<span id="_h_yn"></span><span id="_H_YN"></span>**/h：**{**y** | **n**}  
指定是应 (y) 还是禁用 (n) 启用混合睡眠。 默认值为 "系统策略"。

<span id="_s_134allrndhibernatestandby"></span><span id="_S_134ALLRNDHIBERNATESTANDBY"></span>**/s：**{**1** | **3** | **4** | **所有** | **rnd** | **休眠** | **备用** | **dozes4**}  

<span id="1"></span>**1**  
指定目标状态始终为 S1。

<span id="3"></span>**三维空间**  
指定目标状态始终是 S3。

<span id="4"></span>**4**  
指定目标状态始终为 S4。

<span id="all"></span><span id="ALL"></span>**一切**  
指定按顺序对所有支持的电源状态进行循环。

<span id="rnd"></span><span id="RND"></span>**rnd**  
指定随机遍历所有支持的电源状态。

<span id="hibernate"></span><span id="HIBERNATE"></span>**r**  
指定目标状态始终处于休眠状态 (S4) 。

<span id="standby"></span><span id="STANDBY"></span>**转入**  
指定目标状态为)  (S1 或 S3 可用的任何备用状态。

<span id="standby"></span><span id="STANDBY"></span>**dozes4**  
指定从新式备用 (S0 低功耗空闲) doze 到 S4。

<span id="_unattend____"></span><span id="_UNATTEND____"></span>**/unattend**   
指定在唤醒之后不更改系统执行状态。

<span id="_dt_n"></span><span id="_DT_N"></span>**/dt：**<em>n</em>  
仅适用于 dozeS4，以秒为单位指定 doze 超时（以秒为单位），以便将其转换为休眠状态 (S4) 。

<span id="_e_n"></span><span id="_E_N"></span>**/e：**<em>n</em>  
指定等待转换结束事件的超时时间（秒） (默认) 为120秒。

**示例**

```
pwrtest /sleep /c:4 /s:all 
```

```
pwrtest /sleep /c:4 /p:120 /d:150 /s:all
```

```
pwrtest /sleep /c:10 /s:dozes4 /dt:100 /p:100
```

### <a name="span-idxml_log_file_outputspanspan-idxml_log_file_outputspanspan-idxml_log_file_outputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML 日志文件输出

```XML
<PwrTestLog>
  <SystemInformation>
  </SystemInformation>
  <SleepScenario> 
    <SleepTransitions 
            critical="" 
            hybrid="" 
            delay="" 
            sleeptime=""> 
            <SleepTransition 
                  number="" 
                  status=""> 
                  <StartT></StartT> 
                  <EndT></EndT> 
                  <SleepTimeMs></SleepTimeMs> 
                  <TargetState></TargetState> 
                  <EffectiveState></EffectiveState> 
                  <BIOSInitTimeMs></BIOSInitTimeMs> 
                  <DriverWakeTimeMs></DriverWakeTimeMs> 
                  <Suspend></Suspend> 
                  <Resume></Resume> 
                  <HiberReadTimeMs></HiberReadTimeMs> 
                  <HiberWriteTimeMs></HiberWriteTimeMs> 
                  <HiberPagesWritten></HiberPagesWritten> 
            </SleepTransition> 
            <SleepTransition 
                  number="" 
                  status=""> 
                  <StartT></StartT> 
                  <EndT></EndT> 
                  <SleepTimeMs></SleepTimeMs> 
                  <TargetState></TargetState> 
                  <EffectiveState></EffectiveState> 
                  <BIOSInitTimeMs></BIOSInitTimeMs> 
                  <DriverWakeTimeMs></DriverWakeTimeMs> 
                  <Suspend></Suspend> 
                  <Resume></Resume> 
                  <HiberReadTimeMs></HiberReadTimeMs> 
                  <HiberWriteTimeMs></HiberWriteTimeMs> 
                  <HiberPagesWritten></HiberPagesWritten> 
            </SleepTransition>
    </SleepTransitions> 
  </SleepScenario> 
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
<td align="left"><strong>&lt;SleepScenario&gt;</strong></td>
<td align="left"><p>包含与睡眠方案相关的信息。 PwrTest 日志文件中只有一个<strong> &lt; SleepScenario &gt; </strong>元素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;SleepTransitions&gt;</strong></td>
<td align="left"><p>提供有关睡眠转换循环的总体数据，如关键和混合睡眠功能的状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;SleepTransition&gt;</strong></td>
<td align="left"><p>提供按睡眠的周期信息，如开始时间和结束时间，以及有关恢复时间的详细信息，例如 BIOS 初始化时间。 为每个睡眠过渡周期生成一个<strong> &lt; SleepTransition &gt; </strong>元素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;StartT&gt;</strong></td>
<td align="left"><p>指示睡眠周期的开始时间。  (<em>hh</em>：<em>mm</em>：<em>ss</em>) </p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;EndT&gt;</strong></td>
<td align="left"><p>指示睡眠周期的结束时间。  (<em>hh</em>：<em>mm</em>：<em>ss</em>) </p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;SleepTimeMs&gt;</strong></td>
<td align="left"><p>指示睡眠周期的持续时间。  (<em>hh</em>：<em>mm</em>：<em>ss</em>) </p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;TargetState&gt;</strong></td>
<td align="left"><p>指示目标休眠状态。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;EffectiveState&gt;</strong></td>
<td align="left"><p>指示有效睡眠状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;BIOSInitTimeMs&gt;</strong></td>
<td align="left"><p>指示初始化 BIOS 所需的时间量 (在恢复时必须为 3) （以毫秒为单位）。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;DriverWakeTimeMs&gt;</strong></td>
<td align="left"><p>指示在恢复时初始化驱动程序所需的时间（以毫秒为单位）。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;休眠&gt;</strong></td>
<td align="left"><p>指示挂起系统所需的时间（以毫秒为单位）。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;恢复&gt;</strong></td>
<td align="left"><p>指示恢复系统所需的总时间（以毫秒为单位）。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;HiberReadTimeMs&gt;</strong></td>
<td align="left"><p>指示读取休眠文件所需的时间（以毫秒为单位）。  (TargetState 必须是 4) </p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;HiberWriteTimeMs&gt;</strong></td>
<td align="left"><p>指示写入休眠文件所需的时间（以毫秒为单位）。  (EffectiveState 必须是 4) </p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;HiberPagesWritten&gt;</strong></td>
<td align="left"><p>在休眠文件中写入的页数。  (EffectiveState 必须是 4) </p></td>
</tr>
</tbody>
</table>



## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[PwrTest 语法](pwrtest-syntax.md)










