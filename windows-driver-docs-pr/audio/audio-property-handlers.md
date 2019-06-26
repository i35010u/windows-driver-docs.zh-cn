---
title: 音频属性处理程序
description: 音频属性处理程序
ms.assetid: 4bf176ae-b3fd-47e6-9802-a92ef5e9904f
keywords:
- 音频属性 WDK，处理程序
- WDM 音频属性 WDK，处理程序
- 处理程序 WDK 音频
- 属性处理程序 WDK 音频
- 设置属性 WDK 音频
- 获取属性 WDK 音频
- basic 支持查询 WDK 音频
- 自动化表 WDK 音频
- 筛选 WDK 音频，属性处理程序
- pin WDK 音频，属性处理程序
- 节点 WDK 音频，属性处理程序
ms.date: 08/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: f1a90f9ac8f1924d275c61f751a050d984ed8cb5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355649"
---
# <a name="audio-property-handlers"></a>音频属性处理程序


## <span id="audio_property_handlers"></span><span id="AUDIO_PROPERTY_HANDLERS"></span>


微型端口驱动程序存储有关每个属性，它支持的信息[ **PCPROPERTY\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ns-portcls-pcproperty_item)结构。 此结构包含有关属性的以下信息：

-   属性集 GUID 和属性 ID （或索引）

-   指向该属性的处理程序例程的函数指针

-   指定处理程序支持的属性操作的标志

微型端口驱动程序提供了自动化表 (由指定[ **PCAUTOMATION\_表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ns-portcls-pcautomation_table)结构) 的筛选器。 该驱动程序提供额外的自动化功能表的筛选器的固定类型和节点类型的每个 pin 或节点类型都有其自己的表。 每个自动化表包含 PCPROPERTY （可能为空） 数组\_项结构和每个这些结构描述的筛选器、 pin 或节点的一个属性。 客户端将属性请求发送到筛选器、 pin 或节点，端口驱动程序将通过自动化表将请求路由到相应的属性处理程序。

微型端口驱动程序可以指定每个属性的唯一属性处理程序例程。 但是，如果驱动程序处理多个相似的属性，这些可以有时将合并到单个处理程序例程为方便起见。 是否每个属性提供一个唯一的处理程序或将多个属性合并到单个处理程序是由驱动程序编写器的实施决策以及应该是透明的提交属性请求的客户端。

用户模式下客户端可以通过调用 Microsoft Win32 函数发送 get、 集或 basic 支持属性请求[ **DeviceIoControl** ](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)与*dwIoControlCode*调用参数设置为 IOCTL\_KS\_属性。 操作系统将转换到此调用[ **IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_irp)，其中它将调度到的类驱动程序。 有关详细信息，请参阅[KS 属性](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-properties)。

当客户端发送 KS 属性请求 (即，IOCTL\_KS\_属性我/O-控制 IRP) 到筛选器句柄或 pin 句柄，KS 系统驱动程序 (Ks.sys) 提供对 pin 对象的筛选器对象的端口驱动程序的请求。 如果微型端口驱动程序属性提供一个处理程序，则端口驱动程序将请求转发到处理程序。 转发请求之前, 端口驱动程序将信息从属性请求转换为指定的格式[ **PCPROPERTY\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ns-portcls-_pcproperty_request)结构。 端口驱动程序将此结构传递给微型端口驱动程序的处理程序。

**MajorTarget** PCPROPERTY 成员\_请求指向音频设备的主微型端口驱动程序接口。 例如，对于 WavePci 设备，这是指向微型端口驱动程序对象的指针[IMiniportWavePci](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavepci)接口。

在发送到筛选器的句柄，KS 属性请求的情况下**MinorTarget** PCPROPERTY 成员\_请求**NULL**。 如果请求发送到固定句柄**MinorTarget**指向流接口的 pin。 例如，对于 WavePci 设备，这是指向流对象的指针[IMiniportWavePciStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavepcistream)接口。

**实例**并**值**PCPROPERTY 成员\_请求指向输入和输出缓冲区中，分别，KS 属性请求。 (通过指定缓冲区*lpInBuffer*并*lpOutBuffer*的参数[ **DeviceIoControl** ](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)函数。)这些缓冲区包含的属性描述符 （实例数据） 和属性值 （操作数据） 中所述分别[音频驱动程序的属性集](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-drivers-property-sets)。 **值**成员指向输出缓冲区的开头，但**实例**指针相对于输入缓冲区开头的偏移量。

输入的缓冲区开头[ **KSPROPERTY** ](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))或[ **KSNODEPROPERTY** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)结构。 端口驱动程序将信息从这种结构复制到 PCPROPERTY\_请求结构**节点**， **PropertyItem**，并且**谓词**成员。 如果任何数据遵循缓冲区中的 KSPROPERTY 或 KSNODEPROPERTY 结构，端口驱动程序将加载**实例**用一个指针指向此数据成员。 否则，它设置**实例**到**NULL**。

如果输入的缓冲区开头的 KSPROPERTY 结构，不包含节点信息，端口驱动程序设置 PCPROPERTY\_请求结构**节点**ULONG(-1) 的成员。 在这种情况下，端口驱动程序会从微型端口驱动程序的自动化表相应的处理程序的筛选器或 pin，具体取决于是否属性请求的目标指定的筛选器句柄或 pin 句柄来调用。 （如果表没有指定属性的处理程序，端口驱动程序处理的请求而。）

如果输入的缓冲区开头 KSNODEPROPERTY 结构，端口驱动程序的节点 ID 将从复制此结构到 PCPROPERTY\_请求结构**节点**成员，并调用相应的处理程序节点的微型端口驱动程序的自动化表。 （同样，如果表没有指定属性的处理程序，端口驱动程序处理的请求而。）

端口驱动程序将查看 KSPROPERTY\_类型\_拓扑中的属性请求以确定这两个结构 KSPROPERTY 或 KSNODEPROPERTY，操作标志位驻留在输入缓冲区的开头：

-   如果设置此位，则该请求是针对节点属性，并输入的缓冲区开头 KSNODEPROPERTY 结构。

-   否则，输入的缓冲区开头 KSPROPERTY 结构。

详细了解 KSPROPERTY\_类型\_拓扑，请参阅[ **KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))。

PCPROPERTY\_请求结构**InstanceSize**并**ValueSize**成员指定指向的缓冲区的大小**实例**和**值**成员。 **ValueSize**等于属性请求的输出缓冲区的大小，但**InstanceSize**是遵循在输入缓冲区中的 KSPROPERTY 或 KSNODEPROPERTY 结构的数据的大小。 即**InstanceSize** KSPROPERTY 或 KSNODEPROPERTY 结构的大小减去输入缓冲区的大小。 如果没有其他数据将遵循此结构，端口驱动程序设置**InstanceSize**为零 (和**实例**到**NULL**)。

例如，如果客户端指定了[ **KSNODEPROPERTY\_音频\_通道**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)中输入缓冲区，端口驱动程序的实例数据的结构将传递该处理程序PCPROPERTY\_请求结构，其**实例**成员指向 KSNODEPROPERTY\_音频\_通道结构**通道**成员并且其**InstanceSize**成员包含的值

**sizeof**(KSNODEPROPERTY\_音频\_通道)- **sizeof**(KSNODEPROPERTY)

在提交之前的属性 get 请求检索属性值，客户端应分配微型端口驱动程序的属性处理程序可以将属性值写入到其中的输出缓冲区。 对于某些属性，输出缓冲区的大小依赖于设备，而且客户端必须查询所需的缓冲区大小的属性处理程序。 在这些情况下，客户端将提交与 nullptr 的输出缓冲区指针和输出缓冲区长度为零的初始属性请求。 通过返回的所需的缓冲区大小以及状态代码 STATUS_BUFFER_OVERFLOW 响应处理程序。 然后，客户端通过分配指定大小的输出缓冲区，并在第二个属性 get 请求中发送此缓冲区检索属性值。
 
如果指定的缓冲区大小太小，无法接收任何所需的信息，该方法将返回 STATUS_BUFFER_TOO_SMALL。 
 
在某些情况下，PortCls 端口驱动程序在具有非零输出缓冲区地址和大小的属性请求的响应中返回而不是 STATUS_BUFFER_OVERFLOW STATUS_BUFFER_TOO_SMALL。 在这种情况下不返回所需的缓冲区大小。 
 
有关详细信息，请参阅[使用 NTSTATUS 值](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-ntstatus-values)和这些博客文章：

- [如何返回后续的操作所需的字节数](https://blogs.msdn.microsoft.com/doronh/2006/12/12/how-to-return-the-number-of-bytes-required-for-a-subsequent-operation/)

- [STATUS_BUFFER_OVERFLOW 实际上应命名为 STATUS_BUFFER_OVERFLOW_PREVENTED](https://devblogs.microsoft.com/oldnewthing/?p=22863)




 

 




