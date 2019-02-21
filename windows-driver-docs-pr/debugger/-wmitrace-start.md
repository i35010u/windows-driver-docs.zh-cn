---
title: wmitrace.start
description: Wmitrace.start 扩展启动目标计算机上的事件跟踪 Windows (ETW) 记录器。
ms.assetid: 52ed0c5a-6ca9-4890-bae5-54394bc43d51
keywords:
- wmitrace.start Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.start
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9203a4cfd30c71f844713cd7b3068f8bdc3e9c0d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545332"
---
# <a name="wmitracestart"></a>!wmitrace.start


**！ Wmitrace.start**扩展启动目标计算机上的事件跟踪 Windows (ETW) 记录器。

```dbgcmd
!wmitrace.start LoggerName [-cir Size | -seq Size] [-f File] [-b Size] [-max Num] [-min Num] [-kd] [-ft Time] 
```

## <a name="span-idddkwmitracestrdumpdbgspanspan-idddkwmitracestrdumpdbgspanparameters"></a><span id="ddk__wmitrace_strdump_dbg"></span><span id="DDK__WMITRACE_STRDUMP_DBG"></span>参数


<span id="_______LoggerName______"></span><span id="_______loggername______"></span><span id="_______LOGGERNAME______"></span> *LoggerName*   
提供要用于跟踪会话的名称。 *LoggerName*不能包含空格或引号。

<span id="_______-cir_______Size______"></span><span id="_______-cir_______size______"></span><span id="_______-CIR_______SIZE______"></span> **-cir** *Size*   
导致要以循环方式编写的日志文件。 *大小*指定最大文件大小，以字节为单位。 当文件达到此长度时，则新的数据将写入到文件中以循环方式，覆盖从开头到末尾的文件。 这不能结合 **-seq**参数。 如果既没有 **-cir**也不 **-seq**文件写入在缓冲模式下的指定。

<span id="_______-seq_______Num______"></span><span id="_______-seq_______num______"></span><span id="_______-SEQ_______NUM______"></span> **-seq** *Num*   
导致要以顺序方式编写的日志文件。 *大小*指定最大文件大小，以字节为单位。 当文件达到此长度时，则新数据追加到末尾时，从该文件的开头将删除最旧的数据。 这不能结合 **-cir**参数。 如果既没有 **-cir**也不 **-seq**文件写入在缓冲模式下的指定。

<span id="_______-f_______File______"></span><span id="_______-f_______file______"></span><span id="_______-F_______FILE______"></span> **-f** *File*   
指定要在目标计算机上创建的日志文件的名称。 *文件*必须包括一个绝对目录路径，并且不能包含空格或引号。

<span id="_______-b_______Size______"></span><span id="_______-b_______size______"></span><span id="_______-B_______SIZE______"></span> **-b** *Size*   
指定每个缓冲区的大小以千字节为单位。 允许范围*大小*介于 1 和 2048，非独占。

<span id="_______-max_______Num______"></span><span id="_______-max_______num______"></span><span id="_______-MAX_______NUM______"></span> **-max** *Num*   
指定要使用缓冲区最大的数目。 *Num*可以是任何正整数。

<span id="_______-min_______Num______"></span><span id="_______-min_______num______"></span><span id="_______-MIN_______NUM______"></span> **-min** *Num*   
指定要使用缓冲区最小的数目。 *Num*可以是任何正整数。

<span id="_______-kd______"></span><span id="_______-KD______"></span> **-kd**   
启用 KD 筛选器模式。 将发送到内核调试程序并在屏幕上显示的消息。

<span id="_______-ft_______Time______"></span><span id="_______-ft_______time______"></span><span id="_______-FT_______TIME______"></span> **-ft** *Time*   
以秒为单位指定刷新计时器的持续的时间。 从开始 Windows 8 中，您可以指定刷新计时器持续时间以毫秒为单位通过追加**ms**到*时间*值。 例如， **-ft 100ms**。

**请注意**  如果你在 KD 筛选器模式下启动跟踪会话 (**-kd**)，以显示目标计算机上的跟踪缓冲区发送到主机计算机上的调试器。 此参数指定目标计算机上的缓冲区何种频率刷新并发送到主计算机。

 

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

此扩展插件导出的 Wmitrace.dll。

此扩展是在 Windows 7 和更高版本的 Windows 中可用。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

此扩展的参数的更多详细信息，请参阅[StartTrace 函数](https://go.microsoft.com/fwlink/p/?linkid=139652)并[事件\_跟踪\_属性](https://go.microsoft.com/fwlink/p/?linkid=139653)。 事件跟踪的概念概述，请参阅 Microsoft Windows SDK。 有关跟踪工具的信息，请参阅 Windows Driver Kit (WDK)。

<a name="remarks"></a>备注
-------

使用此扩展插件之后, 必须继续执行程序 (例如，通过使用[ **g （转向）** ](g--go-.md)命令)，使其生效。 在很短的时间之后, 目标计算机自动进入调试器再次中断。

当启动跟踪会话时，系统将其分配了一个序号 (*记录器 ID*)。 然后，会话可以引用到通过记录器名称或记录器 id。

若要停止 ETW 记录器，请使用[ **！ wmitrace.stop**](-wmitrace-stop.md)。

 

 





