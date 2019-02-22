---
title: Windows 内核模式进程和线程管理器
description: Windows 内核模式进程和线程管理器
ms.assetid: 4053c73e-190d-4ffe-8db2-f531d120ba81
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7eb171169fa476b5c0c74a53f3e9ff7c6d2695f1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534601"
---
# <a name="windows-kernel-mode-process-and-thread-manager"></a>Windows 内核模式进程和线程管理器


一个*进程*是当前在 Windows 中运行的软件程序。 每个进程有一个 ID，用于标识它的数字。 一个*线程*是一个对象，标识哪些计划的一部分运行。 每个线程有一个 ID，用于标识它的数字。

一个进程可以包含多个线程。 线程的目的是要分配处理器时间百分比。 在具有一个处理器的计算机，可以分配多个线程，但只有一个线程可以运行一次。 每个线程仅在短时间运行，然后执行将传递给下一个线程，为用户提供多个一件事同时发生动作的视觉效果。 在具有多个处理器的计算机，真正的多线程处理可能会发生。 如果应用程序具有多个线程，线程可以同时在不同的处理器上运行。

Windows 内核模式进程和线程管理器处理的过程中的所有线程的执行。 是否有一个处理器或更多，但是必须谨慎驱动程序以确保所有线程过程的经过专门都设计，因此，无论何种顺序处理线程的编程中，您的驱动程序将正常运行。

如果来自不同进程的线程尝试在同一时间使用同一资源，可能出现问题。 Windows 提供了多种方法来避免此问题。 确保来自不同进程的线程不会接触相同资源的方法称为*同步*。 有关同步的详细信息，请参阅[同步技术](synchronization-techniques.md)。

向进程和线程管理器提供直接接口的例程都通常带有前缀字母"**Ps**"; 例如， **PsCreateSystemThread**。 有关内核 DDIs 的列表，请参阅[Windows 内核](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_kernel/)。

此组的指导原则适用于这些回调例程：

[_PCREATE_PROCESS_NOTIFY_ROUTINE_](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-pcreate_process_notify_routine)

[_PCREATE_PROCESS_NOTIFY_ROUTINE_EX_](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-pcreate_process_notify_routine_ex)

[_PCREATE_THREAD_NOTIFY_ROUTINE_](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-pcreate_thread_notify_routine)

[_PLOAD_IMAGE_NOTIFY_ROUTINE_](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-pload_image_notify_routine)

-    保持通知例程简短和简单。
-    不执行到用户模式服务的调用来验证进程、 线程或图像。 
-    不执行注册表调用。 
-    不进行阻止和/或进程间通信 (IPC) 函数调用。 
-    不要同步与其他线程，因为它可能会导致重新进入死锁。 
-    使用[系统工作线程数](https://docs.microsoft.com/windows-hardware/drivers/kernel/system-worker-threads)尤其是工作涉及将工作排队到： 
        -    API 或 API 的调用到其他进程降低速度。
        -    任何阻塞行为，这可能中断核心服务中的线程。 
-    周密的内核模式堆栈使用情况的最佳做法。 有关示例，请参阅[如何使我的驱动程序的内核模式堆栈不足？](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn613940(v=vs.85))并[重要驱动程序的概念和提示](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn614604(v%3dvs.85))。


## <a name="subsystem-processes"></a>子系统进程


从 Windows 10 开始，Windows 子系统用于 Linux (WSL) 使用户能够与其他 Windows 应用程序一同上 Windows，运行本机 Linux ELF64 二进制文件。 有关 WSL 体系结构和运行的二进制文件所需的用户模式和内核模式组件的信息，请参阅文章在[适用于 Linux 的 Windows 子系统](https://go.microsoft.com/fwlink/p/?linkid=838012)博客。

一个组件是*子系统过程*承载未修改的用户模式 Linux 二进制文件，例如/bin/bash。 子系统进程不包含与 Win32 进程，如进程环境块 (PEB) 和线程环境块 (TEB) 相关联的数据结构。 对于的子系统进程，系统调用和用户模式异常将被分派给配对的驱动程序。

以下是对的更改[进程和线程管理器例程](https://msdn.microsoft.com/library/windows/hardware/ff559917)为了支持子系统进程：

-   WSL 类型为由**SubsystemInformationTypeWSL**中的值[**子系统\_信息\_类型**](https://msdn.microsoft.com/library/windows/hardware/mt805892)枚举。 驱动程序可以调用[ **NtQueryInformationProcess** ](https://msdn.microsoft.com/library/windows/desktop/ms684280)并[ **NtQueryInformationThread** ](https://msdn.microsoft.com/library/windows/desktop/ms684283)以确定基本子系统。 这些调用将返回**SubsystemInformationTypeWSL** WSL 的。
-   其他内核模式驱动程序可以获取有关的通知子系统进程创建/删除通过注册通过其回调例程[ **PsSetCreateProcessNotifyRoutineEx2** ](https://msdn.microsoft.com/library/windows/hardware/mt805891)调用。 若要获取有关线程创建/删除的通知，驱动程序可以调用[ **PsSetCreateThreadNotifyRoutineEx**](https://msdn.microsoft.com/library/windows/hardware/dn957857)，并指定**PsCreateThreadNotifySubsystems**作为通知的类型。
-   [ **PS\_创建\_通知\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff559960)结构已扩展为包括**IsSubsystemProcess**成员，指示非 Win32 子系统。 其他成员，如**的文件对象**，**映像文件名**， **CommandLine**指示子系统过程有关的其他信息。 有关这些成员的行为的信息，请参阅[**子系统\_信息\_类型**](https://msdn.microsoft.com/library/windows/hardware/mt805892)。

 

 




