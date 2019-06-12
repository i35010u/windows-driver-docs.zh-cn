---
title: 使用 AMLI 调试器命令
description: 使用 AMLI 调试器命令
ms.assetid: 8efa6f13-67db-417a-83ec-8219afc9874c
keywords:
- AMLI 调试器，AMLI 调试器命令
ms.date: 11/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0e6507ad0e708e59444f229a9df8489272e9dce0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383745"
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
<th align="left">特定的操作</th>
<th align="left">AMLI 调试器命令</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>控制调试器</p></td>
<td align="left"><p></p>
继续执行中断添加到内核调试程序</td>
<td align="left"><p></p>
<strong>g</strong>
<strong>q</strong></td>
</tr>
<tr class="even">
<td align="left"><p>控制 AML 执行</p></td>
<td align="left"><p></p>
通过 AML 代码跟踪方法步骤遇到 AML 代码</td>
<td align="left"><p></p>
<strong>run</strong>
<strong>p</strong>
<strong>t</strong></td>
</tr>
<tr class="odd">
<td align="left"><p>控制跟踪模式设置</p></td>
<td align="left"><p>配置跟踪模式</p></td>
<td align="left"><p><strong>trace</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>通知 Namespace 对象</p></td>
<td align="left"><p>通知 Namespace 对象</p></td>
<td align="left"><p><strong>notify</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>显示对象的计数表</p></td>
<td align="left"><p>显示对象计数表</p></td>
<td align="left"><p><strong>dc</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>访问内存</p></td>
<td align="left"><p></p>
显示数据显示数据字节显示数据单词显示数据包括显示数据字符串编辑内存</td>
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
读取来自端口的端口读取 Word 中的字节读取来自端口 DWORD 将字节写入到端口写入 DWORD 以端口的端口写入 Word</td>
<td align="left"><p></p>
<strong>i</strong>
<strong>iw</strong>
<strong>id</strong>
<strong>o</strong>
<strong>ow</strong>
<strong>od</strong></td>
</tr>
<tr class="even">
<td align="left"><p>显示帮助</p></td>
<td align="left"><p>显示帮助</p></td>
<td align="left"><p><strong>?</strong></p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcontrollingthedebuggerspanspan-idcontrollingthedebuggerspancontrolling-the-debugger"></a><span id="controlling_the_debugger"></span><span id="CONTROLLING_THE_DEBUGGER"></span>控制调试器

这些命令退出 AMLI 调试器。 **G**命令将继续正常执行目标计算机，并**q**命令将冻结目标计算机并进入内核调试器。

**g**

**q**

### <a name="span-idcontrollingamlexecutionspanspan-idcontrollingamlexecutionspancontrolling-aml-execution"></a><span id="controlling_aml_execution"></span><span id="CONTROLLING_AML_EXECUTION"></span>控制 AML 执行

这些命令可用于运行或单步执行 AML 方法。 **运行**命令开始的指定点处的执行。 **P**并**t**命令使您可以单步执行一次一条指令。 如果遇到函数调用，则**p**命令将函数视为一个步骤中，虽然**t**命令跟踪为一次新的函数一个指令。


**运行** *MethodName*  **\[ ***ArgumentList***\]**

**run** *CodeAddress* **\[***ArgumentList***\]**

**p**

**t**

<span id="MethodName"></span><span id="methodname"></span><span id="METHODNAME"></span>*MethodName*  
指定完整路径和方法的名称。 执行将在此方法的内存位置的开始处启动。

<span id="CodeAddress"></span><span id="codeaddress"></span><span id="CODEADDRESS"></span>*CodeAddress*  
指定执行的开始位置的地址。

<span id="ArgumentList"></span><span id="argumentlist"></span><span id="ARGUMENTLIST"></span>*ArgumentList*  
指定要传递给方法的参数列表。 每个自变量必须是整数。 应该用空格分隔多个自变量。

### <a name="span-idcontrollingtracemodesettingsspanspan-idcontrollingtracemodesettingsspancontrolling-trace-mode-settings"></a><span id="controlling_trace_mode_settings"></span><span id="CONTROLLING_TRACE_MODE_SETTINGS"></span>控制跟踪模式设置

**跟踪**命令控制 AML 解释器的跟踪模式设置。 如果不带任何参数使用此命令，将显示当前的跟踪模式设置。

**trace \[trigon|trigoff\] \[level=** <em>Level</em> **\] \[add=** <em>TPStrings</em> **\] \[zap=** <em>TPNumbers</em> **\]**

<span id="trigon"></span><span id="TRIGON"></span>**trigon**  
激活跟踪触发器模式。

<span id="trigoff"></span><span id="TRIGOFF"></span>**trigoff**  
停用跟踪触发器模式。

<span id="Level"></span><span id="level"></span><span id="LEVEL"></span>*级别*  
指定跟踪级别的新设置。

<span id="TPStrings"></span><span id="tpstrings"></span><span id="TPSTRINGS"></span>*TPStrings*  
指定要添加的一个或多个触发器点。 每个触发点是由名称指定。 应由逗号分隔多个触发器点字符串。

<span id="TPNumbers"></span><span id="tpnumbers"></span><span id="TPNUMBERS"></span>*TPNumbers*  
指定要删除的一个或多个触发器点。 每个触发点被指定的数量。 应由逗号分隔多个触发器点号。 若要查看触发器的点号列表，请使用**跟踪**命令不带任何参数。

### <a name="span-idnotifyinganamespaceobjectspanspan-idnotifyinganamespaceobjectspannotifying-a-namespace-object"></a><span id="notifying_a_namespace_object"></span><span id="NOTIFYING_A_NAMESPACE_OBJECT"></span>通知 Namespace 对象

**通知**命令将通知发送到 ACPI 命名空间对象。 将指定的对象的队列中放置该通知。

**通知** *ObjectName 值*

**通知** *ObjectAddress 值*

<span id="ObjectName"></span><span id="objectname"></span><span id="OBJECTNAME"></span>*ObjectName*  
指定要通知的对象的完整命名空间路径。

<span id="ObjectAddress"></span><span id="objectaddress"></span><span id="OBJECTADDRESS"></span>*ObjectAddress*  
指定要通知的对象的地址。

<span id="Value"></span><span id="value"></span><span id="VALUE"></span>*值*  
指定的通知值。

### <a name="span-iddisplayingtheobjectcounttablespanspan-iddisplayingtheobjectcounttablespandisplaying-the-object-count-table"></a><span id="displaying_the_object_count_table"></span><span id="DISPLAYING_THE_OBJECT_COUNT_TABLE"></span>显示对象的计数表

**Dc**命令显示内存对象计数表。

**dc**

### <a name="span-idaccessingmemoryspanspan-idaccessingmemoryspanaccessing-memory"></a><span id="accessing_memory"></span><span id="ACCESSING_MEMORY"></span>访问内存

内存访问命令可用于读取和写入内存。 当读取内存时，可以选择使用的内存单位的大小**db**， **dw**， **dd**或者**da**命令。 一个简单**d**命令显示内存中的最近最选择单位。 如果这是所使用的第一个显示命令，将使用字节为单位。

如果不指定任何地址或方法，将前一个显示命令结束的地方开始显示。

这些命令具有相同的效果与标准内核调试器内存命令;它们被复制在轻松访问 AMLI 调试器。

**d\[b | w | d |\] \[ \[l =** <em>长度</em> **\] \[** *方法* **|  \[ %% \]** <em>地址</em> **\] \]**

**电子\[ %% \]** <em>解决 Datalist</em>

<span id="b"></span><span id="B"></span>**b**  
指定应以字节为单位显示数据。

<span id="w"></span><span id="W"></span>**w**  
指定应以 word （16 位） 为单位显示数据。

<span id="d"></span><span id="D"></span>**d**  
指定应以 DWORD （32 位） 为单位显示数据。

<span id="a"></span><span id="A"></span>**a**  
指定数据，应显示为一个字符串。 数据显示为 ASCII 字符。 显示终止 NULL 字符读取时，或当*长度*在显示字符。

<span id="Length"></span><span id="length"></span><span id="LENGTH"></span>*长度*  
指定要显示的字节数。 *长度*必须是十六进制数 (而无需**0x**前缀)。 如果*长度*是省略，默认显示大小为 0x80 字节。

<span id="Method"></span><span id="method"></span><span id="METHOD"></span>*方法*  
指定完整路径和方法的名称。 显示将在此方法的内存位置的开始处启动。

<span id="Address"></span><span id="address"></span><span id="ADDRESS"></span>*Address*  
指定将开始读取或写入的内存地址。 如果地址前缀为两个百分号 ( **%%** )，它被解释为物理地址。 否则，它被解释为一个虚拟地址。

<span id="DataList"></span><span id="datalist"></span><span id="DATALIST"></span>*DataList*  
指定要写入到内存的数据。 在列表中的每个项可以是一个十六进制字节或字符串。 使用字符串时，它必须括在引号中。 应由空格分隔多个项。

### <a name="span-idaccessingportsspanspan-idaccessingportsspanaccessing-ports"></a><span id="accessing_ports"></span><span id="ACCESSING_PORTS"></span>访问端口

端口命令可用于将输出发送或接收来自一个数据端口的输入。 **我**并**o**命令传输单字节**iw**并**ow**命令传输单词 （16 位） 和**id**并**od**命令传输 DWORD （32 位）。

这些命令具有相同的效果标准内核调试程序端口命令;它们被复制在轻松访问 AMLI 调试器。

**我***端口*

**信息工作者***端口*

**id** *端口*

**o** *Port* *DataForPort*

**ow** *Port* *DataForPort*

**od** *Port* *DataForPort*

<span id="Port"></span><span id="port"></span><span id="PORT"></span>*端口*  
指定要访问的端口地址。 端口大小必须与匹配选择的命令。

<span id="DataForPort"></span><span id="dataforport"></span><span id="DATAFORPORT"></span>*DataForPort*  
指定要写入端口的数据。 此数据的大小必须与匹配选择的命令。

### <a name="span-iddisplayinghelpspanspan-iddisplayinghelpspandisplaying-help"></a><span id="displaying_help"></span><span id="DISPLAYING_HELP"></span>显示帮助

此命令显示 AMLI 调试器命令的帮助文本。

**？\[** <em>命令</em> **\]**

<span id="Command"></span><span id="command"></span><span id="COMMAND"></span>*命令*  
指定要为其显示帮助的命令。 如果省略此属性，将显示所有 AMLI 调试器命令和 AMLI 调试器扩展的列表。

## <a name="see-also"></a>请参阅

[AMLI 调试器](the-amli-debugger.md) 
