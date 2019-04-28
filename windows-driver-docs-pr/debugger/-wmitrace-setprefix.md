---
title: wmitrace.setprefix
description: Wmitrace.setprefix 扩展指定可从此会话预置到跟踪消息的跟踪消息前缀。
ms.assetid: 8712af44-f231-48f6-97ac-56a1d737cd6b
keywords:
- wmitrace.setprefix Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.setprefix
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c04b8e2376d877c470ed651061a452e7fd5606ba
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348045"
---
# <a name="wmitracesetprefix"></a>!wmitrace.setprefix


**！ Wmitrace.setprefix**扩展指定可在此会话预置到跟踪消息的跟踪消息前缀。 该扩展允许您在调试会话期间更改的前缀。

```dbgcmd
!wmitrace.setprefix [+] PrefixVariables 
!wmitrace.setprefix 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="______________"></span> **+**   
将导致*PrefixVariables*为 apended 到跟踪消息前缀。 如果**+** 未使用令牌，则*PrefixVariables*替换现有的跟踪消息前缀。

<span id="_______PrefixVariables______"></span><span id="_______prefixvariables______"></span><span id="_______PREFIXVARIABLES______"></span> *PrefixVariables*   
指定的格式和数据中跟踪消息前缀的变量集。

变量具有格式 %n ！ x ！，其中 %n 表示一个数据字段和 ！ x ！ 表示数据类型。 您还可以包含分隔字符，例如冒号 （:）、 分号 （;）、 圆括号 （（））、 大括号 （{}） 和括号 ( \[ \] ) 分隔的字段。

每个 %n 变量表示下表中描述的参数。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">前缀变量标识符</th>
<th align="left">变量类型</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>%1</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>消息的跟踪消息的 GUID 的友好名称。 默认情况下，一条消息的 GUID 的友好名称是目录的在其中生成跟踪提供程序的名称。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%2</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>源文件和行号。</p>
<p>此变量表示的跟踪消息的友好名称。 默认情况下，跟踪消息的友好名称是代码的源文件和生成的跟踪消息的行号的名称。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%3</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>线程 id。</p>
<p>标识生成的跟踪消息的线程。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%4</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>生成的跟踪消息的时间的时间戳。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%5</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>内核时间。</p>
<p>在生成的跟踪消息的时间中 CPU 时钟周期数，显示内核模式的说明，已用的执行时间。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%6</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>用户时间。</p>
<p>在生成的跟踪消息的时间中 CPU 时钟周期数，显示用户模式下的说明，已用的执行时间。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%7</p></td>
<td align="left"><p>长</p></td>
<td align="left"><p>序列号。</p>
<p>显示跟踪消息的本地或全局序列号。 本地序列号，是仅对此跟踪会话唯一的这是默认值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%8</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>进程 id。</p>
<p>标识生成的跟踪消息的进程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%9</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>CPU 数。</p>
<p>标识在其生成的跟踪消息的 CPU。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%!FUNC!</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>函数名称。</p>
<p>显示生成的跟踪消息的函数的名称。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%!FLAGS%</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>显示启用跟踪消息的跟踪标志的名称。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%!级别 ！</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>显示启用跟踪消息的跟踪级别值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%!COMPNAME!</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>组件名称。</p>
<p>显示生成的跟踪消息的提供程序的组件的名称。 仅当指定的跟踪代码中，将显示该组件名称。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%!SUBCOMP!</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>子组件名称。</p>
<p>显示生成的跟踪消息的提供程序的子组件名称。 仅当指定的跟踪代码中，将显示子组件名称。</p></td>
</tr>
</tbody>
</table>

 

在感叹号符号是指定的格式和变量的精度的转换字符。 例如，%8 ！ 04x ！ 指定的进程 ID 格式化为一个四位数字、 无符号十六进制数字。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

此扩展插件导出的 Wmitrace.dll。

此扩展是在 Windows 2000 和更高版本的 Windows 中可用。 如果你想要 Windows 2000 中使用此扩展，您必须先将复制 Wmitrace.dll 文件的 Windows 调试工具安装目录的 winxp 子目录到 w2kfre 子目录。

### <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>示例

以下命令会调试器输出中的跟踪消息前缀更改为以下格式：

**！ wmitrace.setprefix %2 2!s ！: %！FUNC ！: %8 ！ 04x ！。%3 ！ 04x ！: %4 ！:**

此扩展命令跟踪消息前缀设置为以下格式：

*SourceFile\_行号：FunctionName:ProcessID.ThreadID:SystemTime:*

因此，跟踪消息前面带有指定的格式中的指定信息。 下面的代码示例摘自 Tracedrv 示例驱动程序 WDK 中的跟踪。

```dbgcmd
tracedrv_c258: TracedrvDispatchDeviceControl: 0af4.0c64: 07/25/2003-13:55:39.998:  IOCTL = 1
```

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

事件跟踪的概念概述，请参阅 Microsoft Windows SDK 文档。 有关跟踪消息格式化文件的信息，请参阅 WDK 文档中的"跟踪消息前缀"主题。

<a name="remarks"></a>备注
-------

使用不带任何参数时 **！ wmitrace.setprefix**显示跟踪消息前缀的当前值。

*跟踪消息前缀*包含 Windows 软件跟踪预处理器 (WPP) 软件跟踪过程预置到每条跟踪消息的跟踪消息有关的数据。 此数据有跟踪日志 (.etl) 文件和跟踪消息格式 (.tmf) 文件中。 您可以自定义格式和跟踪消息前缀中的数据。

默认跟踪消息前缀是按如下所示：

```dbgcmd
[%9!d!]%8!04X!.%3!04X!::%4!s! [%1!s!]
```

并生成以下前缀：

```dbgcmd
[CPUNumber]ProcessID.ThreadID::SystemTime [ProviderDirectory] 
```

您可以通过设置 %跟踪更改的格式和在调试器外的跟踪消息前缀中的数据\_格式\_前缀 %环境变量。 说明了如何设置在调试器外的跟踪消息前缀的示例，请参阅"示例 7:自定义的跟踪消息前缀"中的 Windows Driver Kit (WDK) 文档。 如果你的消息的跟踪消息前缀从默认值而异，可能会在计算机上设置此环境变量。

使用此扩展命令设置的前缀会影响仅调试程序输出。 默认值和 %跟踪的值来确定会出现在跟踪日志的跟踪消息前缀\_格式\_前缀 %环境变量。

此扩展在 WPP 软件跟踪和早期的 Windows 事件跟踪 （旧版） 方法期间才有用。 其他清单表示提供程序生成的跟踪事件不使用跟踪消息格式 (TMF) 文件，并因此，此扩展不影响它们。

 

 





