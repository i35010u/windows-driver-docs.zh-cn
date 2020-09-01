---
title: '我 (Windows 调试器词汇表) '
description: 词汇表页面-I
ms.assetid: 4415522d-6ea3-42f6-9acc-0e3ceaa36dc7
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37521c8df53d8f12a7b4db9e2801eee351bbd3e5
ms.sourcegitcommit: cd84cc10570384b0e7a91cb6f91fe67009c1a90e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/01/2020
ms.locfileid: "89238139"
---
# <a name="i"></a>I


<span id="i_o_request_packet__irp_"></span><span id="I_O_REQUEST_PACKET__IRP_"></span>**I/o 请求数据包 (IRP) **  
用于表示 i/o 请求并控制其处理的数据结构。 IRP 结构包含一个标头和一个或多个堆栈位置。

<span id="image"></span><span id="IMAGE"></span>**影像**  
Windows 已作为用户模式进程或 Windows 内核的一部分加载的可执行文件、DLL 或驱动程序。

另请参阅图像文件。

<span id="image_file"></span><span id="IMAGE_FILE"></span>**映像文件**  
从中加载映像的文件。

<span id="implicit_process"></span><span id="IMPLICIT_PROCESS"></span>**隐式进程**  
在内核模式调试中，用于确定执行虚拟到物理地址转换时要使用的虚拟地址空间的过程。 事件发生时，隐式进程将设置为事件进程。

另请参阅隐式线程。

有关详细信息，请参阅 [线程和进程](threads-and-processes.md)。

<span id="implicit_thread"></span><span id="IMPLICIT_THREAD"></span>**隐式线程**  
在内核模式调试中，用于确定目标的某些寄存器（包括帧偏移量和指令偏移量）的线程。 事件发生时，隐式线程设置为事件线程。

<span id="inaccessible"></span><span id="INACCESSIBLE"></span>**无法访问**  
正在执行所有目标时， *无法访问* 调试会话。

<span id="initial_breakpoint"></span><span id="INITIAL_BREAKPOINT"></span>**初始断点**  
在调试会话开始时、重新启动之后或在目标应用程序重新启动之后自动发生的断点。

有关详细信息，请参阅 [使用断点](using-breakpoints.md)。

<span id="input_callback_objects"></span><span id="INPUT_CALLBACK_OBJECTS"></span>**输入回调对象**  
已向客户端注册的 [IDebugInputCallbacks](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebuginputcallbacks) 接口的实例。 每当调试器引擎需要输入时，它都会要求输入回调提供它。

另请参阅输出回调。

有关详细信息，请参阅 [USING AMLI 调试器命令](using-amli-debugger-commands.md)。

<span id="input_callbacks"></span><span id="INPUT_CALLBACKS"></span>**输入回调**  
请参阅输入回调对象。

<span id="interrupt"></span><span id="INTERRUPT"></span>**妨碍**  
中断正常命令执行并将控制转移到中断处理程序的条件。 需要处理器服务的 i/o 设备通常会启动中断。

<span id="interrupt_request_level__irql_"></span><span id="INTERRUPT_REQUEST_LEVEL__IRQL_"></span>**中断请求级别 (IRQL) **  
中断的优先级排名。 每个处理器都有一个可以提高或降低线程的 IRQL 设置。 在处理器的 IRQL 设置下或之下发生的中断会被屏蔽，并且不会影响当前操作。 超出处理器的 IRQL 设置的中断优先于当前操作。

 

