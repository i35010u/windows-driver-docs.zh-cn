---
title: Windows 内核模式进程和线程管理器
description: Windows 内核模式进程和线程管理器
ms.assetid: 4053c73e-190d-4ffe-8db2-f531d120ba81
ms.localizationpriority: High
ms.date: 10/17/2018
ms.openlocfilehash: e3a456484eef4f959aba2a745ecb284ccab1d6ea
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403484"
---
# <a name="windows-kernel-mode-process-and-thread-manager"></a>Windows 内核模式进程和线程管理器


 进程是当前在 Windows 中运行的软件程序。 每个进程都有一个 ID（一个标识该进程的数字）。  线程是一个对象，用于标识程序的哪个部分正在运行。 每个线程都有一个 ID（一个标识该线程的数字）。

一个进程可以有多个线程。 线程的用途是分配处理器时间。 在具有一个处理器的计算机上，可以分配多个线程，但一次只能运行一个线程。 每个线程仅运行一小段时间，然后执行会传递到下一个线程，使得用户产生多个事件正在同时发生的错觉。 在具有多个处理器的计算机上，可以进行真正的多线程处理。 如果应用程序有多个线程，则这些线程可以在不同的处理器上同时运行。

Windows 内核模式进程和线程管理器处理进程中的所有线程的执行。 无论你有一个处理器还是多个处理器，都必须在进行驱动程序编程时非常小心，以确保进程的所有线程都被设计为无论处理线程的顺序如何，驱动程序都将正常运行。

如果来自不同进程的线程尝试同时使用同一资源，则可能会出现问题。 Windows 提供了几种技术来避免此问题。 确保不同进程中的线程不触及同一资源的技术称为“同步”  。 有关同步的详细信息，请参阅[同步技术](introduction-to-kernel-dispatcher-objects.md)。

为进程和线程管理器提供直接接口的例程通常有字母“**Ps**”前缀；例如，**PsCreateSystemThread**。 有关内核 DDI 的列表，请参阅 [Windows 内核](/windows-hardware/drivers/ddi/_kernel/)。

这组指导原则适用于以下回调例程：

[_PCREATE_PROCESS_NOTIFY_ROUTINE_](/windows-hardware/drivers/ddi/ntddk/nc-ntddk-pcreate_process_notify_routine)

[_PCREATE_PROCESS_NOTIFY_ROUTINE_EX_](/windows-hardware/drivers/ddi/ntddk/nc-ntddk-pcreate_process_notify_routine_ex)

[_PCREATE_THREAD_NOTIFY_ROUTINE_](/windows-hardware/drivers/ddi/ntddk/nc-ntddk-pcreate_thread_notify_routine)

[_PLOAD_IMAGE_NOTIFY_ROUTINE_](/windows-hardware/drivers/ddi/ntddk/nc-ntddk-pload_image_notify_routine)

-    使通知例程保持简短且简单。
-    请勿调用用户模式服务来验证进程、线程或映像。 
-    请勿进行注册表调用。 
-    请勿进行阻塞和/或进程间通信 (IPC) 函数调用。 
-    请勿与其他线程同步，因为这可能会导致发生重入死锁。 
-    使用[系统工作线程](./system-worker-threads.md)来对工作进行排队，尤其是涉及以下任何一项的工作： 
        -    慢速 API 或调用其他进程的 API。
        -    可能会中断核心服务中的线程的任何阻止行为。 
-    处处考虑到适用于内核模式堆栈使用情况的最佳做法。 有关示例，请参阅[如何防止驱动程序耗尽内核模式堆栈？](/previous-versions/windows/hardware/design/dn613940(v=vs.85))和[重要驱动程序概念和提示](/previous-versions/windows/hardware/design/dn614604(v=vs.85))。


## <a name="subsystem-processes"></a>子系统进程


从 Windows 10 开始，适用于 Linux 的 Windows 子系统 (WSL) 可让用户在 Windows 上将本机 Linux ELF64 二进制文件与其他 Windows 应用程序一起运行。 有关 WSL 体系结构以及运行二进制文件所需的用户模式和内核模式组件的信息，请参阅[适用于 Linux 的 Windows 子系统](https://go.microsoft.com/fwlink/p/?linkid=838012)博客中的帖子。

其中一个组件是托管未修改的用户模式 Linux 二进制文件（如 /bin/bash）的子系统进程  。 子系统进程不包含与 Win32 进程关联的数据结构，例如进程环境块 (PEB) 和线程环境块 (TEB)。 对于子系统进程，系统调用和用户模式异常将被调度到配对的驱动程序。

下面是为了支持子系统进程而对 [进程和线程管理器例程](/windows-hardware/drivers/ddi/index)进行的更改：

-   WSL 类型由 [**SUBSYSTEM\_INFORMATION\_TYPE**](/windows-hardware/drivers/ddi/ntddk/ne-ntddk-_subsystem_information_type) 枚举中的 **SubsystemInformationTypeWSL** 值指示。 驱动程序可以调用 [**NtQueryInformationProcess**](/windows/desktop/api/winternl/nf-winternl-ntqueryinformationprocess) 和 [**NtQueryInformationThread**](/windows/desktop/api/winternl/nf-winternl-ntqueryinformationthread) 来确定基础子系统。 对于 WSL，这些调用会返回 **SubsystemInformationTypeWSL**。
-   其他内核模式驱动程序可以通过调用 [**PsSetCreateProcessNotifyRoutineEx2**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-pssetcreateprocessnotifyroutineex2) 来注册其回调例程，从而收到有关创建/删除子系统进程的通知。 若要获取有关创建/删除线程的通知，驱动程序可以调用 [**PsSetCreateThreadNotifyRoutineEx**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-pssetcreatethreadnotifyroutineex)，并指定 **PsCreateThreadNotifySubsystems** 作为通知的类型。
-   [**PS\_CREATE\_NOTIFY\_INFO**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_ps_create_notify_info) 结构已扩展为包含 **IsSubsystemProcess** 成员，该成员指示 Win32 之外的子系统。 其他成员（如 **FileObject**、**ImageFileName**、**CommandLine**）指示有关子系统进程的其他信息。 有关这些成员的行为的信息，请参阅 [**SUBSYSTEM\_INFORMATION\_TYPE**](/windows-hardware/drivers/ddi/ntddk/ne-ntddk-_subsystem_information_type)。

 

