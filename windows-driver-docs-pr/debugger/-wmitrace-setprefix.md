---
title: wmitrace.setprefix
description: Wmitrace. setprefix 扩展指定从此会话跟踪消息前面预置的跟踪消息前缀。
ms.assetid: 8712af44-f231-48f6-97ac-56a1d737cd6b
keywords:
- wmitrace setprefix Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.setprefix
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b93c586578e5e20efd498f0ac301c4a721e76975
ms.sourcegitcommit: ee1fc949d1ae5eb14df4530758f767702a886e36
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2019
ms.locfileid: "71164785"
---
# <a name="wmitracesetprefix"></a>!wmitrace.setprefix


**！ Wmitrace。 setprefix**扩展指定从此会话跟踪消息前面预置的跟踪消息前缀。 此扩展允许您在调试会话期间更改前缀。

```dbgcmd
!wmitrace.setprefix [+] PrefixVariables 
!wmitrace.setprefix 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="______________"></span> **+**    
导致*PrefixVariables*追加到跟踪消息前缀。 如果未 **+** 使用该令牌，则*PrefixVariables*将替换现有的跟踪消息前缀。

<span id="_______PrefixVariables______"></span><span id="_______prefixvariables______"></span><span id="_______PREFIXVARIABLES______"></span>*PrefixVariables*   
指定跟踪消息前缀中的格式和数据的一组变量。

变量的格式为% n！ x！，其中% n 表示数据字段，！ x！ 表示数据类型。 还可以包括分隔字符，如冒号（:)、分号（;)、括号（（））、大括号（{}）和方括号（ \[ \] ），以分隔字段。

每个% n 变量都表示一个参数，下表对此进行了说明。

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
<td align="left"><p>跟踪消息的消息 GUID 的友好名称。 默认情况下，消息 GUID 的友好名称是在其中生成跟踪提供程序的目录的名称。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%2</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>源文件和行号。</p>
<p>此变量表示跟踪消息的友好名称。 默认情况下，跟踪消息的友好名称是源文件的名称和生成跟踪消息的代码的行号。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%3</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>线程 ID。</p>
<p>标识生成跟踪消息的线程。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%4</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>生成跟踪消息的时间的时间戳。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>% 5</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>内核时间。</p>
<p>显示生成跟踪消息时内核模式指令的已用执行时间（以 CPU 刻度为单位）。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%6</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>用户时间。</p>
<p>显示生成跟踪消息时用户模式指令的已用执行时间（以 CPU 刻度为单位）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%7</p></td>
<td align="left"><p>漫长</p></td>
<td align="left"><p>序列号。</p>
<p>显示跟踪消息的本地序列号或全局序列号。 默认情况下，仅在此跟踪会话中唯一的本地序列号为默认值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%8</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>进程 ID。</p>
<p>标识生成跟踪消息的进程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%9</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>CPU 号。</p>
<p>标识生成跟踪消息的 CPU。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%!求!</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>函数名称。</p>
<p>显示生成跟踪消息的函数的名称。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%!随意</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>显示启用跟踪消息的跟踪标志的名称。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%!调配!</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>显示启用跟踪消息的跟踪级别的值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%!COMPNAME!</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>组件名称。</p>
<p>显示生成跟踪消息的提供程序组件的名称。 仅当在跟踪代码中指定组件名称时，才会显示该组件名称。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%!SUBCOMP!</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>子组件名称。</p>
<p>显示生成跟踪消息的提供程序的子组件的名称。 仅当在跟踪代码中指定子组件名称时，才会显示子组件名称。</p></td>
</tr>
</tbody>
</table>

 

感叹号内的符号是一个转换字符，用于指定变量的格式和精度。 例如，% 8！04X！ 指定格式化为四位数、无符号十六进制数的进程 ID。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

此扩展由 Wmitrace 导出。

此扩展在 windows 2000 和更高版本的 Windows 中可用。 如果要将此扩展与 Windows 2000 一起使用，必须先将 Wmitrace 文件从 Windows 的调试工具的 winxp 子目录复制到 w2kfre 子目录。

### <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>实例

以下命令将调试器输出中的跟踪消息前缀更改为以下格式：

**！ wmitrace. setprefix% 2！ s！：%！FUNC！：% 8！04x！。% 3！04x！：% 4！ s！：**

此扩展命令将跟踪消息前缀设置为以下格式：

*SourceFile\_LineNumber：FunctionNameProcessID. ThreadID：SystemTime*

因此，将使用指定的格式为跟踪消息预置指定的信息。 下面的代码示例取自 WDK 中 Tracedrv 示例驱动程序的跟踪。

```dbgcmd
tracedrv_c258: TracedrvDispatchDeviceControl: 0af4.0c64: 07/25/2003-13:55:39.998:  IOCTL = 1
```

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关事件跟踪的概念性概述，请参阅 Microsoft Windows SDK 文档。 有关跟踪消息格式化文件的信息，请参阅 WDK 文档中的 "跟踪消息前缀" 主题。

<a name="remarks"></a>备注
-------

当与没有参数一起使用时， **！ wmitrace**显示跟踪消息前缀的当前值。

*跟踪消息前缀*包含有关跟踪消息的数据，这些数据在 Windows 软件跟踪预处理器（WPP）软件跟踪过程中预置到每个跟踪消息。 此数据源自跟踪日志（.etl）文件和跟踪消息格式（. tmf）文件。 您可以自定义跟踪消息前缀中的格式和数据。

默认跟踪消息前缀如下：

```dbgcmd
[%9!d!]%8!04X!.%3!04X!::%4!s! [%1!s!]
```

和生成以下前缀：

```dbgcmd
[CPUNumber]ProcessID.ThreadID::SystemTime [ProviderDirectory] 
```

可以通过设置% trace\_format\_prefix% 环境变量来更改调试器外部跟踪消息前缀中的格式和数据。 有关演示如何在调试器外设置跟踪消息前缀的示例，请参阅 "示例7：在 Windows 驱动程序工具包（WDK）文档中自定义跟踪消息前缀。 如果消息的跟踪消息前缀不同于默认值，则可能会在计算机上设置此环境变量。

使用此扩展命令设置的前缀仅影响调试器输出。 跟踪日志中显示的跟踪消息前缀由默认值和% 跟踪\_格式\_前缀% 环境变量的值确定。

此扩展仅适用于 WPP 软件跟踪和 Windows 事件跟踪的早期（旧）方法。 其他类提供程序生成的跟踪事件不使用跟踪消息格式（TMF）文件，因此此扩展不会影响它们。

 

 





