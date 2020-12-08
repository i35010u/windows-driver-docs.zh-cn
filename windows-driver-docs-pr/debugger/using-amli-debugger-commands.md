---
title: 使用 AMLI 调试器命令
description: 使用 AMLI 调试器命令
keywords:
- AMLI 调试器，AMLI 调试器命令
ms.date: 11/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 09d48d0ed2eb845a0cc36c28f870dbce0ae1e12f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803189"
---
# <a name="using-amli-debugger-commands"></a>使用 AMLI 调试器命令


## <span id="ddk_using_amli_debugger_commands_dbg"></span><span id="DDK_USING_AMLI_DEBUGGER_COMMANDS_DBG"></span>


可以从 AMLI 调试器提示符发出以下命令。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">常规类别</th>
<th align="left">特定操作</th>
<th align="left">AMLI 调试器命令</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>控制调试器</p></td>
<td align="left"><p></p>
继续执行内核调试器</td>
<td align="left"><p></p>
<strong>g</strong>
<strong>q</strong></td>
</tr>
<tr class="even">
<td align="left"><p>控制 AML 执行</p></td>
<td align="left"><p></p>
在 AML 代码跟踪上运行方法单步执行 AML 代码</td>
<td align="left"><p></p>
<strong>运行</strong>
<strong>p</strong>
<strong>t</strong></td>
</tr>
<tr class="odd">
<td align="left"><p>控制跟踪模式设置</p></td>
<td align="left"><p>配置跟踪模式</p></td>
<td align="left"><p><strong>跟踪</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>通知命名空间对象</p></td>
<td align="left"><p>通知命名空间对象</p></td>
<td align="left"><p><strong>警告</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>显示 "对象计数" 表</p></td>
<td align="left"><p>显示对象计数表</p></td>
<td align="left"><p><strong>dc</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>访问内存</p></td>
<td align="left"><p></p>
显示数据显示数据字节显示数据字显示数据 Dword 显示数据字符串编辑内存</td>
<td align="left"><p></p>
<strong>d</strong>
<strong>db</strong>
<strong>dw</strong>
<strong>dd</strong>
<strong>da</strong>
<strong>e</strong></td>
</tr>
<tr class="odd">
<td align="left"><p>访问端口</p></td>
<td align="left"><p></p>
从端口读取到端口的读取字节从端口读取 DWORD 从端口写入字节到端口写入字到端口写入 DWORD 到端口</td>
<td align="left"><p></p>
<strong>i</strong>
<strong>iw</strong>
<strong>id</strong>
<strong>o</strong>
<strong>o</strong>
<strong>od</strong></td>
</tr>
<tr class="even">
<td align="left"><p>显示帮助</p></td>
<td align="left"><p>显示帮助</p></td>
<td align="left"><p><strong>?</strong></p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcontrolling_the_debuggerspanspan-idcontrolling_the_debuggerspancontrolling-the-debugger"></a><span id="controlling_the_debugger"></span><span id="CONTROLLING_THE_DEBUGGER"></span>控制调试器

这些命令退出 AMLI 调试器。 **G** 命令将恢复目标计算机的正常执行， **q** 命令将冻结目标计算机并进入内核调试器。

**g**

**：**

### <a name="span-idcontrolling_aml_executionspanspan-idcontrolling_aml_executionspancontrolling-aml-execution"></a><span id="controlling_aml_execution"></span><span id="CONTROLLING_AML_EXECUTION"></span>控制 AML 执行

这些命令允许你运行或单步执行 AML 方法。 **Run** 命令在指定点开始执行。 使用 **p** 和 **t** 命令可以一次单步执行一个指令。 如果遇到函数调用，则 **p** 命令会将函数视为单个步骤，而 **t** 命令每次只跟踪一个指令。


**运行***方法名称* **\[** _ArgumentList_*_\]_*

**运行** *CodeAddress* **\[** _ArgumentList_*_\]_*

**h-p**

**t**

<span id="MethodName"></span><span id="methodname"></span><span id="METHODNAME"></span>*名称*  
指定方法的完整路径和名称。 执行将从该方法的内存位置的开头开始。

<span id="CodeAddress"></span><span id="codeaddress"></span><span id="CODEADDRESS"></span>*CodeAddress*  
指定开始执行的地址。

<span id="ArgumentList"></span><span id="argumentlist"></span><span id="ARGUMENTLIST"></span>*ArgumentList*  
指定要传递给方法的参数列表。 每个参数都必须是整数。 应将多个参数与空格分隔开。

### <a name="span-idcontrolling_trace_mode_settingsspanspan-idcontrolling_trace_mode_settingsspancontrolling-trace-mode-settings"></a><span id="controlling_trace_mode_settings"></span><span id="CONTROLLING_TRACE_MODE_SETTINGS"></span>控制跟踪模式设置

**Trace** 命令控制 AML 解释器的跟踪模式设置。 如果使用不带任何参数的命令，则将显示当前的跟踪模式设置。

**trace \[ trigon | trigoff \] \[ level =**<em>level</em> **\] \[ add =**<em>TPStrings</em> **\] \[ zap =**<em>TPNumbers</em>**\]**

<span id="trigon"></span><span id="TRIGON"></span>**trigon**  
激活跟踪触发器模式。

<span id="trigoff"></span><span id="TRIGOFF"></span>**trigoff**  
停用跟踪触发器模式。

<span id="Level"></span><span id="level"></span><span id="LEVEL"></span>*调配*  
为跟踪级别指定新设置。

<span id="TPStrings"></span><span id="tpstrings"></span><span id="TPSTRINGS"></span>*TPStrings*  
指定要添加的一个或多个触发器点。 每个触发器点都按名称指定。 多个触发器点字符串应由逗号分隔。

<span id="TPNumbers"></span><span id="tpnumbers"></span><span id="TPNUMBERS"></span>*TPNumbers*  
指定要删除的一个或多个触发器点。 每个触发器点都按编号指定。 多个触发器点号应以逗号分隔。 若要查看触发器点编号的列表，请使用不带参数的 **trace** 命令。

### <a name="span-idnotifying_a_namespace_objectspanspan-idnotifying_a_namespace_objectspannotifying-a-namespace-object"></a><span id="notifying_a_namespace_object"></span><span id="NOTIFYING_A_NAMESPACE_OBJECT"></span>通知命名空间对象

**Notify** 命令将通知发送到 ACPI 命名空间对象。 通知将被放入指定对象的队列中。

**通知** *ObjectName 值*

**通知** *ObjectAddress 值*

<span id="ObjectName"></span><span id="objectname"></span><span id="OBJECTNAME"></span>*ObjectName*  
指定要通知的对象的完整命名空间路径。

<span id="ObjectAddress"></span><span id="objectaddress"></span><span id="OBJECTADDRESS"></span>*ObjectAddress*  
指定要通知的对象的地址。

<span id="Value"></span><span id="value"></span><span id="VALUE"></span>*负值*  
指定通知值。

### <a name="span-iddisplaying_the_object_count_tablespanspan-iddisplaying_the_object_count_tablespandisplaying-the-object-count-table"></a><span id="displaying_the_object_count_table"></span><span id="DISPLAYING_THE_OBJECT_COUNT_TABLE"></span>显示 "对象计数" 表

**Dc** 命令显示内存对象计数表。

**dc**

### <a name="span-idaccessing_memoryspanspan-idaccessing_memoryspanaccessing-memory"></a><span id="accessing_memory"></span><span id="ACCESSING_MEMORY"></span>访问内存

内存访问命令允许您读写内存。 读取内存时，可以选择包含 **db**、 **dw**、 **dd** 或 **da** 命令的内存单元大小。 简单的 **d** 命令以最近选择的单位显示内存。 如果这是使用的第一个显示命令，则使用字节单位。

如果未指定地址或方法，则将在上一个显示命令结束的位置开始显示。

这些命令与标准内核调试器内存命令具有相同的效果;它们在 AMLI 调试器中是重复的，以便于访问。

**d \[ b | w | d | a \] \[ \[ l =**<em>Length</em> **\] \[** *方法* **| \[%%\]** <em>Address</em> **\] 地址 \]**

**\[ %% e \]**<em>地址 Datalist</em>

<span id="b"></span><span id="B"></span>**b**  
指定数据应以字节为单位显示。

<span id="w"></span><span id="W"></span>**水平**  
指定在 word (16 位) 单元中显示数据。

<span id="d"></span><span id="D"></span>**2-d**  
指定应在 DWORD (32 位) 单元中显示数据。

<span id="a"></span><span id="A"></span>**的**  
指定数据应显示为字符串。 数据显示为 ASCII 字符。 当读取空字符或显示 *长度* 字符时，显示将终止。

<span id="Length"></span><span id="length"></span><span id="LENGTH"></span>*长短*  
指定要显示的字节数。 *长度* 必须是不带 **0x** 前缀)  (的十六进制数。 如果省略 *Length* ，则默认的显示大小为0x80 个字节。

<span id="Method"></span><span id="method"></span><span id="METHOD"></span>*付款方式*  
指定方法的完整路径和名称。 显示将从该方法的内存位置的开头开始。

<span id="Address"></span><span id="address"></span><span id="ADDRESS"></span>*地址*  
指定开始读取或写入的内存地址。 如果地址的前面有两个百分号 (**%%**) ，则将其解释为物理地址。 否则，会将其解释为虚拟地址。

<span id="DataList"></span><span id="datalist"></span><span id="DATALIST"></span>*DataList*  
指定要写入内存的数据。 列表中的每个项可以是十六进制字节或字符串。 使用字符串时，必须用引号将其引起来。 应该用空格分隔多个项。

### <a name="span-idaccessing_portsspanspan-idaccessing_portsspanaccessing-ports"></a><span id="accessing_ports"></span><span id="ACCESSING_PORTS"></span>访问端口

端口命令允许从数据端口发送输出或接收输入。 **I** 和 **o** 命令传输单个字节， **iw** 和 **o** 命令传输字 (16 位) ， **id** 和 **od** 命令传输 dword (32 bits) 。

这些命令与标准内核调试器端口命令具有相同的效果;它们在 AMLI 调试器中是重复的，以便于访问。

**i** *端口*

**iw** *端口*

**id** *端口*

**o** *端口* *DataForPort*

**o** *端口* *DataForPort*

**od** *端口* *DataForPort*

<span id="Port"></span><span id="port"></span><span id="PORT"></span>*口*  
指定要访问的端口的地址。 端口大小必须与选择的命令匹配。

<span id="DataForPort"></span><span id="dataforport"></span><span id="DATAFORPORT"></span>*DataForPort*  
指定要写入端口的数据。 此数据的大小必须与选择的命令匹配。

### <a name="span-iddisplaying_helpspanspan-iddisplaying_helpspandisplaying-help"></a><span id="displaying_help"></span><span id="DISPLAYING_HELP"></span>显示帮助

此命令显示 AMLI 调试器命令的帮助文本。

**? \[**<em>命令</em>**\]**

<span id="Command"></span><span id="command"></span><span id="COMMAND"></span>*Command*  
指定要显示其帮助的命令。 如果省略此，将显示所有 AMLI 调试器命令和 AMLI 调试器扩展的列表。

## <a name="see-also"></a>另请参阅

[AMLI 调试器](the-amli-debugger.md) 
