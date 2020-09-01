---
title: 'E (Windows 调试器词汇表) '
description: 词汇表页-E
ms.assetid: 1e32bd40-8c77-4c6b-913c-6ec26707ed36
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: af34d7eca3a721315dc1b1fdfa312bfc24ee7123
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207645"
---
# <a name="e"></a>E


<span id="effective_processor_type"></span><span id="EFFECTIVE_PROCESSOR_TYPE"></span>**有效处理器类型**  
调试器在处理目标计算机时使用的处理器类型。 有效的处理器类型会影响调试器设置断点、访问寄存器、获取堆栈跟踪以及执行其他特定于处理器的操作的方式。

<span id="engine"></span><span id="ENGINE"></span>**搜索引擎优化**  
请参阅调试器引擎。

<span id="event"></span><span id="EVENT"></span>**引发**  
调试器引擎监视其目标中发生的一些事件。 其中包括触发的断点、异常、线程和进程创建、模块加载以及内部调试器引擎更改。

<span id="event_filter"></span><span id="EVENT_FILTER"></span>**事件筛选器**  
影响在目标中发生事件后调试器引擎如何进行的规则的集合。 事件筛选器有三种类型：特定事件筛选器、特定异常筛选器和任意异常筛选器。

<span id="event_callback_objects"></span><span id="EVENT_CALLBACK_OBJECTS"></span>**事件回调对象**  
已向客户端注册的 [IDebugEventCallbacks](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugeventcallbacks) 接口的实例。 每当发生事件时，引擎都会通知事件回调。

<span id="event_callbacks"></span><span id="EVENT_CALLBACKS"></span>**事件回调**  
请参阅事件回调对象。

<span id="event_process"></span><span id="EVENT_PROCESS"></span>**事件进程**  
上次发生事件的进程。

<span id="event_target"></span><span id="EVENT_TARGET"></span>**事件目标**  
上次发生事件的目标。

<span id="event_thread"></span><span id="EVENT_THREAD"></span>**事件线程**  
上次发生事件的线程。

<span id="executing_processor_type"></span><span id="EXECUTING_PROCESSOR_TYPE"></span>**正在执行处理器类型**  
当前处理器上下文中的处理器的类型。

<span id="exception"></span><span id="EXCEPTION"></span>**异常**  
由于执行特定的计算机指令或从目标中指示其遇到了错误而导致的错误条件。 异常可能是与硬件或软件相关的错误。

异常是，由其标识。

<span id="exception_code"></span><span id="EXCEPTION_CODE"></span>**异常代码**  
确定异常事件类型的标识符。

<span id="exception_filter"></span><span id="EXCEPTION_FILTER"></span>**异常筛选器**  
异常代码指定的异常事件的事件筛选器。

<span id="extension"></span><span id="EXTENSION"></span>**拓**  
请参阅调试器扩展。

<span id="extension_command"></span><span id="EXTENSION_COMMAND"></span>**extension 命令**  
请参阅调试器扩展。

 

