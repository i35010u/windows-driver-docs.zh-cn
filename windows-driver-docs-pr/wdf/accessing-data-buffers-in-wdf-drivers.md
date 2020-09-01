---
title: 在 WDF 驱动程序（KMDF 或 UMDF）中访问数据缓冲区
description: 当 Windows 驱动程序框架 (WDF) 驱动程序收到读取、写入或设备 i/o 控制请求时，请求对象将包含输入缓冲区和/或输出缓冲区。
ms.assetid: ceba2279-b0fb-4261-b439-723d5dad967b
keywords:
- 请求处理 WDK KMDF，数据缓冲区
- 数据缓冲区 WDK KMDF
- 输入缓冲 WDK KMDF
- 输出缓冲区 WDK KMDF
- 缓冲区 WDK KMDF
- 缓冲 i/o WDK KMDF
- 直接 i/o WDK KMDF
- 缓冲和直接 i/o WDK KMDF
- I/o 请求 WDK KMDF，数据缓冲区
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ea751f1b6b61febd3e8d72ae8b214ed6adc6d73
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192125"
---
# <a name="accessing-data-buffers-in-wdf-drivers-kmdf-or-umdf"></a>在 WDF 驱动程序（KMDF 或 UMDF）中访问数据缓冲区


当 Windows 驱动程序框架 (WDF) 驱动程序收到读取、写入或设备 i/o 控制请求时，请求对象将包含输入缓冲区和/或输出缓冲区。

输入缓冲区包含驱动程序所需的信息。 对于写入请求，此信息通常是函数驱动程序必须发送到设备的数据。 对于设备 i/o 控制请求，输入缓冲区可能包含表明驱动程序必须执行的操作类型的信息。

输出缓冲区从驱动程序接收信息。 对于读取请求，此信息通常是函数驱动程序从设备接收的数据。 对于设备 i/o 控制请求，输出缓冲区可能接收由请求的 i/o 控制代码指定的状态或其他信息。

驱动程序用于访问请求的数据缓冲区的方法取决于用于访问设备数据缓冲区的驱动程序的方法。 有三种访问方法：

-   [缓冲 i/o](#buffered)。 I/o 管理器会创建与驱动程序共享的中间缓冲区。
-   [直接 i/o](#direct)。 I/o 管理器会将缓冲区空间锁定为物理内存，并为该驱动程序提供对缓冲区空间的直接访问。
-   [缓冲或直接](#neither)i/o。 I/o 管理器为驱动程序提供请求的缓冲区空间的虚拟地址。 I/o 管理器不会验证请求的缓冲区空间，因此驱动程序必须验证缓冲区空间是否可访问，并将缓冲区空间锁定为物理内存。

 (KMDF) 驱动程序的内核模式驱动程序框架可以使用三种访问方法中的任意一种。 用户模式驱动程序框架 (UMDF) 驱动程序可以对读、写和 IOCTL 请求使用缓冲的或直接 i/o，并可以 [转换指定 **方法这 \_ 两** 种方法的请求](managing-buffer-access-methods-in-umdf-drivers.md#using-neither-buffered-i-o-nor-direct-i-o-in-umdf-drivers)。

## <a name="specifying-buffer-access-method"></a><a href="" id="ddk-preprocessing-i-o-requests-df"></a>指定缓冲区访问方法


<a href="" id="kmdf-drivers"></a>**KMDF 驱动程序**  

对于读取和写入请求，驱动程序堆栈中的所有驱动程序都必须使用与访问设备缓冲区相同的方法，这是最高级别的驱动程序除外，无论驱动程序使用哪种方法，都可以使用 "两个" 方法。

从1.13 版开始，KMDF 驱动程序通过为每个设备调用 [**WdfDeviceInitSetIoTypeEx**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotypeex) ，为所有设备的读取和写入请求指定访问方法。 例如，如果驱动程序为其某个设备指定了缓冲 i/o 方法，则当将读取和写入请求传递到该设备的驱动程序时，i/o 管理器将使用该缓冲 i/o 方法。

对于设备 i/o 控制请求，i/o 控制代码 (IOCTL) 包含指定缓冲区访问方法的位。 因此，KMDF 驱动程序无需执行任何操作即可为 IOCTLs 选择缓冲方法。 有关 IOCTLs 的详细信息，请参阅 [定义 I/o 控制代码](../kernel/defining-i-o-control-codes.md)。 与读取和写入请求不同，设备的所有 IOCTLs 无需指定相同的访问方法。

<a href="" id="umdf-drivers"></a>**UMDF 驱动程序**  

UMDF 驱动程序为框架用于读取和写入请求的访问方法和设备 i/o 控制请求指定 *首选项* 。 UMDF 驱动程序提供的值仅为首选项，不保证框架使用这些值。 有关详细信息，请参阅 [在 UMDF 驱动程序中管理缓冲区访问方法](managing-buffer-access-methods-in-umdf-drivers.md)。

UMDF 驱动程序通过为每个设备调用 [**WdfDeviceInitSetIoTypeEx**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotypeex) ，为所有设备的读取、写入和 IOCTL 请求指定访问方法。 例如，如果驱动程序为其某个设备指定了缓冲 i/o 方法，则当将读取、写入和 IOCTL 请求传送到该设备的驱动程序时，框架将使用该缓冲 i/o 方法。

请注意在 KMDF 和 UMDF 之间用于 IOCTLs 的缓冲区访问技术之间的差异。 KMDF 驱动程序未指定 IOCTLs 的缓冲区访问方法，而 UMDF 驱动程序则为 IOCTLs 指定缓冲区访问方法。

如果 WDF 驱动程序通过使用对 i/o 目标使用的 i/o 方法不正确的方法来描述 i/o 请求的缓冲区，则该框架会更正缓冲区说明。 例如，如果驱动程序使用 MDL 描述它传递给 [**WdfIoTargetSendReadSynchronously**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendreadsynchronously)的缓冲区，并且 i/o 目标使用缓冲 i/o (这要求使用虚拟地址而不是 MDLs) 来指定缓冲区，则该框架会将 MDL 中的缓冲区描述转换为虚拟地址和长度。 但是，如果您的驱动程序以正确的格式指定缓冲区，则会更有效。

有关 framework 内存对象、后备链表列表、MDLs 和本地缓冲区的信息，请参阅 [使用内存缓冲区](using-memory-buffers.md)。

有关删除内存缓冲区的信息，请参阅 [内存缓冲区生命周期](memory-buffer-life-cycle.md)。

## <a name="accessing-data-buffers-for-buffered-io"></a><a href="" id="buffered"></a> 访问缓冲 i/o 的数据缓冲区


如果你的驱动程序使用的是缓冲 i/o，则其行为会根据数据请求的类型以及它是使用 KMDF 还是 UMDF 而发生更改。

<a href="" id="kmdf-drivers"></a>**KMDF 驱动程序**  

当 KMDF 驱动程序使用缓冲 i/o 时，i/o 管理器会创建一个中间缓冲区，驱动程序可以对每个请求类型进行访问。 下面是发生的具体情况：

-   写入请求。 在调用驱动程序堆栈之前，i/o 管理器会在调用应用的输入缓冲区中传输输入信息。 然后，KMDF 驱动程序从中间缓冲区读取输入信息，并将其写入到设备。
-   读取请求。 KMDF 驱动程序从设备读取信息，并将其存储在中间缓冲器中。 然后，i/o 管理器将输出数据从中间缓冲区复制到应用程序的输出缓冲区。
-   设备 i/o 控制请求。 KMDF 驱动程序在中间缓冲区中读取或写入该请求的数据。

<a href="" id="umdf-drivers"></a>**UMDF 驱动程序**  

当 UMDF 驱动程序使用缓冲 i/o 时，驱动程序主机进程会根据请求的类型创建一个或两个中间缓冲区。 下面是发生的具体情况：

-   写入请求。 该框架将创建一个缓冲区，从调用应用的输入缓冲区传输输入信息，然后调用驱动程序堆栈。 UMDF 驱动程序从中间缓冲区读取输入信息，并将其写入到设备。
-   读取请求。 UMDF 驱动程序从设备读取信息，并将其存储在框架所创建的缓冲区中。 驱动程序主机进程将输出数据从中间缓冲区复制到应用程序的输出缓冲区。
-   设备 i/o 控制请求。 框架创建两个缓冲区，对应于驱动程序可以访问的 IOCTL 的输入和输出缓冲区。 框架将这些输入信息从 IOCTL 复制到新的中间缓冲区，并使其可供驱动程序使用。 该框架不复制输出缓冲区的内容，因此，驱动程序不应尝试从该缓冲区中读取内容 (否则，它将最终读取垃圾数据) 。 驱动程序写入到输出缓冲区的任何数据都将复制回原始 IOCTL 缓冲区，并在 i/o 请求成功完成后返回到应用程序。 请注意，驱动程序写入到输入缓冲区的任何数据都将被丢弃，而不会返回给调用应用程序。

若要检索表示缓冲区的 framework memory 对象的句柄，KMDF 和 UMDF 驱动程序都调用 [**WdfRequestRetrieveInputMemory**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputmemory) 或 [**WdfRequestRetrieveOutputMemory**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory)，具体取决于这是读取还是写入请求。 然后，该驱动程序可以通过调用 [**WdfMemoryGetBuffer**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)来检索指向缓冲区的指针。 若要读取和写入缓冲区，驱动程序将调用 [**WdfMemoryCopyFromBuffer**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycopyfrombuffer) 或 [**WdfMemoryCopyToBuffer**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycopytobuffer)。

若要检索缓冲区的虚拟地址和长度，驱动程序将调用 [**WdfRequestRetrieveInputBuffer**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer) 或 [**WdfRequestRetrieveOutputBuffer**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer)。

若要为缓冲区分配和生成内存描述符列表 (MDL) ，KMDF 驱动程序将调用 [**WdfRequestRetrieveInputWdmMdl**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl) 或 [**WdfRequestRetrieveOutputWdmMdl**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl)。

## <a name="accessing-data-buffers-for-direct-io"></a><a href="" id="direct"></a> 访问直接 i/o 的数据缓冲区


<a href="" id="kmdf-drivers"></a>**KMDF 驱动程序**  

如果你的驱动程序使用直接 i/o，则 i/o 管理器将验证 i/o 请求的发起方 (通常) 指定用户模式应用程序的缓冲空间的可访问性，将缓冲区空间锁定为物理内存，然后为该驱动程序提供对缓冲区空间的直接访问。

<a href="" id="umdf-drivers"></a>**UMDF 驱动程序**  

如果你的驱动程序为直接 i/o 指定了一个首选项，并且满足了直接 i/o 的所有 UMDF 要求 (请参阅 [在 UMDF 驱动程序中管理缓冲区访问方法](managing-buffer-access-methods-in-umdf-drivers.md)) 中，该框架会将从 i/o 管理器接收的内存缓冲区直接映射到驱动程序的主机进程地址空间，从而为驱动程序提供对缓冲区空间的直接访问。

若要检索表示缓冲区空间的 framework memory 对象的句柄，驱动程序将调用 [**WdfRequestRetrieveInputMemory**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputmemory) 或 [**WdfRequestRetrieveOutputMemory**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory)。 然后，该驱动程序可以通过调用 [**WdfMemoryGetBuffer**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)来检索指向缓冲区的指针。 若要读取和写入缓冲区，驱动程序将调用 [**WdfMemoryCopyFromBuffer**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycopyfrombuffer) 或 [**WdfMemoryCopyToBuffer**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycopytobuffer)。

若要检索缓冲空间的虚拟地址和长度，驱动程序将调用 [**WdfRequestRetrieveInputBuffer**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer) 或 [**WdfRequestRetrieveOutputBuffer**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer)。

如果设备的驱动程序使用的是直接 i/o，则 i/o 管理器使用 MDLs 描述缓冲区。 若要检索指向缓冲区 MDL 的指针，KMDF 驱动程序将调用 [**WdfRequestRetrieveInputWdmMdl**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl) 或 [**WdfRequestRetrieveOutputWdmMdl**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl)。 UMDF 驱动程序无法访问 MDLs。

## <a name="accessing-data-buffers-for-neither-buffered-nor-direct-io"></a><a href="" id="neither"></a> 访问非缓冲和直接 i/o 的数据缓冲区


<a href="" id="kmdf-drivers"></a>**KMDF 驱动程序**  

如果你的驱动程序使用称为 *非缓冲 i/o 和直接 i/o 方法* 的缓冲区访问方法 (或，"两者都" 方法对于 short) ，i/o 管理器只是为该驱动程序提供了 i/o 请求的发起方为请求的缓冲区空间指定的虚拟地址。 I/o 管理器不会验证 i/o 请求的缓冲区空间，因此驱动程序必须验证缓冲区空间是否可访问，并将缓冲区空间锁定为物理内存。

只能在 i/o 请求的发起方的进程上下文中访问 i/o 管理器提供的虚拟地址。 仅保证驱动程序堆栈中的最高级别的驱动程序在发起方的进程上下文中执行。

若要获取对 i/o 请求的缓冲区空间的访问权限，最上层的驱动程序必须提供一个 [*EvtIoInCallerContext*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context) 回调函数。 每次收到驱动程序的 i/o 请求时，框架都会调用此回调函数。

如果请求的缓冲区访问方法为 "两者都不"，则 KMDF 驱动程序必须为每个缓冲区执行以下操作：

1.  调用 [**WdfRequestRetrieveUnsafeUserInputBuffer**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveunsafeuserinputbuffer) 或 [**WdfRequestRetrieveUnsafeUserOutputBuffer**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveunsafeuseroutputbuffer) 以获取缓冲区的虚拟地址。

2.  调用 [**WdfRequestProbeAndLockUserBufferForRead**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestprobeandlockuserbufferforread) 或 [**WdfRequestProbeAndLockUserBufferForWrite**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestprobeandlockuserbufferforwrite) 以探测并锁定缓冲区，并获取缓冲区的框架内存对象的句柄。

3.  在请求的 [上下文空间](using-request-object-context.md)中保存内存对象句柄。

4.  调用 [**WdfDeviceEnqueueRequest**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceenqueuerequest)，这将向框架返回请求。

然后，框架会将请求添加到驱动程序的一个 i/o 队列。 如果驱动程序提供了 [请求处理](request-handlers.md)程序，则框架最终将调用相应的请求处理程序。

请求处理程序可以从请求的上下文空间中检索请求的内存对象句柄。 驱动程序可以将句柄传递给 [**WdfMemoryGetBuffer**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer) ，以获取缓冲区的地址。

有时，最高级别的驱动程序必须使用前面的步骤来访问用户模式缓冲区，即使该驱动程序未使用 "两者都" 访问方法。 例如，假设驱动程序使用缓冲 i/o。 使用缓冲访问方法的 i/o 控制代码可能会将包含嵌入指针的结构传递到用户模式缓冲区。 在这种情况下，驱动程序必须提供一个 [*EvtIoInCallerContext*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context) 回调函数，该函数从结构中提取指针，然后使用前面的步骤2到4。

<a href="" id="umdf-drivers"></a>**UMDF 驱动程序**  

UMDF 不支持非缓冲和直接 i/o 类型的缓冲区，因此，UMDF 驱动程序永远不需要直接处理此类型的缓冲区。

但是，如果框架接收到用于从 i/o 管理器中进行读取或写入的缓冲区，则它会根据驱动程序选择的访问方法，将其提供给作为缓冲 i/o 或直接 i/o 的 UMDF 驱动程序。 如果框架接收到指定 "两个" 缓冲区方法的 IOCTL，则可以选择将 IOCTL 请求的缓冲区访问方法转换为缓冲 i/o，或根据 INF 指令的存在性来指示 i/o。 有关详细信息，请参阅 [在 UMDF 驱动程序中管理缓冲区访问方法](managing-buffer-access-methods-in-umdf-drivers.md) 。

 

