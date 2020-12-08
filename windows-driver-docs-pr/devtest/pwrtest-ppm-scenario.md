---
title: PwrTest PPM 方案
description: PwrTest PPM 方案记录处理器电源管理 (PPM) 信息和定期统计信息总计。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b014ce2b9602d632b8fdb768e10dac0a544204a4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823357"
---
# <a name="pwrtest-ppm-scenario"></a>PwrTest PPM 方案


PwrTest PPM 方案记录处理器电源管理 (PPM) 信息和定期统计信息总计。

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>语法


```
pwrtest /ppm [/n:n] [/i:n] [/c:[y|n]] [/p:{y|n}] [/u:{y|n}] [/live] [/t:n] [/?] 
```

<span id="_n_n"></span><span id="_N_N"></span>**/n：**<em>n</em>  
指定默认)  (100 的周期数。 按 **q** 退出) 。

<span id="_i_n"></span><span id="_I_N"></span>**/i：**<em>n</em>  
指定以毫秒为单位的轮询间隔（以毫秒为单位） (ms) ， (5000 ms 是默认) 。

<span id="_c_yn"></span><span id="_C_YN"></span>**/c：**{**y** | **n**}  
指定是否应捕获 C 状态信息。 选项为 yes (**y**) 或 no (**n**) 。 默认值为 yes (**y**) 。

<span id="_p_yn"></span><span id="_P_YN"></span>**/p：**{**y** | **n**}  
指定是否应捕获性能或限制状态信息。 选项为 yes (**y**) 或 no (**n**) 。 是 (**y**) 是默认值。

<span id="_u_yn"></span><span id="_U_YN"></span>**/u：**{**y** | **n**}  
指定是否应捕获 CPU 使用情况信息。 选项为 yes (**y**) 或 no (**n**) 。 是 (**y**) 是默认值。

<span id="_live"></span><span id="_LIVE"></span>**/live**  
实时显示处理器电源管理事件 (其他选项) 不可用。

<span id="_t_n"></span><span id="_T_N"></span>**/t：**<em>n</em>  
指定表示 **/live** 选项 (默认值为 30) 的总运行时间（以分钟为单位）。

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

### <a name="span-idxml_log_file_outputspanspan-idxml_log_file_outputspanspan-idxml_log_file_outputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML 日志文件输出

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
<td align="left"><strong>&lt;PPMScenario&gt;</strong></td>
<td align="left"><p>包含与 PPM 方案有关的信息。 PwrTest 日志文件中只有一个<strong> &lt; SleepScenario &gt; </strong>元素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ProcessorInformation&gt;</strong></td>
<td align="left"><p>包含与处理器的静态属性有关的信息，例如性能和限制状态功能。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;PerformanceStates&gt;</strong></td>
<td align="left"><p>包含<strong> &lt; PerformanceState &gt; </strong>元素的列表。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ProcessorName&gt;</strong></td>
<td align="left"><p>指示处理器的友好名称。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;InterfaceType&gt;</strong></td>
<td align="left"><p>指示用于在 Windows 和平台处理器电源管理功能之间进行交互的机制。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;TransitionLatency&gt;</strong></td>
<td align="left"><p>指示切换性能状态时的延迟。 包含单位属性，通常为微秒 (μs) </p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;ProcessorTraces&gt;</strong></td>
<td align="left"><p>包含<strong> &lt; 跟踪 &gt; </strong>元素的列表。 包含一个间隔属性，指示每个<strong> &lt; 跟踪 &gt; </strong>元素的间隔。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;跟踪&gt;</strong></td>
<td align="left"><p>包含跟踪信息，该信息因您用于 PwrTest 的命令选项而异。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;CpuId&gt;</strong></td>
<td align="left"><p>标识处理器。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ElapsedT&gt;</strong></td>
<td align="left"><p>指示自 PwrTest 开始后经过的时间（以毫秒为单位）。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;CPUIdle&gt;</strong></td>
<td align="left"><p>指示处理器空闲时间的百分比。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;PState&gt;</strong></td>
<td align="left"><p>指示当前处理器性能状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;频率&gt;</strong></td>
<td align="left"><p>指示当前处理器性能状态的实际频率（以兆赫为单位）。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;PercentOfMax&gt;</strong></td>
<td align="left"><p>指示当前性能状态的最大频率的百分比。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;PStateType&gt;</strong></td>
<td align="left"><p>指示性能状态 (1) 还是中止状态 (0) 。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;圆锥体&gt;</strong></td>
<td align="left"><p>指示 C1 CPU 空闲状态所用 CPU 空闲时间的百分比。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;CTwo&gt;</strong></td>
<td align="left"><p>指示在 C2 CPU 空闲状态中所用 CPU 空闲时间的百分比。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;CThree&gt;</strong></td>
<td align="left"><p>指示 C3 CPU 空闲状态所用 CPU 空闲时间的百分比。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[PwrTest 语法](pwrtest-syntax.md)

 

 






