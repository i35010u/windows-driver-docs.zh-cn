---
title: E （Windows 调试器词汇表）
description: 术语表页-E
Robots: noindex, nofollow
ms.assetid: 1e32bd40-8c77-4c6b-913c-6ec26707ed36
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb7fe4c28beb6985435d191da4eb8370843d77c7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378481"
---
# <a name="e"></a>E


<span id="effective_processor_type"></span><span id="EFFECTIVE_PROCESSOR_TYPE"></span>**有效的处理器类型**  
在调试器中的处理器类型使用时面对的目标计算机。 有效的处理器类型会影响调试器设置断点，访问寄存器、 获取堆栈跟踪和方式执行其他特定于处理器的操作。

<span id="engine"></span><span id="ENGINE"></span>**engine**  
请参阅调试器引擎。

<span id="event"></span><span id="EVENT"></span>**event**  
调试器引擎监视一些其目标中发生的事件。 其中包括触发断点、 异常、 线程和进程创建、 加载的模块和内部调试器引擎的更改。

<span id="event_filter"></span><span id="EVENT_FILTER"></span>**事件筛选器**  
影响调试器引擎如何进行后在目标中已发生事件的规则的集合。 有三种类型的事件筛选器： 特定的事件筛选器、 特定的异常筛选器和任意异常筛选器。

<span id="event_callback_objects"></span><span id="EVENT_CALLBACK_OBJECTS"></span>**事件的回调对象**  
实例[IDebugEventCallbacks](https://msdn.microsoft.com/library/windows/hardware/ff550550)接口并已注册到客户端。 每次事件发生时，引擎会通知事件回调。

<span id="event_callbacks"></span><span id="EVENT_CALLBACKS"></span>**事件的回调**  
请参阅事件回调对象。

<span id="event_process"></span><span id="EVENT_PROCESS"></span>**事件进程**  
最后一个事件发生过程。

<span id="event_target"></span><span id="EVENT_TARGET"></span>**事件目标**  
为其发生的最后一个事件的目标。

<span id="event_thread"></span><span id="EVENT_THREAD"></span>**事件线程**  
为其发生的最后一个事件的线程。

<span id="executing_processor_type"></span><span id="EXECUTING_PROCESSOR_TYPE"></span>**正在执行的处理器类型**  
当前处理器上下文中的处理器的类型。

<span id="exception"></span><span id="EXCEPTION"></span>**exception**  
错误条件，从而从特定的计算机指令的执行或目标，该值指示它遇到了错误。 异常可以是硬件或软件相关的错误。

例外情况是，通过标识其。

<span id="exception_code"></span><span id="EXCEPTION_CODE"></span>**异常代码**  
确定类型的异常事件的标识符。

<span id="exception_filter"></span><span id="EXCEPTION_FILTER"></span>**异常筛选器**  
指定的异常代码的异常事件的事件筛选器。

<span id="extension"></span><span id="EXTENSION"></span>**extension**  
查看调试器扩展。

<span id="extension_command"></span><span id="EXTENSION_COMMAND"></span>**扩展命令**  
查看调试器扩展。

 

 





