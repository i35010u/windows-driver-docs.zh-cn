---
title: Windows 内核模式进程和线程管理器
description: Windows 内核模式进程和线程管理器
ms.assetid: 4053c73e-190d-4ffe-8db2-f531d120ba81
ms.localizationpriority: High
ms.date: 10/17/2018
ms.openlocfilehash: e494f2d3021733363fd9bea8b8a312798473e53f
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007580"
---
# <a name="windows-kernel-mode-process-and-thread-manager"></a>Windows 内核模式进程和线程管理器


*进程*是当前在 Windows 中运行的软件程序。 每个进程都有一个 ID 和一个标识该 ID 的数字。 *线程*是标识程序中正在运行的部分的对象。 每个线程都有一个 ID 和一个标识该 ID 的数字。

一个进程可以有多个线程。 线程的用途是分配处理器时间。 在具有一个处理器的计算机上，可以分配多个线程，但是一次只能运行一个线程。 每个线程仅运行一小段时间，然后将执行传递到下一个线程，为用户提供一次发生多项事情的假象。 在具有多个处理器的计算机上，可以进行真正的多线程处理。 如果应用程序具有多个线程，则线程可以在不同的处理器上同时运行。

Windows 内核模式进程和线程管理器处理进程中的所有线程的执行。 无论您有一个处理器还是更多，都必须在驱动程序编程中进行小心，以确保进程的所有线程都被设计为无论处理线程的顺序如何，您的驱动程序都将正常运行。

如果来自不同进程的线程尝试同时使用同一资源，则可能会出现问题。 Windows 提供了几种方法来避免此问题。 确保不同进程中的线程不触及同一资源的方法称为*同步*。 有关同步的详细信息，请参阅[同步技术](synchronization-techniques.md)。

为进程和线程管理器提供直接接口的例程通常以字母 "**Ps**" 为前缀;例如， **PsCreateSystemThread**。 有关内核 DDIs 的列表，请参阅[Windows 内核](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_kernel/)。

这组指导原则适用于以下回调例程：

[_PCREATE_PROCESS_NOTIFY_ROUTINE_](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-pcreate_process_notify_routine)

[_PCREATE_PROCESS_NOTIFY_ROUTINE_EX_](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-pcreate_process_notify_routine_ex)

[_PCREATE_THREAD_NOTIFY_ROUTINE_](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-pcreate_thread_notify_routine)

[_PLOAD_IMAGE_NOTIFY_ROUTINE_](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-pload_image_notify_routine)

-    将通知例程保持简短且简单。
-    请勿调用用户模式服务来验证进程、线程或映像。 
-    请勿调用注册表。 
-    不要发出阻塞和/或进程间通信（IPC）函数调用。 
-    不要与其他线程同步，因为这可能会导致重入死锁。 
-    使用[系统工作线程](https://docs.microsoft.com/windows-hardware/drivers/kernel/system-worker-threads)来排队工作，尤其是涉及的工作： 
        -    调入其他进程的慢速 API 或 API。
        -    可能会中断核心服务中的线程的任何阻止行为。 
-    深思熟虑后得出内核模式堆栈使用的最佳实践。 有关示例，请参阅[如何实现使我的驱动程序不会在内核模式堆栈外运行？](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn613940(v=vs.85))和[关键驱动程序的概念和提示](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn614604(v=vs.85))。


## <a name="subsystem-processes"></a>子系统进程


从 Windows 10 开始，适用于 Linux 的 Windows 子系统（WSL）使用户能够在 Windows 上以及其他 Windows 应用程序上运行本机 Linux ELF64 二进制文件。 有关运行二进制文件所需的 WSL 体系结构和用户模式和内核模式组件的信息，请参阅[适用于 Linux 的 Windows 子系统](https://go.microsoft.com/fwlink/p/?linkid=838012)博客上的文章。

其中一个组件是承载未修改的用户模式 Linux 二进制文件（如/bin/bash。）的*子系统进程*。 子系统进程不包含与 Win32 进程关联的数据结构，例如进程环境块（PEB）和线程环境块（TEB）。 对于子系统进程，系统调用和用户模式异常将被调度到配对的驱动程序中。

下面是对[进程和线程管理器例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)的更改，以便支持子系统进程：

-   WSL 类型由[**子系统 @ no__t-3INFORMATION @ no__t-4TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ne-ntddk-_subsystem_information_type)枚举中的**SubsystemInformationTypeWSL**值指示。 驱动程序可以调用[**NtQueryInformationProcess**](https://docs.microsoft.com/windows/desktop/api/winternl/nf-winternl-ntqueryinformationprocess)和[**NtQueryInformationThread**](https://docs.microsoft.com/windows/desktop/api/winternl/nf-winternl-ntqueryinformationthread)来确定基础子系统。 这些调用返回 WSL 的**SubsystemInformationTypeWSL** 。
-   其他内核模式驱动程序可以通过[**PsSetCreateProcessNotifyRoutineEx2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-pssetcreateprocessnotifyroutineex2)调用注册其回调例程来接收有关子系统进程创建/删除的通知。 若要获取有关线程创建/删除的通知，驱动程序可以调用[**PsSetCreateThreadNotifyRoutineEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-pssetcreatethreadnotifyroutineex)，并将**PsCreateThreadNotifySubsystems**指定为通知的类型。
-   [**PS @ no__t-2CREATE @ no__t-3NOTIFY @ no__t-4INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_ps_create_notify_info)结构已扩展为包含一个**IsSubsystemProcess**成员，该成员指示除 Win32 以外的子系统。 其他成员（如**FileObject**、 **ImageFileName**、**命令行**）指示有关子系统进程的其他信息。 有关这些成员的行为的信息，请参阅[**no__t-2INFORMATION @ no__t-3TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ne-ntddk-_subsystem_information_type)。

 

 




