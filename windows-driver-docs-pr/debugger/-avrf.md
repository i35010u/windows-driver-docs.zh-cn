---
title: avrf
description: Avrf 扩展控制应用程序验证工具的设置，并显示应用程序验证工具生成的各种输出。
keywords:
- avrf Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- avrf
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a9fac44e64e2f406a8a929979f3029156cdc4ffa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799995"
---
# <a name="avrf"></a>!avrf


**！ Avrf** extension 控制 [应用程序验证工具](../devtest/application-verifier.md)的设置，并显示应用程序验证工具生成的各种输出。

```dbgcmd
    !avrf
    !avrf -vs { Length | -a Address }
    !avrf -hp { Length | -a Address }
    !avrf -cs { Length | -a Address }
    !avrf -dlls [ Length ]
    !avrf -trm
    !avrf -ex [ Length ] 
    !avrf -threads [ ThreadID ]
    !avrf -tp [ ThreadID ]
    !avrf -srw  [ Address | Address Length ] [ -stats ]
    !avrf -leak  [ -m ModuleName] [ -r ResourceType] [ -a Address ] [ -t ]
    !avrf -trace TraceIndex 
    !avrf -cnt
    !avrf -brk [BreakEventType]  
    !avrf -flt [EventType Probability] 
    !avrf -flt break EventType 
    !avrf -flt stacks Length 
    !avrf -trg [ Start End | dll Module | all ] 
    !avrf -settings 
    !avrf -skp [ Start End | dll Module | all | Time ] 
```

## <a name="span-idddk__avrf_dbgspanspan-idddk__avrf_dbgspanparameters"></a><span id="ddk__avrf_dbg"></span><span id="DDK__AVRF_DBG"></span>参数


<span id="-vs___Length___-a_Address__"></span><span id="-vs___length___-a_address__"></span><span id="-VS___LENGTH___-A_ADDRESS__"></span>**-vs {** *Length* **\| -a** *Address* **}**  
显示虚拟空间操作日志。 *Length* 指定要显示的记录数，从最新值开始。 *Address* 指定虚拟地址。 将显示包含此虚拟地址的虚拟操作的记录。

<span id="-hp___Length___-a_Address__"></span><span id="-hp___length___-a_address__"></span><span id="-HP___LENGTH___-A_ADDRESS__"></span>**-hp {** *长度* **\| -a** *地址* **}**  
显示堆操作日志。 *Address* 指定堆地址。 将显示包含此堆地址的堆操作的记录。

<span id="-cs___Length___-a_Address__"></span><span id="-cs___length___-a_address__"></span><span id="-CS___LENGTH___-A_ADDRESS__"></span>**-cs {** *长度* **\| -a** *地址* **}**  
显示临界区删除日志。 *Length* 指定要显示的记录数，从最新值开始。 *Address* 指定关键部分地址。 指定 *Address* 时，将显示特定关键部分的记录。

<span id="-dlls___Length__"></span><span id="-dlls___length__"></span><span id="-DLLS___LENGTH__"></span>**-dll \[***长度***\]**  
显示 DLL 加载/卸载日志。 *Length* 指定要显示的记录数，从最新值开始。

<span id="-trm"></span><span id="-TRM"></span>**-trm**  
显示所有终止和暂停的线程的日志。

<span id="-ex___Length__"></span><span id="-ex___length__"></span><span id="-EX___LENGTH__"></span>**-ex \[***长度***\]**  
显示异常日志。 应用程序验证工具跟踪应用程序中的所有异常。

<span id="-threads___ThreadID__"></span><span id="-threads___threadid__"></span><span id="-THREADS___THREADID__"></span>**-threads \[***ThreadID***\]**  
显示有关目标进程中的线程的信息。 对于子线程，还会显示由父级指定的堆栈大小和 **CreateThread** 标志。 如果提供线程 ID，则只显示该线程的信息。

<span id="-tp___ThreadID___"></span><span id="-tp___threadid___"></span><span id="-TP___THREADID___"></span>**-tp \[***ThreadID***\]**   
显示 threadpool 日志。 此日志包含各种操作的堆栈跟踪，例如更改线程关联掩码、更改线程优先级、发布线程消息以及从线程池回调内初始化或取消初始化 COM。 如果提供线程 ID，则仅显示该线程的信息。

<span id="-srw____Address___Address_Length_____-stats___"></span><span id="-srw____address___address_length_____-stats___"></span><span id="-SRW____ADDRESS___ADDRESS_LENGTH_____-STATS___"></span>**-srw \[***地址* **\|***地址长度* **\] \[ -统计 \]** 信息   
 (SRW) 日志中显示超薄读卡器/写入器。 如果指定 *address*，则会显示该地址处的 SRW 锁的记录。 如果指定 *address* 和 *Length*，则会显示该地址范围内的 SRW 锁的记录。 如果包括 **-stats** 选项，则显示 SRW 锁统计信息。

<span id="-leak___-m_ModuleName____-r_ResourceType____-a_Address_____-t___"></span><span id="-leak___-m_modulename____-r_resourcetype____-a_address_____-t___"></span><span id="-LEAK___-M_MODULENAME____-R_RESOURCETYPE____-A_ADDRESS_____-T___"></span>**-泄漏 \[ -m** <em>ModuleName</em> -**\] \[ r** <em>ResourceType</em> **\] \[ -a** *Address* **\] \[ -t \]**   
显示 "未完成的资源" 日志。 这些资源可能会在任何给定点泄露，也可能不会泄漏。 如果指定 *Modulename* (包括扩展) ，则将显示指定模块中的所有未处理资源。 如果指定 *ResourceType*，将显示该资源类型的所有未处理资源。 如果指定 " *地址*"，则会显示该地址的未处理资源的记录。 *ResourceType* 可以是以下项之一：

堆：使用 Win32 堆 Api 显示堆分配

Local：显示本地/全局分配

CRT：使用 CRT Api 显示分配

虚拟：显示虚拟保留

BSTR：显示 BSTR 分配

注册表：显示注册表项打开

Power：显示电源通知对象

处理：显示线程、文件和事件句柄分配

<span id="-trace_TraceIndex"></span><span id="-trace_traceindex"></span><span id="-TRACE_TRACEINDEX"></span>**-trace** *TraceIndex* 为指定的跟踪索引显示堆栈跟踪。 某些结构使用此16位索引号来标识堆栈跟踪。 此索引指向 stack 跟踪数据库中的某个位置。

<span id="-cnt"></span><span id="-CNT"></span>**-cnt** 显示全局计数器列表。

<span id="-brk___BreakEventType__"></span><span id="-brk___breakeventtype__"></span><span id="-BRK___BREAKEVENTTYPE__"></span>**-brk \[***BreakEventType* **\]** 指定中断事件。 *BreakEventType* 是中断事件的类型号。 有关可能的类型的列表以及当前中断事件设置的列表，请输入 **！ avrf-brk**。

<span id="-flt___EventType_Probability__"></span><span id="-flt___eventtype_probability__"></span><span id="-FLT___EVENTTYPE_PROBABILITY__"></span>**-flt \[***事件的概率* **\]** 指定错误注入。 *事件类型是事件* 的类型号。 *概率* 是事件失败的频率。 这可以是0到1000000之间的任意整数 (0xF4240) 。 如果输入 **！ avrf-flt** ，但没有其他参数，则会显示当前的错误注入设置。

<span id="-flt_break_EventType"></span><span id="-flt_break_eventtype"></span><span id="-FLT_BREAK_EVENTTYPE"></span>-**flt 中断***事件* 可能导致每次注入由 *事件* 行指定的错误时，应用程序验证工具进入调试器。

<span id="-flt_stacks_Length"></span><span id="-flt_stacks_length"></span><span id="-FLT_STACKS_LENGTH"></span>**-flt** stack *length* 显示最新的故障插入操作的堆栈跟踪的 *长度* 。

<span id="-trg___Start_End___dll_Module___all____"></span><span id="-trg___start_end___dll_module___all____"></span><span id="-TRG___START_END___DLL_MODULE___ALL____"></span>**-.trg \[***开始结束* **\| dll** *模块* **\| all \]** 指定了目标范围。 *起始* 地址是目标范围的起始地址。 *结束* 是目标范围的结束地址。 *模块* 指定名称 (包括 .exe 或 .dll 扩展名，但不包括要以其为目标的模块的路径) 。 如果输入 **-.trg all**，则将重置所有目标范围。 如果输入 **-.trg** ，但没有其他参数，则会显示当前的目标范围。

<span id="-skp___Start_End___dll_Module___all___Time____"></span><span id="-skp___start_end___dll_module___all___time____"></span><span id="-SKP___START_END___DLL_MODULE___ALL___TIME____"></span>**-skp \[***开始结束* **\| dll** *模块* **\| 所有 \|** *时间* **\]** 指定排除范围。 *起始* 地址是排除范围的起始地址。 *结尾* 是排除范围的结束地址。 Module 指定要以其为目标或排除的模块的名称。 *模块* 指定包含 .exe 或 .dll 扩展名 (名称，但不包括要排除的模块的路径) 。 如果输入 **-skp all**，则将重置所有目标范围或排除范围。 如果输入 *时间* 值，则在执行恢复后，将抑制所有错误的 *时间* 毫秒。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

exts.dll

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关如何下载和安装应用程序验证工具及其文档的信息，请参阅 [应用程序验证工具](../devtest/application-verifier.md)。

<a name="remarks"></a>备注
-------

如果使用不带参数的 **！ avrf** 扩展，则将显示当前应用程序验证工具选项。 如果已启用 **整页堆** 或 **快速填充堆** 选项，则还会显示有关活动页堆的信息。 有关一些示例，请参阅应用程序验证工具文档中的 "堆操作日志"。

如果应用程序验证工具停止，则不带参数的 **！ avrf** 扩展将显示 Stop 的性质及其原因。 有关一些示例，请参阅应用程序验证工具文档中的 "调试应用程序验证工具停止"。

如果缺少 ntdll.dll 和 verifier.dll 的符号， **！ avrf** 扩展将生成错误消息。 有关如何解决此问题的信息，请参阅应用程序验证工具文档中的 "为应用程序验证工具设置调试程序"。
