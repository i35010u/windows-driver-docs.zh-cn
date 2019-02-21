---
title: 创建可靠的内核模式驱动程序
description: 创建可靠的内核模式驱动程序
ms.assetid: 31bbf1fe-dc90-43e0-a53e-eca902ec343e
keywords:
- 内核模式驱动程序 WDK，可靠性
- 可靠性 WDK 内核
- 可靠性 WDK 内核，有关可靠的驱动程序
- Irp WDK 内核，可靠性问题
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec3d064e5f1bd63d0876519025edeaac9a2683d2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519301"
---
# <a name="creating-reliable-kernel-mode-drivers"></a>创建可靠的内核模式驱动程序





驱动程序构成了所有在内核模式下执行的代码的显著百分比。 实际上，内核模式驱动程序是操作系统的组件。 因此，可靠且安全的驱动程序会导致显著的操作系统整体可信度。 若要创建可靠的内核模式驱动程序，请遵循以下准则：

-   正确保护设备对象。

    由系统分配给设备对象的安全描述符控制用户对系统的驱动程序和设备访问权限。 大多数情况下，系统将在设备安装时设置设备安全参数。 有关详细信息，请参阅[创建安全的设备安装](https://msdn.microsoft.com/library/windows/hardware/ff540212)。 有时很适合的驱动程序播放中控制到其设备的访问权限的部件。 有关详细信息，请参阅[保护设备对象](securing-device-objects.md)。

-   正确验证设备的对象。

    如果驱动程序创建多种类型的设备对象，它必须检查每个 IRP 中收到哪种类型。 有关详细信息，请参阅[验证设备对象与失败](failure-to-validate-device-objects.md)。

-   使用"安全字符串"函数。

    当操作字符串时，驱动程序应使用安全的字符串函数而不是与 C/c + + 语言运行时库提供的字符串函数。 有关详细信息，请参阅[使用安全字符串函数](using-safe-string-functions.md)。

-   验证对象句柄。

    输入必须验证句柄有效，因为接收对象句柄的驱动程序可访问，以及为预期的类型。 有关使用对象句柄的详细信息，请参阅以下主题：

    [对象管理](managing-kernel-objects.md)

    [验证对象句柄失败](failure-to-validate-object-handles.md)

-   正确地支持多处理器系统。

    绝不能假定您的驱动程序将仅在单处理器系统上运行。 有关编程可用于确保您的驱动程序在多处理器系统上的函数将正确的技术信息，请参阅以下主题：

    [同步技术](synchronization-techniques.md)

    [在多处理器环境中的错误](errors-in-a-multiprocessor-environment.md)

-   正确处理驱动程序状态。

    请务必始终确认您的驱动程序是在假定它是在状态中。 例如，如果该驱动程序接收 IRP，它已经在为服务相同的类型的 IRP？ 如果该驱动程序不会检查这种情况下，第一个 IRP 可能会丢失。 有关详细信息，请参阅[未能检查驱动程序的状态](failure-to-check-a-driver-s-state.md)。

-   验证 IRP 输入的值。

    很重要，可靠性和安全性的角度，来验证与 IRP，如缓冲区地址和长度相关联的所有值。 以下主题提供有关验证 IRP 输入的值的信息：

    [DispatchReadWrite 使用缓冲的 I/O](dispatchreadwrite-using-buffered-i-o.md)

    [中缓冲的 I/O 错误](errors-in-buffered-i-o.md)

    [使用直接 I/O DispatchReadWrite](dispatchreadwrite-using-direct-i-o.md)

    [在直接 I/O 错误](errors-in-direct-i-o.md)

    [I/O 控制代码的安全问题](security-issues-for-i-o-control-codes.md)

    [引用用户空间地址中的错误](errors-in-referencing-user-space-addresses.md)

-   正确处理 I/O 堆栈。

    当[将 Irp 传递驱动程序堆栈的下层](passing-irps-down-the-driver-stack.md)，务必要调用的驱动程序[ **IoSkipCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff550355)或[ **IoCopyCurrentIrpStackLocationToNext** ](https://msdn.microsoft.com/library/windows/hardware/ff548387)设置下一步驱动程序的 I/O 堆栈位置。 不编写代码，直接将一个 I/O 堆栈位置复制到下一步。

-   正确处理 IRP 完成操作。

    驱动程序必须永远不会完成状态将 status 值 IRP\_成功除非实际上支持，且处理 IRP。 有关处理 IRP 完成操作的正确方法的信息，请参阅[完成 Irp](completing-irps.md)。

-   正确处理 IRP 取消操作。

    取消操作可能会对代码很难正确因为它们通常以异步方式执行。 处理取消操作的代码中的问题可被忽略，长时间，因为执行此代码通常不经常在正在运行的系统中。

    请务必阅读并理解所有下提供的信息[取消 Irp](canceling-irps.md)。 特别注意[同步 IRP 取消](synchronizing-irp-cancellation.md)并[指向考虑时取消 Irp](points-to-consider-when-canceling-irps.md)。

    避免相关联的同步问题的一种方法与取消操作是实现[取消安全 IRP 队列](cancel-safe-irp-queues.md)。 取消安全 IRP 队列是引入了针对 Windows XP 和更高版本的操作系统版本，但也是向后兼容早期版本的驱动程序管理队列。

-   处理 IRP 清理并正确关闭操作。

    请务必了解之间的区别[ **IRP\_MJ\_清理**](https://msdn.microsoft.com/library/windows/hardware/ff550718)并[ **IRP\_MJ\_关闭** ](https://msdn.microsoft.com/library/windows/hardware/ff550720)请求。 清理请求到达后关闭的应用程序的所有句柄上的文件对象，但有时在所有 I/O 之前请求已完成。 关闭请求到达后的文件对象的所有 I/O 请求已完成或已取消。 有关详情，请参阅以下主题：

    [DispatchCreate、 DispatchClose 和 DispatchCreateClose 例程](dispatchcreate--dispatchclose--and-dispatchcreateclose-routines.md)

    [DispatchCleanup 例程](dispatchcleanup-routines.md)

    [处理清除和关闭操作中的错误](errors-in-handling-cleanup-and-close-operations.md)

了解如何正确处理 Irp 的详细信息，请参阅[还有其他错误处理 Irp](additional-errors-in-handling-irps.md)。

### <a name="using-driver-verifier"></a>使用驱动程序验证程序

[驱动程序验证程序](https://msdn.microsoft.com/library/windows/hardware/ff545448)是最重要的工具可用来确保您的驱动程序的可靠性。 各种常见驱动程序问题，包括在本部分中讨论了其中一些可以检查驱动程序验证程序。 但是，使用驱动程序验证程序不会替换仔细考虑周全的软件设计。

 

 




