---
title: K （Windows 调试器词汇表）
description: 术语表页-K
Robots: noindex, nofollow
ms.assetid: 93b65114-f680-41f7-b754-699f773955ba
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55bba94dabf12a88675bf5b4b1db4f8eeeef450e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534112"
---
# <a name="k"></a>K


<span id="kd_connection_server"></span><span id="KD_CONNECTION_SERVER"></span>**KD 连接服务器**  
在某些形式的内核模式远程调试过程中使用代理服务器。 它侦听来自智能客户端的连接并执行内存、 处理器、 或 Windows 操作根据这些远程客户端的请求。

请参阅也在调试服务器。

有关详细信息，请参阅[KD 连接服务器 （内核模式）](kd-connection-servers--kernel-mode-.md)。

<span id="kernel"></span><span id="KERNEL"></span>**kernel**  
内核是 Windows 操作系统的管理和控制硬件资源的访问权限的部分。 它执行线程计划和调度、 中断和异常处理和多处理器同步。

<span id="kernel_error"></span><span id="KERNEL_ERROR"></span>**内核错误**  
检查的 bug，请参阅。

<span id="kernel_mode"></span><span id="KERNEL_MODE"></span>**内核模式**  
内核模式代码有权访问的系统，任何部分，并不局限于用户模式代码。 它可以访问在用户模式或内核模式中运行的任何其他进程的任何部分。

在内核模式下运行性能敏感操作系统组件。 在这种方式中它们可以与硬件进行交互并与彼此无需使用的上下文切换。 所有内核模式组件完全都防止在用户模式下运行的应用程序。 可以将它们分组，如下所示：

-   高级管理人员。

    这包含基础操作系统组件，如内存管理、 进程和线程管理、 安全性、 I/O、 进程间通信。

-   内核。

    这将执行线程计划、 中断和调度，异常和多处理器同步等低级别功能。 它还提供了一组例程和基本对象的高级管理人员用于实现更高级别的语义。

-   硬件抽象层 (HAL)。

    这可以处理所有的直接接口到硬件。 它因此 Windows 内核、 设备驱动程序和 Windows 执行经理将与隔离开来的特定于平台的硬件差异。

-   窗口和图形子系统。

    这会实现图形用户界面 (GUI) 函数。

如果在进程会错误地访问的部分是另一个应用程序或系统正在使用的内存，缺乏对内核模式进程限制会强制停止整个系统的 Windows。 这称为的 bug 检查。

运行不正常的硬件设备或设备驱动程序，它驻留在内核模式下，通常是在错误检查的原因。

<span id="kernel_mode_target"></span><span id="KERNEL_MODE_TARGET"></span>**kernel-mode target**  
请参阅目标计算机。

<span id="kernel_mode_debugging"></span><span id="KERNEL_MODE_DEBUGGING"></span>**内核模式调试**  
在其中目标在内核模式下运行一个调试器会话。

 

 





