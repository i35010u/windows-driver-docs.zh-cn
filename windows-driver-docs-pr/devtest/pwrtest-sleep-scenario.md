---
title: PwrTest 睡眠方案
description: PwrTest 睡眠方案有助于自动测试睡眠和恢复转换。
ms.assetid: 2003ff3e-bc29-4741-a0a6-371948982679
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f121bdcd2b5dc2241547720eea5a88211b20b02
ms.sourcegitcommit: f8c3585ec7b1bdfcd65f7f2cc9aa688655de4d20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/15/2020
ms.locfileid: "81396307"
---
# <a name="pwrtest-sleep-scenario"></a>PwrTest 睡眠方案


PwrTest 睡眠方案有助于自动测试睡眠和恢复转换。

PwrTest 能够以自动方式将平台定向到一个或多个睡眠状态，并记录睡眠状态性能信息，例如 BIOS 初始化和总恢复时间。

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>语法


```
pwrtest /sleep [/c:n] [/d:n] [/p:n] [/h:{y|n}] [/s:{1|3|4|all|rnd|hibernate|standby}] [/unattend] [/e:n] [/?] 
```

<span id="_c_n"></span><span id="_C_N"></span> **/c：** <em>n</em>  
指定要运行的周期数（默认值为1）。

<span id="_d_n"></span><span id="_D_N"></span> **/d：** <em>n</em>  
指定延迟时间（以秒为单位）（默认值为90）。

<span id="_p_n"></span><span id="_P_N"></span> **/p：** <em>n</em>  
指定睡眠时间（以秒为单位）（默认值为60）。 如果休眠时不支持唤醒计时器，系统将重新启动并在写入休眠文件后立即恢复。

<span id="_h_yn"></span><span id="_H_YN"></span> **/h：** {**y**|**n**}  
指定是启用（y）还是禁用混合睡眠（n）。 默认值为 "系统策略"。

<span id="_s_134allrndhibernatestandby"></span><span id="_S_134ALLRNDHIBERNATESTANDBY"></span> **/s：** {**1**|**3**|**4**|**所有**|**rnd**|**休眠**|**待机**}  

<span id="1"></span>**2**  
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
指定目标状态始终为 "休眠（S4）"。

<span id="standby"></span><span id="STANDBY"></span>**转入**  
指定目标状态为任何可用的待机状态（S1 或 S3）。

<span id="_unattend____"></span><span id="_UNATTEND____"></span> **/unattend**   
指定在唤醒之后不更改系统执行状态。

<span id="_e_n"></span><span id="_E_N"></span> **/e：** <em>n</em>  
指定等待转换结束事件（默认值为120秒）的超时值（以秒为单位）。

**示例**

```
pwrtest /sleep /c:4 /s:all 
```

```
  pwrtest /sleep /c:4 /p:120 /d:150 /s:all
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
                  <Duration></Duration> 
                  <TargetState></TargetState> 
                  <EffectiveState></EffectiveState> 
                  <BIOSInit></BIOSInit> 
                  <DriverInit></DriverInit> 
                  <Suspend></Suspend> 
                  <Resume></Resume> 
                  <HiberRead></HiberRead> 
                  <HiberWrite></HiberWrite> 
            </SleepTransition> 
            <SleepTransition 
                  number="" 
                  status=""> 
                  <StartT></StartT> 
                  <EndT></EndT> 
                  <Duration></Duration> 
                  <TargetState></TargetState> 
                  <EffectiveState></EffectiveState> 
                  <BIOSInit></BIOSInit> 
                  <DriverInit></DriverInit> 
                  <Suspend></Suspend> 
                  <Resume></Resume> 
                  <HiberRead></HiberRead> 
                  <HiberWrite></HiberWrite> 
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
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>&lt;SleepScenario&gt;</strong></td>
<td align="left"><p>包含与睡眠方案相关的信息。 PwrTest 日志文件中只有一个<strong>&lt;SleepScenario&gt;</strong>元素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;SleepTransitions&gt;</strong></td>
<td align="left"><p>提供有关睡眠转换循环的总体数据，如关键和混合睡眠功能的状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;SleepTransition&gt;</strong></td>
<td align="left"><p>提供按睡眠的周期信息，如开始时间和结束时间，以及有关恢复时间的详细信息，例如 BIOS 初始化时间。 为每个休眠转换循环生成一个<strong>&lt;SleepTransition&gt;</strong>元素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;StartT&gt;</strong></td>
<td align="left"><p>指示睡眠周期的开始时间。 （<em>hh</em>：<em>mm</em>：<em>ss</em>）</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;EndT&gt;</strong></td>
<td align="left"><p>指示睡眠周期的结束时间。 （<em>hh</em>：<em>mm</em>：<em>ss</em>）</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;持续时间&gt;</strong></td>
<td align="left"><p>指示睡眠周期的持续时间。 （<em>hh</em>：<em>mm</em>：<em>ss</em>）</p></td>
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
<td align="left"><strong>&lt;BIOSInit&gt;</strong></td>
<td align="left"><p>指示在恢复时（以毫秒为单位）初始化 BIOS 所需的时间（TargetState 必须为3）。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;DriverInit&gt;</strong></td>
<td align="left"><p>指示在恢复时初始化驱动程序所需的时间（以毫秒为单位）。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;挂起&gt;</strong></td>
<td align="left"><p>指示挂起系统所需的时间（以毫秒为单位）。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;恢复&gt;</strong></td>
<td align="left"><p>指示恢复系统所需的总时间（以毫秒为单位）。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;HiberRead&gt;</strong></td>
<td align="left"><p>指示读取休眠文件所需的时间（以毫秒为单位）。 （TargetState 必须为4）</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;HiberWrite&gt;</strong></td>
<td align="left"><p>指示写入休眠文件所需的时间（以毫秒为单位）。 （EffectiveState 必须为4）</p></td>
</tr>
</tbody>
</table>



## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[PwrTest 语法](pwrtest-syntax.md)










