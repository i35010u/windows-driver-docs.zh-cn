---
title: 线程和进程
description: 线程和进程
keywords:
- 调试器引擎、线程和进程
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97a9e79caf192a72ee085742bd72a0d50d9bacdb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838351"
---
# <a name="threads-and-processes"></a>线程和进程


### <a name="span-idterminologyspanspan-idterminologyspanterminology"></a><span id="terminology"></span><span id="TERMINOLOGY"></span>术语

线程和进程概念在用户模式调试和内核模式调试之间有所不同。

-   在 *用户模式调试* 中， *进程* 是操作系统进程，而 *线程* 是操作系统线程。

-   在 *内核模式调试* 中， [调试器引擎](introduction.md#debugger-engine) 为每个目标创建一个 *虚拟进程* ;此进程表示内核，与任何操作系统进程都不对应。 对于目标计算机中的每个物理处理器，调试器会创建一个 *虚拟线程*;这些线程表示处理器，不对应于任何操作系统线程。

事件发生时，引擎会将 *事件进程* 和 *事件线程* 设置为发生事件的进程和线程 (操作系统或虚拟) 。

*当前线程* 是引擎当前控制 (操作系统或虚拟) 线程。 *当前进程* 是引擎当前控制 (操作系统或虚拟) 的过程。 事件发生时，当前线程和进程最初设置为事件线程并处理;但在会话可访问时，可以使用客户端对其进行更改。

在内核模式下，调试器将跟踪隐式进程和隐式线程。 *隐式进程* 是确定从虚拟机到物理内存地址的转换的操作系统进程。

*隐式线程* 是确定目标的寄存器（包括调用堆栈、堆栈帧和指令偏移量）的操作系统线程。

事件发生时，隐式线程和隐式进程最初设置为事件线程并处理;可以在会话可访问时更改它们。

### <a name="span-idthread_and_process_dataspanspan-idthread_and_process_dataspanthread-and-process-data"></a><span id="thread_and_process_data"></span><span id="THREAD_AND_PROCESS_DATA"></span>线程和进程数据

引擎维护有关每个线程和进程的几个信息。 这包括系统线程、进程 ID 和系统句柄，进程环境 (PEB) ，线程环境块 (TEB) 及其在目标内存中的位置。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关使用线程和进程的详细信息，请参阅 [控制线程和进程](controlling-threads-and-processes.md)。

 

 





