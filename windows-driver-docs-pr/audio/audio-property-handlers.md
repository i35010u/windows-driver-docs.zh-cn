---
title: 音频属性处理程序
description: 音频属性处理程序
ms.assetid: 4bf176ae-b3fd-47e6-9802-a92ef5e9904f
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
ms.openlocfilehash: bd5c5ea8c8945f4ef1dd15d2d594ac6b21995c47
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831331"
---
# <a name="audio-property-handlers"></a>音频属性处理程序


## <span id="audio_property_handlers"></span><span id="AUDIO_PROPERTY_HANDLERS"></span>


微型端口驱动程序将有关它支持的每个属性的信息存储在[**PCPROPERTY\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcproperty_item)结构中。 此结构包含有关属性的下列信息：

-   属性集 GUID 和属性 ID （或索引）

-   指向属性的处理程序例程的函数指针

-   指定处理程序支持的属性操作的标志

微型端口驱动程序为筛选器提供自动化表（由[**PCAUTOMATION\_表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcautomation_table)结构指定）。 驱动程序为筛选器的 pin 类型和节点类型提供其他自动化表-每个 pin 或节点类型都有其自己的表。 每个自动化表都包含一个（可能为空） PCPROPERTY\_项结构的数组，其中每个结构都描述了筛选器、pin 或节点的一个属性。 当客户端将属性请求发送到筛选器、pin 或节点时，端口驱动程序会通过自动化表将请求路由到相应的属性处理程序。

微型端口驱动程序可以为每个属性指定唯一的属性处理程序例程。 但是，如果驱动程序处理几个类似的属性，有时可能会将它们合并为单个处理程序例程以便于方便。 无论是为每个属性提供唯一的处理程序，还是要将多个属性合并为单个处理程序，都是由驱动程序编写器做出的实现决策，并且应对提交属性请求的客户端是透明的。

用户模式客户端可以通过调用 Microsoft Win32 函数[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol) （将*dwIoControlCode*调用参数设置为 IOCTL\_KS\_属性）发送 get、set 或基本支持属性请求。 操作系统将此调用转换为[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)，并将其调度到类驱动程序。 有关详细信息，请参阅[KS 属性](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-properties)。

当客户端向筛选器句柄或固定句柄发送 KS 属性请求（即 IOCTL\_KS\_属性 i/o 控制 IRP）时，KS 系统驱动程序（Ks）会将请求传递给筛选器对象或固定对象的端口驱动程序。 如果微型端口驱动程序为属性提供处理程序，则端口驱动程序会将请求转发到处理程序。 转发请求之前，端口驱动程序将属性请求中的信息转换为[**PCPROPERTY\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-_pcproperty_request)结构指定的格式。 端口驱动程序将此结构传递给微型端口驱动程序的处理程序。

PCPROPERTY\_的**MajorTarget**成员指向音频设备的主要微型端口驱动程序接口。 例如，对于 WavePci 设备，这是一个指向微型端口驱动程序对象的[IMiniportWavePci](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavepci)接口的指针。

对于发送到筛选器句柄的 KS 属性请求，PCPROPERTY\_请求的**MinorTarget**成员为**NULL**。 如果请求发送到 pin 句柄， **MinorTarget**将指向该 pin 的流接口。 例如，对于 WavePci 设备，这是指向流对象的[IMiniportWavePciStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavepcistream)接口的指针。

PCPROPERTY 的**实例**和**值**成员分别\_为 KS 属性请求的输入和输出缓冲区。 （缓冲区由[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)函数的*lpInBuffer*和*lpOutBuffer*参数指定。）这些缓冲区分别包含属性描述符（实例数据）和属性值（操作数据），如[音频驱动程序属性集](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-drivers-property-sets)中所述。 **值**成员指向输出缓冲区的开头，但**实例**指针与输入缓冲区的开头偏移。

输入缓冲区以[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))或[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)结构开头。 端口驱动程序将此结构中的信息复制到 PCPROPERTY\_请求结构的**Node**、 **PropertyItem**和**Verb**成员。 如果任何数据遵循缓冲区中的 KSPROPERTY 或 KSNODEPROPERTY 结构，则端口驱动程序将使用指向此数据的指针加载**实例**成员。 否则，它会将**实例**设置为**NULL**。

如果输入缓冲区以 KSPROPERTY 结构（不包含任何节点信息）开头，则端口驱动程序会将 PCPROPERTY\_请求结构的**节点**成员设置为 ULONG （-1）。 在这种情况下，端口驱动程序会根据筛选器句柄或固定句柄是否指定属性请求的目标，从微型端口驱动程序的自动化表中调用相应的处理程序。 （如果表未指定属性的处理程序，则端口驱动程序将改为处理该请求。）

如果输入缓冲区以 KSNODEPROPERTY 结构开始，则端口驱动程序会将该结构中的节点 ID 复制到 PCPROPERTY\_请求结构的**节点**成员中，并从微型端口驱动程序的自动化调用适当的处理程序。表。 （同样，如果表未指定属性的处理程序，则端口驱动程序将改为处理该请求。）

端口驱动程序在属性请求的操作标志中检查 KSPROPERTY\_类型\_拓扑位，以确定两个结构中的哪一个 KSPROPERTY 或 KSNODEPROPERTY 位于输入缓冲区的开头：

-   如果设置了此位，则请求适用于 node 属性，输入缓冲区以 KSNODEPROPERTY 结构开始。

-   否则，输入缓冲区以 KSPROPERTY 结构开始。

有关 KSPROPERTY\_类型\_拓扑的详细信息，请参阅[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))。

PCPROPERTY\_请求结构的**InstanceSize**和**ValueSize**成员指定由**实例**和**值**成员指向的缓冲区的大小。 **ValueSize**等于属性请求的输出缓冲区的大小，但**InstanceSize**是输入缓冲区中 KSPROPERTY 或 KSNODEPROPERTY 结构之后的数据的大小。 也就是说， **InstanceSize**是输入缓冲区的大小减去 KSPROPERTY 或 KSNODEPROPERTY 结构的大小。 如果没有其他数据遵循此结构，则端口驱动程序将**InstanceSize**设置为零（并将**实例**设置为**NULL**）。

例如，如果客户端将[**KSNODEPROPERTY\_音频\_通道**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)结构指定为输入缓冲区中的实例数据，则端口驱动程序将向处理程序传递一个 PCPROPERTY\_请求结构，其**实例**成员指向 KSNODEPROPERTY\_音频\_通道结构的**通道**成员，其**InstanceSize**成员包含值

**sizeof**（KSNODEPROPERTY\_音频\_频道）- **sizeof**（KSNODEPROPERTY）

在提交 get 属性请求以检索属性值之前，客户端应分配一个输出缓冲区，微型端口驱动程序的属性处理程序可以将属性值写入其中。 对于某些属性，输出缓冲区的大小取决于设备，并且客户端必须在属性处理程序中查询所需的缓冲区大小。 在这些情况下，客户端将提交一个初始属性请求，其输出缓冲区指针为 nullptr，输出缓冲区长度为零。 处理程序通过返回所需的缓冲区大小以及状态代码 STATUS_BUFFER_OVERFLOW 来做出响应。 然后，客户端通过分配指定大小的输出缓冲区并在第二个 get 属性请求中发送此缓冲区来检索属性值。
 
如果指定的缓冲区大小太小，无法接收任何所需的信息，则该方法将返回 STATUS_BUFFER_TOO_SMALL。 
 
在某些情况下，PortCls 端口驱动程序返回 STATUS_BUFFER_TOO_SMALL 而不是 STATUS_BUFFER_OVERFLOW，以响应具有非零输出缓冲区地址和大小的属性请求。 在这种情况下，不会返回所需的缓冲区大小。 
 
有关详细信息，请参阅[使用 NTSTATUS 值](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-ntstatus-values)和这些博客文章：

- [如何返回后续操作所需的字节数](https://blogs.msdn.microsoft.com/doronh/2006/12/12/how-to-return-the-number-of-bytes-required-for-a-subsequent-operation/)

- [STATUS_BUFFER_OVERFLOW 确实应命名为 STATUS_BUFFER_OVERFLOW_PREVENTED](https://devblogs.microsoft.com/oldnewthing/?p=22863)




 

 




