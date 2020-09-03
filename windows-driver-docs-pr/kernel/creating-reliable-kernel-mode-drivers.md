---
title: 创建可靠的内核模式驱动程序
description: 创建可靠的内核模式驱动程序
ms.assetid: 31bbf1fe-dc90-43e0-a53e-eca902ec343e
keywords:
- 内核模式驱动程序 WDK、可靠性
- 可靠性 WDK 内核
- 可靠性 WDK 内核，关于可靠驱动程序
- Irp WDK 内核，可靠性问题
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41e79107f5834771e31d44299540b17bf0393bb4
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89402810"
---
# <a name="creating-reliable-kernel-mode-drivers"></a>创建可靠的内核模式驱动程序





驱动程序占内核模式下执行的总代码的百分比。 内核模式驱动程序实际上是操作系统的一个组件。 因此，可靠和安全的驱动程序会极大地影响操作系统的总体可信任性。 若要创建可靠的内核模式驱动程序，请遵循以下准则：

-   正确保护设备对象。

    用户对系统驱动程序和设备的访问权限由系统分配给设备对象的安全描述符控制。 最常见的情况是，系统会在安装设备时设置设备安全参数。 有关详细信息，请参阅 [创建安全设备安装](../install/creating-secure-device-installations.md)。 有时，驱动程序可以在控制其设备的访问权限的过程中发挥作用。 有关详细信息，请参阅 [保护设备对象](controlling-device-access.md)。

-   正确验证设备对象。

    如果驱动程序创建多种类型的设备对象，则必须检查每个 IRP 中接收的类型。 有关详细信息，请参阅 [无法验证设备对象](failure-to-validate-device-objects.md)。

-   使用 "safe string" 函数。

    在操作字符串时，驱动程序应使用安全字符串函数，而不是与 C/c + + 语言运行库一起提供的字符串函数。 有关详细信息，请参阅 [使用安全字符串函数](using-safe-string-functions.md)。

-   验证对象句柄。

    接收对象句柄作为输入的驱动程序必须验证这些句柄是否有效、是否可访问以及是否是预期类型。 有关使用对象句柄的详细信息，请参阅以下主题：

    [对象管理](managing-kernel-objects.md)

    [无法验证对象句柄](failure-to-validate-object-handles.md)

-   正确支持处理器。

    永远不会假设您的驱动程序将仅在单处理器系统上运行。 有关可用于确保驱动程序在多处理器系统上正常运行的编程技术的信息，请参阅以下主题：

    [同步技术](introduction-to-kernel-dispatcher-objects.md)

    [多处理器环境出错](errors-in-a-multiprocessor-environment.md)

-   正确处理驱动程序状态。

    务必要始终验证驱动程序是否处于您所采用的状态。 例如，如果驱动程序收到 IRP，是否已为相同类型的 IRP 提供服务？ 如果驱动程序没有检查这种情况，则第一个 IRP 可能会丢失。 有关详细信息，请参阅 [检查驱动程序状态失败](failure-to-check-a-driver-s-state.md)。

-   验证 IRP 输入值。

    从可靠性和安全性的角度来看，验证与 IRP 关联的所有值（如缓冲区地址和长度）是必不可少的。 以下主题提供有关验证 IRP 输入值的信息：

    [使用缓冲 I/O 执行 DispatchReadWrite](dispatchreadwrite-using-buffered-i-o.md)

    [缓冲 I/O 出错](failure-to-check-the-size-of-buffers.md)

    [使用直接 I/O 执行 DispatchReadWrite](dispatchreadwrite-using-direct-i-o.md)

    [直接 I/O 出错](errors-in-direct-i-o.md)

    [I/O 控制代码的安全问题](security-issues-for-i-o-control-codes.md)

    [引用用户空间地址时出错](errors-in-referencing-user-space-addresses.md)

-   正确处理 i/o 堆栈。

    将 [irp 沿驱动程序堆栈向下传递](passing-irps-down-the-driver-stack.md)时，驱动程序必须调用 [**IoSkipCurrentIrpStackLocation**](./mm-bad-pointer.md) 或 [**IoCopyCurrentIrpStackLocationToNext**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext) 来设置下一个驱动程序的 i/o 堆栈位置，这一点非常重要。 不要编写直接将一个 i/o 堆栈位置复制到下一个 i/o 堆栈位置的代码。

-   正确处理 IRP 完成操作。

    驱动程序绝不能完成状态值为 "成功" 的 IRP， \_ 除非它实际支持和处理 irp。 有关处理 IRP 完成操作的正确方法的信息，请参阅 [完成 irp](completing-irps.md)。

-   正确处理 IRP 取消操作。

    取消操作很难正确编码，因为它们通常以异步方式执行。 处理取消操作的代码中的问题可能会很长时间被忽略，因为通常不会在运行的系统中频繁执行此代码。

    务必阅读并了解 [取消 irp](canceling-irps.md)下提供的所有信息。 [在取消 Irp 时，请](points-to-consider-when-canceling-irps.md)特别注意[同步 IRP 取消](synchronizing-irp-cancellation.md)和要考虑的事项。

    避免与取消操作关联的同步问题的一种方法是实现 [取消安全 IRP 队列](cancel-safe-irp-queues.md)。 取消安全 IRP 队列是为 Windows XP 和更高版本的操作系统版本引入的驱动程序托管队列，但也向后兼容早期版本。

-   正确处理 IRP 清理并关闭操作。

    请确保了解 [**IRP \_ mj \_ 清除**](./irp-mj-cleanup.md) 和 [**irp \_ mj \_ 关闭**](./irp-mj-close.md) 请求之间的差异。 清理请求在应用程序关闭文件对象上的所有句柄之后，但有时在所有 i/o 请求完成之前到达。 完成或取消对文件对象的所有 i/o 请求后，关闭请求即可到达。 有关详细信息，请参阅下列主题：

    [DispatchCreate、DispatchClose 和 DispatchCreateClose 例程](dispatchcreate--dispatchclose--and-dispatchcreateclose-routines.md)

    [DispatchCleanup 例程](dispatchcleanup-routines.md)

    [处理清理和关闭操作时出错](errors-in-handling-cleanup-and-close-operations.md)

有关正确处理 Irp 的详细信息，请参阅 [处理 irp 中的其他错误](additional-errors-in-handling-irps.md)。

### <a name="using-driver-verifier"></a>使用驱动程序验证程序

[驱动程序验证程序](../devtest/driver-verifier.md) 是最重要的工具，可用于确保驱动程序的可靠性。 驱动程序验证程序可以检查各种常见的驱动程序问题，包括本节中讨论的一些问题。 但是，使用驱动程序验证器并不能替代谨慎的精心软件设计。

 

