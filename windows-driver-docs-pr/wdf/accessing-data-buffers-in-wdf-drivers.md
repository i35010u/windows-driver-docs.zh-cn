---
title: WDF 驱动程序 （KMDF 或 UMDF） 中访问数据缓冲区
description: 当 Windows 驱动程序框架 (WDF) 驱动程序收到读取、 写入或设备的 I/O 控制请求时，请求对象将包含输入的缓冲区、 输出缓冲区，或这两者。
ms.assetid: ceba2279-b0fb-4261-b439-723d5dad967b
keywords:
- 请求处理 WDK KMDF，数据缓冲区
- 数据缓冲 WDK KMDF
- 输入的缓冲区 WDK KMDF
- 输出缓冲区 WDK KMDF
- 缓冲区 WDK KMDF
- 缓冲的 I/O WDK KMDF
- 直接 I/O WDK KMDF
- 既不缓冲，也不直接 I/O WDK KMDF
- I/O 请求 WDK KMDF，数据缓冲区
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcf3495783391447c9b33a443906ae4d463b3ccf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526624"
---
# <a name="accessing-data-buffers-in-wdf-drivers-kmdf-or-umdf"></a>WDF 驱动程序 （KMDF 或 UMDF） 中访问数据缓冲区


当 Windows 驱动程序框架 (WDF) 驱动程序收到读取、 写入或设备的 I/O 控制请求时，请求对象将包含输入的缓冲区、 输出缓冲区，或这两者。

输入的缓冲区包含驱动程序需要的信息。 对于写请求，此信息通常是功能驱动程序必须向设备发送的数据。 对于设备 I/O 控制请求，请输入的缓冲区可能包含指示驱动程序必须执行的操作的类型的信息。

输出缓冲区接收来自驱动程序的信息。 对于读取请求，此信息通常是功能驱动程序从设备接收的数据。 对于设备 I/O 控制请求，输出缓冲区可能会收到状态或指定请求的 I/O 控制代码的其他信息。

您的驱动程序使用来访问请求的数据缓冲区的方法取决于用于访问数据缓冲区的设备驱动程序的方法。 有三种访问方法：

-   [缓冲 I/O](#buffered)。 I/O 管理器创建它，驱动程序与共享的中间缓冲区。
-   [直接 I/O](#direct)。 I/O 管理器到物理内存中，锁定缓冲区空间，然后为该驱动程序提供了直接访问权限的缓冲区空间。
-   [既不缓冲，也不直接 I/O](#neither)。 I/O 管理器将驱动程序提供请求的缓冲区空间的虚拟地址。 I/O 管理器不会验证请求的缓冲区空间，因此，该驱动程序必须验证缓冲区空间的可访问，并锁定到物理内存中缓冲区空间。

内核模式驱动程序框架 (KMDF) 驱动程序可以使用任何三种访问方法。 用户模式驱动程序框架 (UMDF) 驱动程序可以用于读取、 写入和 IOCTL 请求缓冲或直接 I/O，并且可以[转换指定的请求**方法\_NEITHER**方法](managing-buffer-access-methods-in-umdf-drivers.md#using-neither-buffered-i-o-nor-direct-i-o-in-umdf-drivers)。

## <a href="" id="ddk-preprocessing-i-o-requests-df"></a>指定缓冲区的访问方法


<a href="" id="kmdf-drivers"></a>**KMDF 驱动程序**  

对于读取和写入请求时，驱动程序堆栈中的所有驱动程序必须使用相同的方法，用于访问设备的缓冲区，但最高级别的驱动程序，可以使用"不"方法，无论哪个方法由较低的驱动程序除外。

从版本 1.13，KMDF 驱动程序通过调用中指定的所有设备的读取和写入请求的访问方法[ **WdfDeviceInitSetIoTypeEx** ](https://msdn.microsoft.com/library/windows/hardware/dn265604)为每个设备。 例如，如果驱动程序指定其设备之一的缓冲的 I/O 方法，I/O 管理器使用缓冲的 I/O 方法时提供读取和写入请求发送到该设备的驱动程序。

对于设备 I/O 控制请求的 I/O 控制代码 (IOCTL) 包含指定的缓冲区的访问方法的位。 因此，KMDF 驱动程序不需要采取任何操作来为 Ioctl 选择缓冲方法。 Ioctl 有关详细信息，请参阅[定义的 I/O 控制代码](https://msdn.microsoft.com/library/windows/hardware/ff543023)。 与不同的是读取和写入请求时，所有设备的 Ioctl 不需要指定相同的访问方法。

<a href="" id="umdf-drivers"></a>**UMDF 驱动程序**  

UMDF 驱动程序指定*首选项*访问的方法，该框架使用的方法读取和写入请求，以及设备 I/O 控制请求。 UMDF 驱动程序提供的值是仅首选项，并不保证由框架使用。 有关详细信息，请参阅[UMDF 驱动程序中管理缓冲区的访问方法](managing-buffer-access-methods-in-umdf-drivers.md)。

UMDF 驱动程序指定的所有设备的读取、 写入和 IOCTL 请求的访问方法通过调用[ **WdfDeviceInitSetIoTypeEx** ](https://msdn.microsoft.com/library/windows/hardware/dn265604)为每个设备。 例如，如果驱动程序指定其设备之一的缓冲的 I/O 方法，该框架使用缓冲的 I/O 方法传送到该设备的驱动程序的读取、 写入和 IOCTL 请求时。

请注意 KMDF 和 UMDF 之间 Ioctl 缓冲区访问技术中的差异。 KMDF 驱动程序没有为 Ioctl，指定缓冲区的访问方法，而 UMDF 驱动程序执行为 Ioctl 指定缓冲区的访问方法。

如果 WDF 驱动程序使用的 I/O 目标使用的 I/O 方法对于不正确的技术描述 I/O 请求的缓冲区，该框架将更正缓冲区说明。 例如，如果驱动程序使用 MDL 来描述它将传递到的缓冲区[ **WdfIoTargetSendReadSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548669)，如果 I/O 目标使用缓冲的 I/O (这需要缓冲区是使用指定的虚拟地址而不是 MDLs），该框架将从 MDL 缓冲区说明转换为虚拟地址和长度。 但是，它是效率更高如果您的驱动程序在正确的格式中指定的缓冲区。

有关 framework 内存对象、 后备链列表、 MDLs 和的本地缓冲区的信息，请参阅[使用的内存缓冲区](using-memory-buffers.md)。

有关何时删除内存缓冲区的信息，请参阅[内存缓冲区生命周期](memory-buffer-life-cycle.md)。

## <a href="" id="buffered"></a> 对于缓冲的 I/O 访问数据缓冲区


如果您的驱动程序使用缓冲的 I/O，具体取决于数据请求和是否使用 KMDF 或 UMDF 类型发生更改其行为。

<a href="" id="kmdf-drivers"></a>**KMDF 驱动程序**  

当 KMDF 驱动程序使用缓冲的 I/O 时，I/O 管理器创建一个驱动程序可以访问的每种类型的请求的中间缓冲区。 下面是会发生什么情况：

-   写入请求。 调用驱动程序堆栈之前，I/O 管理器将从调用应用程序的输入缓冲区传输输入的信息。 然后，KMDF 驱动程序从中间缓冲区中读取输入的信息并将其写入到设备。
-   读取请求。 KMDF 驱动程序从设备中读取信息并将其存储在中间的缓冲区中。 然后，I/O 管理器将中间缓冲区的输出数据复制到应用的输出缓冲区。
-   设备 I/O 控制请求。 KMDF 驱动程序读取，或将该请求的数据写入或从中间缓冲区。

<a href="" id="umdf-drivers"></a>**UMDF 驱动程序**  

当 UMDF 驱动程序使用缓冲的 I/O 时，驱动程序主机进程将创建一个或两个中间缓冲区，具体取决于请求的类型。 下面是会发生什么情况：

-   写入请求。 框架将创建一个缓冲区，将从调用应用程序的输入缓冲区传输输入的信息，然后调用驱动程序堆栈。 UMDF 驱动程序从中间缓冲区中读取输入的信息，并将其写入到设备。
-   读取请求。 UMDF 驱动程序从设备读取信息并将其存储在框架创建的缓冲区。 驱动程序主机进程将输出数据从中间缓冲区复制到应用的输出缓冲区。
-   设备 I/O 控制请求。 框架将创建两个对应的驱动程序可以访问 IOCTL 的输入和输出缓冲区的缓冲区。 框架将从 IOCTL 的输入的信息复制到新的中间缓冲区，并使其可供该驱动程序。 框架不会复制输出缓冲区的内容，以便该驱动程序不应尝试从其读取 （否则将其读取包含垃圾数据）。 该驱动程序将写入到输出缓冲区的任何数据复制回原始 IOCTL 缓冲区，并返回到 I/O 请求的成功完成后应用。 请注意，驱动程序将写入到输入缓冲区的任何数据是被丢弃，并且不返回到调用应用程序。

若要检索的句柄表示的缓冲区的 framework 内存对象，KMDF 和 UMDF 驱动程序调用[ **WdfRequestRetrieveInputMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff550015)或[ **WdfRequestRetrieveOutputMemory**](https://msdn.microsoft.com/library/windows/hardware/ff550019)，具体取决于这是读取或写入请求。 该驱动程序然后可以通过调用检索到缓冲区的指针[ **WdfMemoryGetBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff548715)。 读取和写入的缓冲区，驱动程序调用[ **WdfMemoryCopyFromBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff548701)或[ **WdfMemoryCopyToBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff548703)。

若要检索的虚拟地址和缓冲区的长度，该驱动程序调用[ **WdfRequestRetrieveInputBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff550014)或[ **WdfRequestRetrieveOutputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550018).

若要分配并生成缓冲区的内存描述符列表 (MDL)，KMDF 驱动程序调用[ **WdfRequestRetrieveInputWdmMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff550016)或[ **WdfRequestRetrieveOutputWdmMdl**](https://msdn.microsoft.com/library/windows/hardware/ff550021).

## <a href="" id="direct"></a> 对于直接 I/O 访问数据缓冲区


<a href="" id="kmdf-drivers"></a>**KMDF 驱动程序**  

如果您的驱动程序使用的直接 I/O，I/O 管理器验证发信方的 I/O 请求 （通常在用户模式应用程序） 指定，到物理内存中，将锁定缓冲区空间，然后即可提供与驱动程序的缓冲区空间的可访问性缓冲区空间的直接访问。

<a href="" id="umdf-drivers"></a>**UMDF 驱动程序**  

如果您的驱动程序已指定直接 I/O 的首选项，因此已达到直接 I/O 的所有 UMDF 要求 (请参阅[UMDF 驱动程序中管理缓冲区的访问方法](managing-buffer-access-methods-in-umdf-drivers.md))，框架将映射从 I/O 收到的内存缓冲区管理器直接插入驱动程序的主机进程地址空间，并因此为驱动程序提供了直接访问权限的缓冲区空间。

若要检索表示缓冲区空间，驱动程序调用 framework 内存对象的句柄[ **WdfRequestRetrieveInputMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff550015)或[ **WdfRequestRetrieveOutputMemory**](https://msdn.microsoft.com/library/windows/hardware/ff550019)。 该驱动程序然后可以通过调用检索到缓冲区的指针[ **WdfMemoryGetBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff548715)。 读取和写入的缓冲区，驱动程序调用[ **WdfMemoryCopyFromBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff548701)或[ **WdfMemoryCopyToBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff548703)。

若要检索的虚拟地址和长度的缓冲区空间，该驱动程序调用[ **WdfRequestRetrieveInputBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff550014)或[ **WdfRequestRetrieveOutputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550018).

如果设备的驱动程序使用的直接 I/O，I/O 管理器通过使用 MDLs 描述缓冲区。 若要检索一个指向缓冲区的 MDL，KMDF 驱动程序调用[ **WdfRequestRetrieveInputWdmMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff550016)或[ **WdfRequestRetrieveOutputWdmMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff550021). UMDF 驱动程序无法访问 MDLs。

## <a href="" id="neither"></a> 对于既不缓冲，也不直接 I/O 访问数据缓冲区


<a href="" id="kmdf-drivers"></a>**KMDF 驱动程序**  

如果您的驱动程序使用名为缓冲区的访问方法*既不缓冲 I/O，也不直接 I/O 方法*（或"方法都不"，简称），I/O 管理器只需提供驱动程序和虚拟地址的发起方指定请求的缓冲区空间的 I/O 请求。 I/O 管理器不会验证 I/O 请求的缓冲区空间，因此，该驱动程序必须验证缓冲区空间的可访问，并锁定到物理内存中缓冲区空间。

I/O 管理器提供的虚拟地址可以访问仅在 I/O 请求的发起进程上下文中。 保证仅驱动程序堆栈中的最高级别的驱动程序创建者进程上下文中执行。

若要获得访问权限的 I/O 请求的缓冲区空间，最高级别的驱动程序必须提供[ *EvtIoInCallerContext* ](https://msdn.microsoft.com/library/windows/hardware/ff541764)回调函数。 框架调用此回调函数每次收到该驱动程序的 I/O 请求。

如果请求的缓冲区的访问方法是"均不"，KMDF 驱动程序必须执行以下操作为每个缓冲区：

1.  调用[ **WdfRequestRetrieveUnsafeUserInputBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff550022)或[ **WdfRequestRetrieveUnsafeUserOutputBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff550024)若要获取的缓冲区虚拟地址。

2.  调用[ **WdfRequestProbeAndLockUserBufferForRead** ](https://msdn.microsoft.com/library/windows/hardware/ff549987)或[ **WdfRequestProbeAndLockUserBufferForWrite** ](https://msdn.microsoft.com/library/windows/hardware/ff549989)探测和锁定缓冲和若要获取的句柄 framework 内存对象缓冲区。

3.  在请求中保存内存对象句柄[上下文空间](using-request-object-context.md)。

4.  调用[ **WdfDeviceEnqueueRequest**](https://msdn.microsoft.com/library/windows/hardware/ff545945)，它返回与框架的请求。

随后，框架将请求添加到驱动程序的 I/O 队列之一。 如果已提供该驱动程序[请求处理程序](request-handlers.md)，框架将最终调用相应的请求处理程序。

请求处理程序可以从请求的上下文空间检索请求的内存对象句柄。 该驱动程序可以将传递到句柄[ **WdfMemoryGetBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff548715)获取缓冲区的地址。

有时，最高级别的驱动程序必须使用在前面的步骤来访问的用户模式缓冲区，即使该驱动程序使用"不"访问方法。 例如，假设驱动程序使用缓冲的 I/O。 使用缓冲的访问方法的 I/O 控制代码可能会传递包含嵌入到用户模式缓冲区指针的结构。 在这种情况下，该驱动程序必须提供[ *EvtIoInCallerContext* ](https://msdn.microsoft.com/library/windows/hardware/ff541764)回调函数，该结构中提取指针，然后使用前面步骤 2 至 4。

<a href="" id="umdf-drivers"></a>**UMDF 驱动程序**  

UMDF 不支持既不缓冲，也不直接 I/O 类型缓冲区，因此 UMDF 驱动程序永远不需要直接处理此类型的缓冲区。

但是，如果框架收到的此类缓冲区将读取或写入 I/O 管理器中，会将其提供给 UMDF 驱动程序为缓冲的 I/O 或直接 I/O，具体取决于所选驱动程序的访问方法。 如果框架接收 IOCTL 指定"不"缓冲区方法，它可以根据需要将 IOCTL 请求的缓冲区的访问方法转换为缓冲的 I/O 或基于存在一个 INF 指令的直接 I/O。 请参阅[UMDF 驱动程序中管理缓冲区的访问方法](managing-buffer-access-methods-in-umdf-drivers.md)的详细信息。

 

 





