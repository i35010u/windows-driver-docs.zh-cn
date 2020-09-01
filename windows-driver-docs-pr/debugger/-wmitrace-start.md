---
title: wmitrace
description: Wmitrace 扩展在目标计算机上启动 Windows (ETW) 记录器的事件跟踪。
ms.assetid: 52ed0c5a-6ca9-4890-bae5-54394bc43d51
keywords:
- wmitrace Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.start
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 40163c87bed97186bd7e8eb77d64ae6741fc3426
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207675"
---
# <a name="wmitracestart"></a>!wmitrace.start


**！ Wmitrace**扩展将在目标计算机上启动 WINDOWS (ETW) 记录器的事件跟踪。

```dbgcmd
!wmitrace.start LoggerName [-cir Size | -seq Size] [-f File] [-b Size] [-max Num] [-min Num] [-kd] [-ft Time] 
```

## <a name="span-idddk__wmitrace_strdump_dbgspanspan-idddk__wmitrace_strdump_dbgspanparameters"></a><span id="ddk__wmitrace_strdump_dbg"></span><span id="DDK__WMITRACE_STRDUMP_DBG"></span>参数


<span id="_______LoggerName______"></span><span id="_______loggername______"></span><span id="_______LOGGERNAME______"></span>*LoggerName*   
提供用于跟踪会话的名称。 *LoggerName* 不能包含空格或引号。

<span id="_______-cir_______Size______"></span><span id="_______-cir_______size______"></span><span id="_______-CIR_______SIZE______"></span>**-cir** *大小*   
导致以循环方式写入日志文件。 *大小* 指定最大文件大小（以字节为单位）。 当文件达到此长度时，新数据将以循环方式写入文件，并从一开始就覆盖文件。 这不能与 **-seq** 参数组合在一起。 如果 **-cir** 和 **-seq** 均未指定，则文件将以缓冲模式写入。

<span id="_______-seq_______Num______"></span><span id="_______-seq_______num______"></span><span id="_______-SEQ_______NUM______"></span>**-seq** *Num*   
使日志文件以顺序写入。 *大小* 指定最大文件大小（以字节为单位）。 当文件达到此长度时，只要将新数据追加到末尾，就会从文件的开头删除最早的数据。 这不能与 **-cir** 参数结合。 如果 **-cir** 和 **-seq** 均未指定，则文件将以缓冲模式写入。

<span id="_______-f_______File______"></span><span id="_______-f_______file______"></span><span id="_______-F_______FILE______"></span>**-f** *文件*   
指定要在目标计算机上创建的日志文件的名称。 *文件* 必须包含绝对目录路径，并且不能包含空格或引号。

<span id="_______-b_______Size______"></span><span id="_______-b_______size______"></span><span id="_______-B_______SIZE______"></span>**-b** *大小*   
指定每个缓冲区的大小（以 kb 为单位）。 允许的 *大小* 范围介于1到2048（含）之间。

<span id="_______-max_______Num______"></span><span id="_______-max_______num______"></span><span id="_______-MAX_______NUM______"></span>**-最大***数目*   
指定要使用的最大缓冲区数。 *Num* 可以是任意正整数。

<span id="_______-min_______Num______"></span><span id="_______-min_______num______"></span><span id="_______-MIN_______NUM______"></span>**-最小** *Num*   
指定要使用的最小缓冲区数。 *Num* 可以是任意正整数。

<span id="_______-kd______"></span><span id="_______-KD______"></span>**-kd**   
启用 KD 筛选模式。 消息将发送到内核调试器，并显示在屏幕上。

<span id="_______-ft_______Time______"></span><span id="_______-ft_______time______"></span><span id="_______-FT_______TIME______"></span>**-ft** *时间*   
指定刷新计时器的持续时间（以秒为单位）。 从 Windows 8 开始，可以通过将 **ms** 追加到 *时间* 值来指定刷新计时器的持续时间（以毫秒为单位）。 例如， **-ft 100ms**。

**注意**   如果在 KD filter 模式下启动跟踪会话 (**-KD**) ，则目标计算机上的跟踪缓冲区将发送到主计算机上的调试程序以供显示。 此参数指定将目标计算机上的缓冲区刷新并发送到主计算机的频率。

 

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

此扩展由 Wmitrace.dll 导出。

Windows 7 和更高版本的 Windows 中提供了此扩展。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关此扩展的参数的更多详细信息，请参阅 [StartTraceA 函数](/windows/win32/api/evntrace/nf-evntrace-starttracea) 和 [事件 \_ 跟踪 \_ 属性](/windows/win32/api/evntrace/ns-evntrace-event_trace_properties)。 有关事件跟踪的概念性概述，请参阅 Microsoft Windows SDK。 有关跟踪工具的信息，请参阅 Windows 驱动程序工具包 (WDK) 。

<a name="remarks"></a>备注
-------

使用此扩展后，你必须继续执行程序 (例如，通过使用 [**g (转) **](g--go-.md) 命令) ，使其生效。 经过一段时间后，目标计算机会自动中断到调试器。

启动跟踪会话时，系统会为其分配一个序号 (*记录器 ID*) 。 然后，可以通过记录器名称或记录器 ID 引用会话。

若要停止 ETW 记录器，请使用 [**！ wmitrace**](-wmitrace-stop.md)。

 

