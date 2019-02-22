---
title: 我 （Windows 调试器词汇表）
description: 术语表页-H
Robots: noindex, nofollow
ms.assetid: 4415522d-6ea3-42f6-9acc-0e3ceaa36dc7
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 257bf93483dc6bd31b7aa48361f688a5c724460c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548216"
---
# <a name="i"></a>I


<span id="i_o_request_packet__irp_"></span><span id="I_O_REQUEST_PACKET__IRP_"></span>**I/O 请求数据包 (IRP)**  
用于表示 I/O 请求并控制其处理的数据结构。 IRP 结构包含一个标头和一个或多个堆栈位置。

<span id="image"></span><span id="IMAGE"></span>**image**  
可执行文件、 DLL 或 Windows 用户模式进程或 Windows 内核的一部分已加载的驱动程序。

另请参阅图像文件。

<span id="image_file"></span><span id="IMAGE_FILE"></span>**图像文件**  
从其加载图像文件。

<span id="implicit_process"></span><span id="IMPLICIT_PROCESS"></span>**隐式过程**  
在内核模式调试，用于确定要执行虚拟到物理地址转换时使用的虚拟地址空间的过程。 事件发生时，隐式过程设置为事件处理。

另请参阅隐式线程。

有关详细信息，请参阅[线程和进程](threads-and-processes.md)。

<span id="implicit_thread"></span><span id="IMPLICIT_THREAD"></span>**隐式线程**  
在内核模式调试，用于确定某些目标的寄存器的线程中包括的帧的偏移量和指令偏移量。 事件发生时，隐式线程设置为事件线程。

<span id="inaccessible"></span><span id="INACCESSIBLE"></span>**inaccessible**  
调试会话处于*无法访问*何时执行所有目标。

<span id="initial_breakpoint"></span><span id="INITIAL_BREAKPOINT"></span>**初始断点**  
会自动发生后重新启动，或后重新启动目标应用程序的调试会话，开始一个断点。

有关详细信息，请参阅[使用断点](using-breakpoints.md)。

<span id="input_callback_objects"></span><span id="INPUT_CALLBACK_OBJECTS"></span>**输入的回调对象**  
实例[IDebugInputCallbacks](https://msdn.microsoft.com/library/windows/hardware/ff550785)接口并已注册到客户端。 每当调试器引擎需要输入时它会要求输入的回调提供它。

另请参阅输出回调。

有关详细信息，请参阅[使用 AMLI 调试器命令](using-amli-debugger-commands.md)。

<span id="input_callbacks"></span><span id="INPUT_CALLBACKS"></span>**输入的回调**  
请参阅输入的回调对象。

<span id="interrupt"></span><span id="INTERRUPT"></span>**interrupt**  
一个条件，会中断到中断处理程序的标准命令执行，并将控制权。 通常需要服务从处理器的 I/O 设备启动中断。

<span id="interrupt_request_level__irql_"></span><span id="INTERRUPT_REQUEST_LEVEL__IRQL_"></span>**中断请求级别 (IRQL)**  
中断的优先级顺序。 每个处理器都有线程可以提高或降低的 IRQL 设置。 中断的发生或以下处理器的 IRQL 设置被屏蔽并不会干扰当前操作。 中断的发生以上处理器的 IRQL 设置优先于当前操作。

 

 





