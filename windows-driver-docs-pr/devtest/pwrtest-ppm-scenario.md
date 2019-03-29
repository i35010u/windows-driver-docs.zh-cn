---
title: PwrTest PPM 方案
description: PwrTest PPM 方案记录处理器电源管理 (PPM) 信息和定期统计信息汇总。
ms.assetid: 735834dc-7351-44d1-a63f-9cb541184fde
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8596f134de9cf018fbc254fee0b7acab44d86749
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568902"
---
# <a name="pwrtest-ppm-scenario"></a>PwrTest PPM 方案


PwrTest PPM 方案记录处理器电源管理 (PPM) 信息和定期统计信息汇总。

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>语法


```
pwrtest /ppm [/n:n] [/i:n] [/c:[y|n]] [/p:{y|n}] [/u:{y|n}] [/live] [/t:n] [/?] 
```

<span id="_n_n"></span><span id="_N_N"></span>**/n:**<em>n</em>  
指定 （100 是默认值） 的周期的数。 按**q**退出)。

<span id="_i_n"></span><span id="_I_N"></span>**/i:**<em>n</em>  
指定轮询间隔以毫秒 (ms) 为单位 （5000 毫秒的延迟是默认值） 的 C-状态和处理器使用率。

<span id="_c_yn"></span><span id="_C_YN"></span>**/c:**{**y**|**n**}  
指定是否应该捕获 C 状态信息。 选项为是 (**y**) 或无 (**n**)。 默认值为是 (**y**)。

<span id="_p_yn"></span><span id="_P_YN"></span>**/p:**{**y**|**n**}  
指定是否应捕获性能或限制状态信息。 选项为是 (**y**) 或无 (**n**)。 是 (**y**) 是默认值。

<span id="_u_yn"></span><span id="_U_YN"></span>**/u:**{**y**|**n**}  
指定是否应捕获 CPU 使用情况信息。 选项为是 (**y**) 或无 (**n**)。 是 (**y**) 是默认值。

<span id="_live"></span><span id="_LIVE"></span>**/live**  
实时显示处理器电源管理事件 （其他选项将不可用）。

<span id="_t_n"></span><span id="_T_N"></span>**/t:**<em>n</em>  
指定以分钟为单位表示的总运行时， **/ live**选项 （默认值为 30）。

**示例**

```
pwrtest /ppm /c:y /p:y /u:y /n:60 /i:1000
```

```
  pwrtest /ppm /c:n /p:n /u:y /n:3600 /i:1000
```

```
  pwrtest /ppm /live
```

```
  pwrtest /ppm /live /t:60
```

### <a name="span-idxmllogfileoutputspanspan-idxmllogfileoutputspanspan-idxmllogfileoutputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML 日志文件输出

```XML
<PwrTestLog>
  <SystemInformation>
  </SystemInformation>
  <PPMScenario> 
    <ProcessorInformation> 
      <PerformanceStates> 
        <PerformanceState  
            number="0" 
            frequency="" 
            percentofmaxfrequency="" 
            type="" /> 
      </PerformanceStates> 
      <ProcessorName> </ProcessorName> 
      <InterfaceType> </InterfaceType> 
      <TransitionLatency units=""></TransitionLatency> 
    </ProcessorInformation> 
    <ProcessorTraces interval=""> 
      <Trace> 
        <CpuId></CpuId> 
        <ElapsedT></ElapsedT> 
        <CPUIdle></CPUIdle> 
        <PState></PState> 
        <Frequency></Frequency> 
        <PercentOfMax></PercentOfMax> 
        <PStateType></PStateType> 
        <COne></COne> 
        <CTwo></COne> 
        <CThree></CThree> 
      </Trace> 
    </ProcessorTraces> 
  </PPMScenario> 
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
<td align="left"><strong>&lt;PPMScenario&gt;</strong></td>
<td align="left"><p>包含有关 PPM 方案的相关信息。 只有一个<strong>&lt;SleepScenario&gt;</strong> PwrTest 日志文件中的元素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ProcessorInformation&gt;</strong></td>
<td align="left"><p>包含与处理器，如性能和限制状态功能的静态属性相关的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;PerformanceStates&gt;</strong></td>
<td align="left"><p>包含一系列<strong>&lt;PerformanceState&gt;</strong>元素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ProcessorName&gt;</strong></td>
<td align="left"><p>指示处理器的友好名称。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;InterfaceType&gt;</strong></td>
<td align="left"><p>指示用于 Windows 和平台之间建立连接处理器电源管理功能的机制。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;TransitionLatency&gt;</strong></td>
<td align="left"><p>指示延迟时切换性能状态。 包含单元属性通常微秒 （祍）</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;ProcessorTraces&gt;</strong></td>
<td align="left"><p>包含一系列<strong>&lt;跟踪&gt;</strong>元素。 包括，该值指示每个间隔的间隔属性<strong>&lt;跟踪&gt;</strong>元素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;Trace&gt;</strong></td>
<td align="left"><p>包含跟踪信息，具体取决于使用 PwrTest 命令选项而异。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;CpuId&gt;</strong></td>
<td align="left"><p>标识处理器。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ElapsedT&gt;</strong></td>
<td align="left"><p>指示以毫秒为单位的 PwrTest 启动以来经过的时间。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;CPUIdle&gt;</strong></td>
<td align="left"><p>指示处理器空闲时间的百分比。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;PState&gt;</strong></td>
<td align="left"><p>指示当前的处理器性能状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;频率&gt;</strong></td>
<td align="left"><p>指示当前的处理器性能状态，以兆赫为单位的实际频率。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;PercentOfMax&gt;</strong></td>
<td align="left"><p>表示当前性能状态的最大频率的百分比。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;PStateType&gt;</strong></td>
<td align="left"><p>表示性能状态是否是性能状态 (1) 或限制状态 (0)。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;COne&gt;</strong></td>
<td align="left"><p>表示处于 C1 CPU 空闲状态所用的 CPU 空闲时间的百分比。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;CTwo&gt;</strong></td>
<td align="left"><p>表示处于 C2 CPU 空闲状态所用的 CPU 空闲时间的百分比。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;CThree&gt;</strong></td>
<td align="left"><p>表示处于 C3 CPU 空闲状态所用的 CPU 空闲时间的百分比。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[PwrTest 语法](pwrtest-syntax.md)

 

 






