---
title: 音频属性处理程序
description: 音频属性处理程序
keywords:
- 音频属性 WDK，处理程序
- WDM 音频属性 WDK，处理程序
- 处理程序 WDK 音频
- 属性处理程序 WDK 音频
- 设置-属性 WDK 音频
- 获取-属性 WDK 音频
- 基本-支持查询 WDK 音频
- 自动化表 WDK 音频
- 筛选 WDK 音频，属性处理程序
- 锁定 WDK 音频，属性处理程序
- 节点 WDK 音频，属性处理程序
ms.date: 08/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: faaba8b346cb9107f2c0bdeaf0e33a8d70257dc8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789375"
---
# <a name="audio-property-handlers"></a>音频属性处理程序


## <span id="audio_property_handlers"></span><span id="AUDIO_PROPERTY_HANDLERS"></span>


微型端口驱动程序将有关它所支持的每个属性的信息存储在 [**PCPROPERTY \_ 项**](/windows-hardware/drivers/ddi/portcls/ns-portcls-pcproperty_item) 结构中。 此结构包含有关属性的下列信息：

-   属性集 GUID 和属性 ID (或索引) 

-   指向属性的处理程序例程的函数指针

-   指定处理程序支持的属性操作的标志

微型端口驱动程序提供 [**PCAUTOMATION \_ 表**](/windows-hardware/drivers/ddi/portcls/ns-portcls-pcautomation_table) 结构) 为筛选器指定 (自动化表。 驱动程序为筛选器的 pin 类型和节点类型提供其他自动化表-每个 pin 或节点类型都有其自己的表。 每个自动化表都包含一个 (可能为空的 PCPROPERTY \_ 项结构) 数组，其中每个结构都描述了筛选器、pin 或节点的一个属性。 当客户端将属性请求发送到筛选器、pin 或节点时，端口驱动程序会通过自动化表将请求路由到相应的属性处理程序。

微型端口驱动程序可以为每个属性指定唯一的属性处理程序例程。 但是，如果驱动程序处理几个类似的属性，有时可能会将它们合并为单个处理程序例程以便于方便。 无论是为每个属性提供唯一的处理程序，还是要将多个属性合并为单个处理程序，都是由驱动程序编写器做出的实现决策，并且应对提交属性请求的客户端是透明的。

用户模式客户端可以通过调用 Microsoft Win32 函数 [**DeviceIoControl**](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol) ，并将 *dwIoControlCode* 调用参数设置为 IOCTL KS 属性来发送 get、set 或基本支持的属性请求 \_ \_ 。 操作系统将此调用转换为 [**IRP**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)，并将其调度到类驱动程序。 有关详细信息，请参阅 [KS 属性](../stream/ks-properties.md)。

当客户端发送 KS 属性请求 (即，IOCTL \_ KS \_ 属性 I/O 控制 IRP) 到筛选器句柄或固定句柄，则 KS 系统驱动程序 ( # A0) 将请求传递给筛选器对象或固定对象的端口驱动程序。 如果微型端口驱动程序为属性提供处理程序，则端口驱动程序会将请求转发到处理程序。 转发请求之前，端口驱动程序将属性请求中的信息转换为 [**PCPROPERTY \_ 请求**](/windows-hardware/drivers/ddi/portcls/ns-portcls-_pcproperty_request) 结构指定的格式。 端口驱动程序将此结构传递给微型端口驱动程序的处理程序。

PCPROPERTY 请求的 **MajorTarget** 成员 \_ 指向音频设备的主要微型端口驱动程序接口。 例如，对于 WavePci 设备，这是一个指向微型端口驱动程序对象的 [IMiniportWavePci](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavepci) 接口的指针。

对于发送到筛选器句柄的 KS 属性请求，PCPROPERTY 请求的 **MinorTarget** 成员 \_ 为 **NULL**。 如果请求发送到 pin 句柄， **MinorTarget** 将指向该 pin 的流接口。 例如，对于 WavePci 设备，这是指向流对象的 [IMiniportWavePciStream](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavepcistream) 接口的指针。

PCPROPERTY 请求点的 **实例** 和 **值** 成员 \_ 分别为 KS 属性请求的输入和输出缓冲区。  (缓冲区由 [**DeviceIoControl**](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol)函数的 *lpInBuffer* 和 *LpOutBuffer* 参数指定。 ) 这些缓冲区分别包含 (实例数据) 和属性值 (操作数据) ，如 [音频驱动程序属性集中](./audio-drivers-property-sets.md)所述。 **值** 成员指向输出缓冲区的开头，但 **实例** 指针与输入缓冲区的开头偏移。

输入缓冲区以 [**KSPROPERTY**](/previous-versions/ff564262(v=vs.85)) 或 [**KSNODEPROPERTY**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty) 结构开头。 端口驱动程序将此结构中的信息复制到 PCPROPERTY \_ 请求结构的 **Node**、 **PropertyItem** 和 **Verb** 成员中。 如果任何数据遵循缓冲区中的 KSPROPERTY 或 KSNODEPROPERTY 结构，则端口驱动程序将使用指向此数据的指针加载 **实例** 成员。 否则，它会将 **实例** 设置为 **NULL**。

如果输入缓冲区以 KSPROPERTY 结构（不包含任何节点信息）开头，则端口驱动程序会将 PCPROPERTY \_ 请求结构的 **节点** 成员设置为 ULONG (-1) 。 在这种情况下，端口驱动程序会根据筛选器句柄或固定句柄是否指定属性请求的目标，从微型端口驱动程序的自动化表中调用相应的处理程序。  (如果表未指定属性的处理程序，则端口驱动程序将改为处理该请求。 ) 

如果输入缓冲区以 KSNODEPROPERTY 结构开始，则端口驱动程序会将该结构中的节点 ID 复制到 PCPROPERTY \_ 请求结构的 **节点** 成员中，并从该节点的微型端口驱动程序的自动化表中调用相应的处理程序。 再次 (，如果表未指定属性的处理程序，则端口驱动程序将改为处理该请求。 ) 

端口驱动程序将检查 \_ \_ 属性请求的操作标志中的 KSPROPERTY 类型拓扑位，以确定两个结构（KSPROPERTY 或 KSNODEPROPERTY）位于输入缓冲区的开头：

-   如果设置了此位，则请求适用于 node 属性，输入缓冲区以 KSNODEPROPERTY 结构开始。

-   否则，输入缓冲区以 KSPROPERTY 结构开始。

有关 KSPROPERTY 类型拓扑的详细信息 \_ \_ ，请参阅 [**KSPROPERTY**](/previous-versions/ff564262(v=vs.85))。

PCPROPERTY \_ 请求结构的 **InstanceSize** 和 **ValueSize** 成员指定由 **实例** 和 **值** 成员指向的缓冲区的大小。 **ValueSize** 等于属性请求的输出缓冲区的大小，但 **InstanceSize** 是输入缓冲区中 KSPROPERTY 或 KSNODEPROPERTY 结构之后的数据的大小。 也就是说， **InstanceSize** 是输入缓冲区的大小减去 KSPROPERTY 或 KSNODEPROPERTY 结构的大小。 如果没有其他数据遵循此结构，则端口驱动程序会将 **InstanceSize** 设置为零 (并将 **实例** 设置为 **NULL**) 。

例如，如果客户端将 KSNODEPROPERTY 的 [**\_ 音频 \_ 通道**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel) 结构指定为输入缓冲区中的实例数据，则端口驱动程序会将该处理程序的 PCPROPERTY \_ 请求结构（其 **实例** 成员指向 KSNODEPROPERTY \_ 音频 \_ 通道结构的 **通道** 成员）传递给该请求结构，并将其 **InstanceSize** 成员包含值。

**sizeof** (KSNODEPROPERTY \_ 音频 \_ 通道) - **sizeof** (KSNODEPROPERTY) 

在提交 get 属性请求以检索属性值之前，客户端应分配一个输出缓冲区，微型端口驱动程序的属性处理程序可以将属性值写入其中。 对于某些属性，输出缓冲区的大小取决于设备，并且客户端必须在属性处理程序中查询所需的缓冲区大小。 在这些情况下，客户端将提交一个初始属性请求，其输出缓冲区指针为 nullptr，输出缓冲区长度为零。 处理程序通过返回所需的缓冲区大小以及状态代码 STATUS_BUFFER_OVERFLOW 来做出响应。 然后，客户端通过分配指定大小的输出缓冲区并在第二个 get 属性请求中发送此缓冲区来检索属性值。
 
如果指定的缓冲区大小太小，无法接收任何所需的信息，则该方法将返回 STATUS_BUFFER_TOO_SMALL。 
 
在某些情况下，PortCls 端口驱动程序会返回 STATUS_BUFFER_TOO_SMALL 而不是 STATUS_BUFFER_OVERFLOW 来响应具有非零输出缓冲区地址和大小的属性请求。 在这种情况下，不会返回所需的缓冲区大小。 
 
有关详细信息，请参阅 [使用 NTSTATUS 值](../kernel/using-ntstatus-values.md) 和这些博客文章：

- [如何返回后续操作所需的字节数](/archive/blogs/doronh/how-to-return-the-number-of-bytes-required-for-a-subsequent-operation)

- [STATUS_BUFFER_OVERFLOW 确实应命名为 STATUS_BUFFER_OVERFLOW_PREVENTED](https://devblogs.microsoft.com/oldnewthing/?p=22863)




 

