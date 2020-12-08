---
title: SPB 连接锁
description: 连接锁可用于使两个客户端在简单外围总线 (SPB) 上共享对目标外围设备的访问。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6cc7e56523aed34963eb18c00f4a84f9d52daad8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835397"
---
# <a name="spb-connection-locks"></a>SPB 连接锁


连接锁可用于使两个客户端在 [简单外围总线](/previous-versions/hh450903(v=vs.85)) (SPB) 上共享对目标外围设备的访问。 这两个客户端都可以打开到同一目标设备的逻辑连接，并在客户端要求对设备进行独占访问时使用连接锁定，以执行一系列 i/o 操作。 当一台客户端持有连接锁时，第二个客户端对该设备的请求会自动延迟，直到第一个客户端释放该锁。

客户端使用 [**ioctl \_ spb \_ 锁定 \_ 连接**](https://msdn.microsoft.com/library/windows/hardware/jj819324) 和 [**ioctl \_ spb \_ 解锁 \_ 连接**](https://msdn.microsoft.com/library/windows/hardware/jj819325) 请求，以获取和释放 SPB 上目标设备上的连接锁。 客户端将 (IOCTL) 请求的这些 i/o 控制发送到设备的文件对象。

与 SPB 连接的外围设备的驱动程序通常是 User-Mode Driver Framework (UMDF) 驱动程序或 Kernel-Mode Driver Framework (KMDF) 驱动程序。 为了将 IOCTL 请求发送到已连接到 SPB 的外围设备，UMDF 驱动程序会调用方法，例如 [**IWDFIoRequest：： send**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send)。 KMDF 驱动程序调用诸如 [**WdfIoTargetSendIoctlSynchronously**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendioctlsynchronously)的方法。

通常，不需要连接锁。 大多数客户端驱动程序在 SPB 上始终具有对目标设备的独占访问权限。 只有在相对罕见的情况下才需要连接锁，在这种情况下，两个客户端必须共享对同一目标设备的访问权限，并且一个或两个客户端有时必须具有对设备的独占访问权限，才能实现一系列 i/o 操作。

默认情况下，如果两个客户端共享目标设备，则 [SPB framework 扩展](./spb-framework-extension.md) (SpbCx) 按照它们到达 SpbCx 请求队列的顺序序列化设备的 i/o 请求。 连接锁将覆盖请求的默认排序顺序。 一台客户端获取连接锁后，SpbCx 会持有从第二个客户端接收到的 i/o 请求，直到第一个客户端释放该锁。

在 SpbCx 的当前实现中，连接锁定的主要用途是使目标设备的客户端驱动程序可以使用 ACPI 驱动程序来共享对设备的访问，Acpi.sys。 Acpi.sys 是系统提供的驱动程序，它代表硬件平台的 ACPI 固件管理某些核心资源设备。 例如，使用芯片 (SoC) 上的系统的平台还可能包含 (PMIC) ，同时通过 Acpi.sys 和客户端驱动程序访问该功能。

客户端驱动程序负责确定是否需要对需要独占访问目标设备的 i/o 操作进行连接锁定。 如果驱动程序在某些硬件平台或平台配置中需要连接锁，但在其他情况下，驱动程序开发人员和平台开发人员必须同意特定于驱动程序的机制来确定何时使用连接锁。 通常，平台固件中是否包含有关是否使用连接锁定的信息。 例如，设备的 ACPI 资源描述符中供应商定义的信息块可能包含一个标志位，用来指示驱动程序是否与 Acpi.sys 共享设备。

## <a name="connection-lock-example"></a>连接锁示例


连接锁的典型用法是实现原子读修改写入操作。 如果两个客户端在简单外围总线 (SPB) 上共享对同一目标设备的访问，则客户端可以使用连接锁将读取操作和写入操作合并为单个原子读修改写入操作。 连接锁定会阻止其他客户端访问读写操作之间的目标设备。

以下列表描述了客户端可能发送到连接到 SPB 的目标设备以在设备上执行读修改操作的 i/o 请求系列：

1.  [**IOCTL \_SPB \_ 锁定 \_ 连接**](https://msdn.microsoft.com/library/windows/hardware/jj819324) –获取目标设备上的连接锁。
2.  [**IRP \_MJ \_ read**](../kernel/irp-mj-read.md) –从设备地址读取数据块，以便客户端可以解释和修改数据。
3.  [**IRP \_MJ \_ 写入**](../kernel/irp-mj-write.md) –将修改后的数据块写入设备地址。
4.  [**IOCTL \_SPB \_ 解锁 \_ 连接**](https://msdn.microsoft.com/library/windows/hardware/jj819325) –在目标设备上释放连接锁。

前面的列表可能适用于实现单个设备功能的简单设备。

但是，更复杂的设备可能会实现多个设备功能。 此设备可能包含客户端在数据传输开始时加载的函数地址注册。 对于此设备， [**IOCTL \_ SPB \_ 执行 \_ 序列**](https://msdn.microsoft.com/library/windows/hardware/hh450857) 请求可以将函数地址寄存器的加载和接下来的数据传输组合到一个原子总线操作中。 有关详细信息，请参阅 [原子总线操作](./atomic-bus-operations.md)中的示例 I i2c 设备的说明。

## <a name="comparison-with-controller-locks"></a>与控制器锁的比较


客户端使用连接锁来获取对目标设备的独占访问权限，但连接锁不会阻止与总线上的其他设备进行数据传输。

若要以原子总线操作的形式执行一系列数据传输，客户端通常使用 [**IOCTL \_ SPB \_ 执行 \_ 序列**](https://msdn.microsoft.com/library/windows/hardware/hh450857) 请求。 执行原子总线操作的常见方法是使用控制器锁。 客户端将 [**ioctl \_ spb \_ 锁 \_ 控制器**](https://msdn.microsoft.com/library/windows/hardware/hh450858) 和 [**ioctl \_ spb \_ 解锁 \_ 控制器**](https://msdn.microsoft.com/library/windows/hardware/hh450859) 请求发送到获取并释放控制器锁。

控制器锁不同于连接锁。 控制器锁允许将一系列 i/o 传输到总线上的目标设备，并将其作为单个原子总线操作执行。 控制器锁定生效时，将延迟传输到总线上的其他设备，直到控制器锁释放。 有关详细信息，请参阅 [原子总线操作](./atomic-bus-operations.md)。

**注意**  在某些实现中，连接锁可能会导致传输到总线上的其他设备。 但是，此行为是依赖于实现的，并且客户端驱动程序不应依赖于它。 相反，控制器锁定会可靠地阻止其他客户端访问与持有控制器锁定的客户端相同的目标设备，并且客户端可以安全地依赖于此行为。

 

在目标设备上执行一组 i/o 操作之前，客户端可能需要获取连接锁和控制器锁定。 连接锁定会阻止第二个客户端共享对同一目标设备的访问，以便在设备上执行 i/o 操作，控制器锁定会阻止总线上其他设备的客户端对这些其他设备执行 i/o 操作。 在持有锁的情况下，不会发生阻止发生的 (i/o 操作 ) 。

当客户端为 SPB 上的目标设备同时获取连接锁和控制器锁定时，客户端必须在获取控制器锁之前获取连接锁，并且必须释放控制器锁才能释放连接锁。 在客户端获取连接锁之后，客户端可以根据需要在客户端释放连接锁之前，根据需要获取并释放控制器锁定。

连接锁的嵌套获取是非法的。 在客户端获取连接锁之后，客户端不能再次尝试获取该锁，直到客户端首先释放该锁。 同样，控制器锁的嵌套获取是不允许的。

 

