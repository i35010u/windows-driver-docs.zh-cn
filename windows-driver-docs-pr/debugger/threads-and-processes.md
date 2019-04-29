---
title: 线程和进程
description: 线程和进程
ms.assetid: 7ba8226c-3fb3-4ed6-8f87-69a7999e34ad
keywords:
- 调试器引擎、 线程和进程
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 542611a320b70611dba3be2d7a12db44b245cd1c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366096"
---
# <a name="threads-and-processes"></a>线程和进程


### <a name="span-idterminologyspanspan-idterminologyspanterminology"></a><span id="terminology"></span><span id="TERMINOLOGY"></span>术语

线程和进程概念是用户模式下调试和内核模式调试之间的差异。

-   在*用户模式下调试*即*进程*是一个操作系统的过程和一个*线程*是一个操作系统线程。

-   在中*内核模式调试*，则[调试器引擎](introduction.md#debugger-engine)创建*虚拟过程*对于每个目标; 此过程表示内核，与任何不一致操作系统进程。 为目标计算机中每个物理处理器，调试器都会创建*虚拟线程*; 这些线程表示处理器并不对应于任何操作系统线程。

事件发生时，引擎将设置*事件进程*并*事件线程*到进程和线程 (操作系统或虚拟) 中发生该事件。

*当前线程*是线程 (操作系统或虚拟) 的当前控制引擎。 *当前进程*是过程 (操作系统或虚拟) 的当前控制引擎。 事件发生时，当前线程和进程是最初设置为事件线程和进程;但是，可以使用客户端，在会话处于可访问时更改它们。

在内核模式下，隐式过程和隐式线程，将跟踪的调试器。 *隐式过程*是确定从虚拟转换为物理内存地址的操作系统进程。

*隐式线程*是确定目标的寄存器，包括调用堆栈、 堆栈帧和指令偏移量的操作系统线程。

事件发生时，隐式线程和隐式过程最初设置为事件线程和进程;在会话处于可访问时，它们可以进行更改。

### <a name="span-idthreadandprocessdataspanspan-idthreadandprocessdataspanthread-and-process-data"></a><span id="thread_and_process_data"></span><span id="THREAD_AND_PROCESS_DATA"></span>线程和进程数据

引擎会保留以下几条有关每个线程和进程的信息。 这包括系统线程和进程 ID 和系统句柄和进程环境 (PEB)、 线程环境块 (TEB) 和它们的位置为目标的内存中。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关使用线程和进程的详细信息，请参阅[控制线程和进程](controlling-threads-and-processes.md)。

 

 





