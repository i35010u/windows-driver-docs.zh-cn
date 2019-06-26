---
title: SPB 连接锁
description: 连接锁可用于使两个客户端可以共享到简单的外围总线 （存储） 上的目标外围设备的访问权限。
ms.assetid: 073D9854-0F51-4518-A22B-0A0546694E30
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed08374b284243d1ceb21eebdde9e64a78cc5bea
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376925"
---
# <a name="spb-connection-locks"></a>SPB 连接锁


连接锁可用于启用两个客户端上共享到目标外围设备的访问权限[简单的外围总线](https://docs.microsoft.com/previous-versions/hh450903(v=vs.85))（存储）。 两个客户端可以打开到相同的目标设备的逻辑连接，并使用连接锁时客户端要求对设备执行一系列 I/O 操作的独占访问。 当一台客户端持有连接锁时，第二个客户端请求来访问设备是自动推迟到第一个客户端释放锁。

客户端用[ **IOCTL\_存储\_锁\_连接**](https://msdn.microsoft.com/library/windows/hardware/jj819324)并[ **IOCTL\_存储\_解锁\_连接**](https://msdn.microsoft.com/library/windows/hardware/jj819325)获取和释放连接锁的目标设备上存储的请求。 客户端将这些输入/输出控制 (IOCTL) 请求发送到设备的文件对象。

与存储连接的外围设备的驱动程序通常是用户模式驱动程序框架 (UMDF) 驱动程序或内核模式驱动程序框架 (KMDF) 驱动程序。 若要将 IOCTL 请求发送到与存储连接的外围设备，UMDF 驱动程序调用的方法如[ **IWDFIoRequest::Send**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send)。 KMDF 驱动程序调用的方法，如[ **WdfIoTargetSendIoctlSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetsendioctlsynchronously)。

通常情况下，连接锁是不必要的。 大多数客户端驱动程序始终在存储具有独占访问权的目标设备。 仅在两个客户端必须在其中共享对同一目标设备，访问权限的情况相对很少见的情况下需要连接锁和一个或两个客户端有时必须具有独占访问权的一系列 I/O 操作的设备。

默认情况下，如果两个客户端共享的目标设备，[存储框架扩展](https://docs.microsoft.com/windows-hardware/drivers/spb/spb-framework-extension)(SpbCx) 序列化为 SpbCx 请求队列中到达的顺序根据设备的 I/O 请求。 连接锁重写的默认顺序的请求。 一台客户端获取该锁，连接后，SpbCx 保存回 I/O 请求，它将收到来自第二个客户端直到第一个客户端释放锁。

在 SpbCx 当前实现中，连接锁的主要用途是启用要与 ACPI 驱动程序，Acpi.sys 共享到设备的访问权限的目标设备的客户端驱动程序。 Acpi.sys 是一个系统提供驱动程序，用于管理某些核心资源的设备的硬件平台的 ACPI 固件代表。 例如，一个平台，在芯片 (SoC) 上使用系统还可能包含 Acpi.sys 和客户端驱动程序访问的电源管理集成电路 (PMIC)。

客户端驱动程序负责确定是否需要独占访问的目标设备的 I/O 操作需要连接锁。 如果驱动程序需要连接锁在某些硬件平台或平台配置，但不是在其他用例，则驱动程序开发人员和平台开发人员必须达成用于确定连接锁时要使用的特定于驱动程序的机制。 通常情况下，在平台固件中包含有关是否使用连接锁信息。 例如，设备的 ACPI 资源描述符中的供应商定义的信息块可能包含标志位，以指示驱动程序是否与 Acpi.sys 共享设备。

## <a name="connection-lock-example"></a>锁的连接示例


连接锁的典型用途是实现原子读取-修改-写入操作。 如果两个客户端共享相同的简单外围总线 （存储） 上的目标设备的访问权限，或者客户端可以使用连接锁的读的操作和写入操作合并到单个原子读取-修改-写入操作。 连接锁可阻止其他客户端访问之间读取和写入操作的目标设备。

以下列表描述了 I/O 的一系列请求，客户端可能会发送到已连接存储的目标设备执行在设备上的读取-修改-写入操作：

1.  [**IOCTL\_存储\_锁\_连接**](https://msdn.microsoft.com/library/windows/hardware/jj819324) – 获取对目标设备的连接锁定。
2.  [**IRP\_MJ\_读取**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read) – 从设备地址读取的数据块，以便客户端可以解释和修改数据。
3.  [**IRP\_MJ\_编写**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write) – 将修改后的数据块写入到的设备地址。
4.  [**IOCTL\_存储\_解锁\_连接**](https://msdn.microsoft.com/library/windows/hardware/jj819325) – 释放目标设备上的连接锁。

前面的列表可能适用于实现的单个设备函数的简单设备。

但是，更复杂的设备可能会实现多个设备函数。 此设备可能包含在客户端加载数据传输开始时的函数地址注册。 对于此设备，请[ **IOCTL\_存储\_EXECUTE\_序列**](https://msdn.microsoft.com/library/windows/hardware/hh450857)请求可以组合的函数地址注册的加载和数据传输为单个原子总线操作如下所示。 有关详细信息，请参阅示例 I²C 设备中的说明[总线的原子操作](https://docs.microsoft.com/windows-hardware/drivers/spb/atomic-bus-operations)。

## <a name="comparison-with-controller-locks"></a>与控制器锁的比较


客户端使用的连接锁获取独占访问的目标设备，但连接锁不会阻止在总线上的数据传输到或从其他设备。

若要执行的数据传输一系列原子总线操作的形式，客户端通常使用[ **IOCTL\_存储\_EXECUTE\_序列**](https://msdn.microsoft.com/library/windows/hardware/hh450857)请求。 执行原子总线操作的不太常见方法是使用控制器锁。 客户端发送[ **IOCTL\_存储\_锁\_控制器**](https://msdn.microsoft.com/library/windows/hardware/hh450858)并[ **IOCTL\_存储\_解锁\_控制器**](https://msdn.microsoft.com/library/windows/hardware/hh450859)对获取和发布控制器锁的请求。

控制器锁是不同于连接的锁。 控制器锁定使 I/O 传输到和从目标设备总线上作为单一的原子总线操作执行一系列。 控制器锁在生效时，控制器锁释放前延迟总线上的传输到或从其他设备。 有关详细信息，请参阅[总线的原子操作](https://docs.microsoft.com/windows-hardware/drivers/spb/atomic-bus-operations)。

**请注意**  在某些实现中，连接锁可能会产生了负面影响，防止传输到总线上的其他设备。 但是，此行为是依赖于实现的并且客户端驱动程序不应依赖于它。 与此相反，控制器锁可靠地阻止另一个客户端访问相同的目标设备作为持有控制器锁的客户端和客户端可以安全地依赖于此行为。

 

客户端可能需要执行的一组目标设备上的 I/O 操作之前获取的连接锁以及控制器锁。 连接锁将阻止第二个客户端共享从执行 I/O 操作在设备上的访问相同的目标设备和控制器锁可防止在总线上的其他设备的客户端执行这些其他设备上的 I/O 操作。 （不能从这些锁都会保持过程中所发生的 I/O 操作都只需延迟，直到锁被释放。）

当客户端获取连接锁和目标设备上存储的控制器锁时，客户端必须获取控制器锁之前获取连接锁，并必须释放连接锁之前释放控制器锁。 客户端获取连接锁后，客户端可以如有必要，获取和释放无数次，客户端释放连接锁之前有必要进行控制器锁。

嵌套的收购连接锁是非法的。 客户端已获取了连接锁后，客户端必须不尝试再次获取的锁，直到客户端首先释放锁。 同样，不允许嵌套的收购的控制器锁。

 

 




