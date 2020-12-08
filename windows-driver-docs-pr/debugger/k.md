---
title: 'K (Windows 调试器词汇表) '
description: 词汇表页-K
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16bd63ef281cc23d69c804a9f89a4bc021d861b3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803623"
---
# <a name="k"></a>K


<span id="kd_connection_server"></span><span id="KD_CONNECTION_SERVER"></span>**KD 连接服务器**  
在某种形式的内核模式远程调试过程中使用的代理。 它侦听来自智能客户端的连接，并执行这些远程客户端请求的内存、处理器或 Windows 操作。

另请参阅调试服务器。

有关详细信息，请参阅 [KD 连接服务器 (内核模式) ](kd-connection-servers--kernel-mode-.md)。

<span id="kernel"></span><span id="KERNEL"></span>**壳**  
内核是 Windows 操作系统的一部分，用于管理和控制对硬件资源的访问。 它执行线程计划和调度、中断和异常处理以及多处理器同步。

<span id="kernel_error"></span><span id="KERNEL_ERROR"></span>**内核错误**  
请参阅 bug 检查。

<span id="kernel_mode"></span><span id="KERNEL_MODE"></span>**内核模式**  
内核模式代码有权访问系统的任何部分，并且不受限于用户模式代码。 它可以访问在用户模式或内核模式下运行的任何其他进程的任何部分。

性能敏感的操作系统组件在内核模式下运行。 这样，它们就可以与硬件进行交互，并且无需上下文切换的开销。 所有内核模式组件都完全受到用户模式下运行的应用程序的保护。 可以按如下所示对其进行分组：

-   人员.

    这包含基本操作系统组件，如内存管理、进程和线程管理、安全性、i/o、进程间通信。

-   壳.

    这会执行线程计划、中断和异常调度以及多处理器同步等低级别功能。 它还提供了一组例程和一个用于实现更高级别的语义的基本对象。

-   硬件抽象层 (HAL) 。

    这会处理到硬件的所有直接接口。 因此，它将 Windows 内核、设备驱动程序和 Windows Executive 与特定于平台的硬件区别隔离开来。

-   窗口和图形子系统。

    这会 (GUI) 函数实现图形用户界面。

当某个进程错误地访问其他应用程序或系统正在使用的部分内存时，对内核模式进程的缺少限制将强制 Windows 停止整个系统。 这称为 "bug 检查"。

不正常的硬件设备或设备驱动程序（驻留在内核模式下）通常是 bug 检查中的原因。

<span id="kernel_mode_target"></span><span id="KERNEL_MODE_TARGET"></span>**内核模式目标**  
请参阅目标计算机。

<span id="kernel_mode_debugging"></span><span id="KERNEL_MODE_DEBUGGING"></span>**内核模式调试**  
一个调试器会话，在该会话中，目标在内核模式下运行。

 

 





