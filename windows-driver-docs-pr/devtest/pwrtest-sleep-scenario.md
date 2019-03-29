---
title: PwrTest 睡眠方案
description: PwrTest 睡眠方案有助于自动测试的睡眠和恢复的转换。
ms.assetid: 2003ff3e-bc29-4741-a0a6-371948982679
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fef839a284e51312cc828c5653d3a5bfdb950a46
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568897"
---
# <a name="pwrtest-sleep-scenario"></a>PwrTest 睡眠方案


PwrTest 睡眠方案有助于自动测试的睡眠和恢复的转换。

PwrTest 都能够将平台定向到一个或多个睡眠状态，以自动方式和日志记录睡眠状态性能信息，例如 BIOS 初始化和总恢复时间。

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>语法


```
pwrtest /sleep [/c:n] [/d:n] [/p:n] [/h:{y|n}] [/s:{1|3|4|all|rnd|hibernate|standby}] [/unattend] [/e:n] [/?] 
```

<span id="_c_n"></span><span id="_C_N"></span>**/c:**<em>n</em>  
指定了多少个周期 （1 为默认值） 运行。

<span id="_d_n"></span><span id="_D_N"></span>**/d:**<em>n</em>  
指定延迟时间 （秒） （默认为 90）。

<span id="_p_n"></span><span id="_P_N"></span>**/p:**<em>n</em>  
指定的休眠时间 （秒） （60 是默认值）。 如果不支持休眠状态唤醒计时器，系统将重新启动并立即编写休眠文件后，恢复）。

<span id="_h_yn"></span><span id="_H_YN"></span>**h:**{**y**|**n**}  
指定是否已启用 (y) 或禁用 (n) 应为混合睡眠。 默认值为系统策略。

<span id="_s_134allrndhibernatestandby"></span><span id="_S_134ALLRNDHIBERNATESTANDBY"></span>**/s:**{**1**|**3**|**4**|**所有**| **rnd**|**休眠**|**备用**}  

<span id="1"></span>**1**  
指定目标状态始终是 S1。

<span id="3"></span>**3**  
指定的目标状态始终为 S3。

<span id="4"></span>**4**  
指定的目标状态始终为 S4。

<span id="all"></span><span id="ALL"></span>**all**  
指定循环按顺序的所有受支持的电源状态。

<span id="rnd"></span><span id="RND"></span>**rnd**  
指定随机循环进行所有受支持的电源状态。

<span id="hibernate"></span><span id="HIBERNATE"></span>**hibernate**  
指定目标状态始终是休眠 (S4)。

<span id="standby"></span><span id="STANDBY"></span>**standby**  
指定目标状态为任何可用的备用状态 （S1 或 S3）。

<span id="_unattend____"></span><span id="_UNATTEND____"></span>**/unattend**   
指定不在唤醒后更改系统执行状态。

<span id="_e_n"></span><span id="_E_N"></span>**e:**<em>n</em>  
以秒为单位为转换结束事件等待指定的超时 （默认为 120 秒）。

**示例**

```
pwrtest pwrtest /sleep /c:4 /s:all 
```

```
  pwrtest /sleep /c:4 /p:120 /d:150 /s:all
```

### <a name="span-idxmllogfileoutputspanspan-idxmllogfileoutputspanspan-idxmllogfileoutputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML 日志文件输出

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
<td align="left"><strong>&lt;SleepScenario&gt;</strong></td>
<td align="left"><p>包含与睡眠方案相关的信息。 只有一个<strong>&lt;SleepScenario&gt;</strong> PwrTest 日志文件中的元素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;SleepTransitions&gt;</strong></td>
<td align="left"><p>提供有关睡眠转换周期等的关键状态的总体数据和混合睡眠功能。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;SleepTransition&gt;</strong></td>
<td align="left"><p>提供有关恢复时间，例如 BIOS 初始化时间的开始和结束时间，以及详细信息等的每个睡眠周期信息。 一个<strong>&lt;SleepTransition&gt;</strong>为每个睡眠转换周期生成元素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;StartT&gt;</strong></td>
<td align="left"><p>指示在睡眠周期的开始时间。 (<em>hh</em>:<em>mm</em>:<em>ss</em>)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;EndT&gt;</strong></td>
<td align="left"><p>指示在睡眠周期的结束时间。 (<em>hh</em>:<em>mm</em>:<em>ss</em>)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;持续时间&gt;</strong></td>
<td align="left"><p>指示睡眠周期的持续时间。 (<em>hh</em>:<em>mm</em>:<em>ss</em>)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;TargetState&gt;</strong></td>
<td align="left"><p>指示目标睡眠状态。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;EffectiveState&gt;</strong></td>
<td align="left"><p>指示有效睡眠状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;BIOSInit&gt;</strong></td>
<td align="left"><p>指示初始化 BIOS 所需的时间量 （TargetState 必须为 3） 上继续以毫秒为单位。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;DriverInit&gt;</strong></td>
<td align="left"><p>指示在恢复以毫秒为单位的驱动程序进行初始化所需的时间量。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;挂起&gt;</strong></td>
<td align="left"><p>指示挂起系统以毫秒为单位的所需的时间量。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;恢复&gt;</strong></td>
<td align="left"><p>指示恢复以毫秒为单位的系统所需的时间总量。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;HiberRead&gt;</strong></td>
<td align="left"><p>指示读取以毫秒为单位的休眠文件所需的时间。 （TargetState 必须是 4）</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;HiberWrite&gt;</strong></td>
<td align="left"><p>表示以毫秒为单位写入休眠文件所需的时间。 (EffectiveState must be 4)</p></td>
</tr>
</tbody>
</table>



## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[PwrTest 语法](pwrtest-syntax.md)










