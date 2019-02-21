---
title: avrf
description: Avrf 扩展控制应用程序验证器的设置，并显示各种应用程序验证工具生成输出。
ms.assetid: e9313954-a1fa-45a9-bc1a-78be2451f5aa
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
ms.openlocfilehash: eb452ca2be00cdeca72cc168c28585d617d31069
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543091"
---
# <a name="avrf"></a>!avrf


**！ Avrf**扩展控制的设置[应用程序验证工具](application-verifier.md)并显示各种应用程序验证工具生成输出。

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

## <a name="span-idddkavrfdbgspanspan-idddkavrfdbgspanparameters"></a><span id="ddk__avrf_dbg"></span><span id="DDK__AVRF_DBG"></span>参数


<span id="-vs___Length___-a_Address__"></span><span id="-vs___length___-a_address__"></span><span id="-VS___LENGTH___-A_ADDRESS__"></span>**-与 {** *长度* **|-a** *地址* **}**  
显示虚拟空间操作日志。 *长度*指定要显示的记录数最新的启动。 *地址*指定的虚拟地址。 显示包含此虚拟地址的虚拟操作记录。

<span id="-hp___Length___-a_Address__"></span><span id="-hp___length___-a_address__"></span><span id="-HP___LENGTH___-A_ADDRESS__"></span>**-hp {** *长度* **|-a** *地址* **}**  
显示堆操作日志。 *地址*指定堆地址。 显示包含此堆地址堆操作的记录。

<span id="-cs___Length___-a_Address__"></span><span id="-cs___length___-a_address__"></span><span id="-CS___LENGTH___-A_ADDRESS__"></span>**-cs {** *长度* **|-a** *地址* **}**  
显示关键部分删除日志。 *长度*指定要显示的记录数最新的启动。 *地址*指定关键部分地址。 显示特定的关键部分的记录时*地址*指定。

<span id="-dlls___Length__"></span><span id="-dlls___length__"></span><span id="-DLLS___LENGTH__"></span>**-dll \[**  *长度* **\]**  
显示的 DLL 加载/卸载日志。 *长度*指定要显示的记录数最新的启动。

<span id="-trm"></span><span id="-TRM"></span>**-trm**  
显示所有已终止或挂起线程的日志。

<span id="-ex___Length__"></span><span id="-ex___length__"></span><span id="-EX___LENGTH__"></span>**-ex \[**  *长度* **\]**  
显示的异常日志。 应用程序验证工具跟踪应用程序中的所有异常。

<span id="-threads___ThreadID__"></span><span id="-threads___threadid__"></span><span id="-THREADS___THREADID__"></span>**-线程\[**  *ThreadID* **\]**  
显示有关目标进程中线程的信息。 对于子线程，堆栈大小， **CreateThread**也会显示在父级指定的标志。 如果你提供线程 ID，将显示仅该线程的信息。

<span id="-tp___ThreadID___"></span><span id="-tp___threadid___"></span><span id="-TP___THREADID___"></span>**-tp \[** *ThreadID* **\]**   
显示线程池日志。 此日志包含各种操作，如更改线程关联掩码，更改线程优先级、 发布线程消息和正在初始化或取消 COM 从线程池回调中的堆栈跟踪。 如果提供线程 ID，该线程只被显示信息。

<span id="-srw____Address___Address_Length_____-stats___"></span><span id="-srw____address___address_length_____-stats___"></span><span id="-SRW____ADDRESS___ADDRESS_LENGTH_____-STATS___"></span>**-srw \[**  *地址* **|** *地址长度*  **\] \[的统计信息 \]**   
显示 Slim 读取器/编写器 (SRW) 日志。 如果指定*地址*，SRW 锁在该地址的记录显示。 如果指定*地址*并*长度*，SRW 锁，因为地址范围显示记录。 如果包括**的统计信息**选项，SRW 锁显示统计信息。

<span id="-leak___-m_ModuleName____-r_ResourceType____-a_Address_____-t___"></span><span id="-leak___-m_modulename____-r_resourcetype____-a_address_____-t___"></span><span id="-LEAK___-M_MODULENAME____-R_RESOURCETYPE____-A_ADDRESS_____-T___"></span>**-leak \[ -m** <em>ModuleName</em>**\] \[ -r** <em>ResourceType</em>**\] \[ -a** *Address* **\] \[ -t \]**   
显示未完成的资源日志。 这些资源可能会或可能不是在任意给定时间的泄漏。 如果指定*Modulename* （包括扩展名），将显示在指定的模块中所有未完成的资源。 如果指定*ResourceType*，将显示该资源类型的所有未完成的资源。 如果指定*地址*，显示与该地址的未完成资源记录。 *ResourceType*可以是以下之一：

堆：显示使用堆的 Win32 Api 的堆分配

本地：显示本地/全局分配

CRT:显示分配使用 CRT Api

虚拟：显示虚拟保留项

BSTR:显示 BSTR 分配

注册表：此时将打开显示注册表项

电源：显示电源通知对象

句柄：显示线程、 文件和事件处理分配

<span id="-trace_TraceIndex"></span><span id="-trace_traceindex"></span><span id="-TRACE_TRACEINDEX"></span>**-跟踪** *TraceIndex*显示指定的跟踪索引的堆栈跟踪。 一些结构使用此 16 位索引号来标识堆栈跟踪。 此索引指向堆栈跟踪数据库中的位置。

<span id="-cnt"></span><span id="-CNT"></span>**-cnt**显示全局计数器的列表。

<span id="-brk___BreakEventType__"></span><span id="-brk___breakeventtype__"></span><span id="-BRK___BREAKEVENTTYPE__"></span>**-brk \[**  *BreakEventType* **\]** 指定中断事件。 *BreakEventType*是中断事件的类型数。 对于可能类型的列表以及当前的中断事件设置的列表，请输入 **！ avrf brk**。

<span id="-flt___EventType_Probability__"></span><span id="-flt___eventtype_probability__"></span><span id="-FLT___EVENTTYPE_PROBABILITY__"></span>**-flt \[**  *EventType 概率* **\]** 指定错误注入。 *EventType*是事件的类型的数字。 *概率*将失败事件的频率。 这可以是介于 0 到 1000000 (0xF4240) 之间的任何整数。 如果输入 **！ avrf flt**当前故障注入设置显示不带任何其他参数。

<span id="-flt_break_EventType"></span><span id="-flt_break_eventtype"></span><span id="-FLT_BREAK_EVENTTYPE"></span>-**flt 中断** *EventType*会导致应用程序验证器以在每个调试器中中断时间通过指定此错误*EventType*，注入。

<span id="-flt_stacks_Length"></span><span id="-flt_stacks_length"></span><span id="-FLT_STACKS_LENGTH"></span>**-flt 堆栈***长度*显示*长度*数的最新的故障注入操作的堆栈跟踪。

<span id="-trg___Start_End___dll_Module___all____"></span><span id="-trg___start_end___dll_module___all____"></span><span id="-TRG___START_END___DLL_MODULE___ALL____"></span>**-/{trg \[**  *开始最终* **| dll** *模块* **| 所有\]** 指定的目标范围。 *启动*是目标范围的起始地址。 *结束*是目标范围的结束地址。 *模块*指定名称 （包括.exe 或.dll 扩展名，但不是包括路径） 的模块将作为目标。 如果输入 **/{trg-所有**，所有的目标范围将重置。 如果输入 **-/{trg**不带任何其他参数，显示当前的目标范围。

<span id="-skp___Start_End___dll_Module___all___Time____"></span><span id="-skp___start_end___dll_module___all___time____"></span><span id="-SKP___START_END___DLL_MODULE___ALL___TIME____"></span>**-skp \[**  *开始最终* **| dll** *模块* **| 所有 |***时间* **\]** 指定排除范围。 *启动*是排除范围的起始地址。 *结束*是排除范围的结束地址。 模块指定要在目标或排除的模块的名称。 *模块*指定名称 （包括.exe 或.dll 扩展名，但不是包括路径） 的要排除的模块。 如果输入**skp-所有**、 所有目标范围或排除范围被重置。 如果输入*时间*值，所有错误的都禁止*时间*毫秒后执行将继续。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

exts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关如何下载和安装应用程序验证程序和其文档的信息，请参阅[应用程序验证工具](application-verifier.md)。

<a name="remarks"></a>备注
-------

当 **！ avrf**扩展使用不带任何参数，则会显示当前的应用程序验证工具选项。 如果**整页堆**或**快速填充堆**启用选项、 堆是活动页有关的信息也显示。 一些示例，请参阅应用程序验证工具文档中的"堆操作日志"。

如果应用程序验证工具停止发生，请 **！ avrf**不带任何参数的扩展将显示的性质停止以及其原因。 一些示例，请参阅应用程序验证工具文档中的"应用程序验证工具停止调试"。

如果缺少，ntdll.dll 和 verifier.dll 符号 **！ avrf**扩展插件可生成一条错误消息。 有关如何解决此问题的信息，请参阅应用程序验证工具文档中的"设置启动调试器的应用程序验证器"。

 

 





