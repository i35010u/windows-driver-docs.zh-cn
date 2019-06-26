---
title: 服务接收器和服务组对象
description: 服务接收器和服务组对象
ms.assetid: 00e17e01-8889-4fae-a0ff-e110d7a9b21e
keywords:
- 帮助程序对象 WDK 音频，服务接收器对象
- 帮助程序对象 WDK 音频，服务组对象
- 服务的接收器对象 WDK 音频
- 服务组对象 WDK 音频
- IServiceSink 接口
- IServiceGroup 接口
- 分发中断通知 WDK 音频
- 通知 WDK 音频
- 中断通知 WDK 音频
- 中断服务例程 WDK 音频
- Isr WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc28d79bf70282e6598f5fe502a786c4a35c9d0e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355263"
---
# <a name="service-sink-and-service-group-objects"></a>服务接收器和服务组对象


## <span id="service_sink_and_service_group_objects"></span><span id="SERVICE_SINK_AND_SERVICE_GROUP_OBJECTS"></span>


PortCls 系统驱动程序实现[IServiceSink](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iservicesink)并[IServiceGroup](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iservicegroup)为了方便端口和微型端口驱动程序的接口。 端口驱动程序使用这些接口进行分发到其自身服务例程，中断通知和微型端口驱动程序已针对类似目的使用这些接口的选项。 IServiceSink 对象封装服务例程和 IServiceGroup 对象表示一组 IServiceSink 对象。 当服务组收到服务请求时，它会分发到其服务接收器的每个请求。

[IServiceGroup](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iservicegroup)继承自[IServiceSink](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iservicesink)。 因为服务组也是服务接收器，所以，虽然音频驱动程序通常情况下进行无需使用此功能，并可以包含其他服务组，请服务组。 端口驱动程序当前使用服务组逐层中断服务的请求虽然服务组的功能通常足以使其用于其他目的还可能会有用。

微型端口驱动程序的中断服务例程 (ISR) 在端口驱动程序中调用以下通知方法之一：

[**IPortDMus::Notify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-iportdmus-notify)

[**IPortMidi::Notify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportmidi-notify)

[**IPortWaveCyclic::Notify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportwavecyclic-notify)

[**IPortWavePci::Notify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportwavepci-notify)

通知方法将一个指针，到服务组作为调用参数。 在此调用过程端口驱动程序调用服务组[ **IServiceSink::RequestService** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iservicesink-requestservice)方法延缓的过程调用 (DPC) 进行排队。 DPC 执行时，该服务将请求转发到服务组中的所有成员对象。

微型端口驱动程序代码通常不需要调用任何[IServiceGroup](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iservicegroup)接口方法。 但是，端口驱动程序调用这些方法来添加它自己[IServiceSink](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iservicesink)将从微型端口驱动程序获取的服务组的对象。 微型端口驱动程序创建所需的服务组对象，并将这些服务组与需要定期维护的微型端口和流对象相关联。 例如，WaveCyclic 微型端口驱动程序相关联的流对象作为输出参数为它指定的服务组[ **IMiniportWaveCyclic::NewStream** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavecyclic-newstream)方法。

在 WaveCyclic 微型端口驱动程序的上下文中，将与一个服务组关联的所有流将导致端口驱动程序服务基于一条通知的所有流。 将每个流与自己的服务组相关联允许选择将 DPC 执行期间接受通过端口驱动程序的流中断服务例程。

端口驱动程序调用以下初始化方法之一时，微型端口驱动程序将输出到其服务组的引用：

[**IMiniportDMus::Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-iminiportdmus-init)

[**IMiniportMidi::Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportmidi-init)

[**IMiniportWavePci::Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepci-init)

端口驱动程序会添加其自己[IServiceSink](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iservicesink)对象从其获取的服务组**Init**调用。 当微型端口驱动程序的 ISR 更高版本调用**通知**为了将通知发送到该服务组，服务组在将转发到端口驱动程序的 IServiceSink 对象，进而将转发到的通知的通知 DPC微型端口驱动程序，通过调用以下服务方法之一：

[**IMiniportDMus::Service** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-iminiportdmus-service) （未使用）

[**IMiniportMidi::Service**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportmidi-service)

[**IMiniportWavePci::Service**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepci-service)

当端口驱动程序调用以下的流创建方法之一时，微型端口驱动程序还会输出到其服务组的引用：

[**IMiniportDMus::NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-iminiportdmus-newstream)

[**IMiniportMidi::NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportmidi-newstream)

[**IMiniportWaveCyclic::NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavecyclic-newstream)

[**IMiniportWavePci::NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepci-newstream)

如前文所述，微型端口驱动程序已创建的每个流的不同的服务组或跨所有流共享单个服务组的选项。

Dmu 端口驱动程序避免删除硬件中断和以下方法帮助 MIDI:

[**IPortMidi::RegisterServiceGroup**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportmidi-registerservicegroup)

[**IPortDMus::RegisterServiceGroup**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-iportdmus-registerservicegroup)

执行期间其**Init**方法，MIDI 或 Dmu 微型端口驱动程序通常会调用端口驱动程序**RegisterServiceGroup**方法，然后再启动合成器。 此调用的目的是允许端口驱动程序插入服务接收器对象 （包含其中断处理程序） 到服务组硬件开始生成中断之前。 尽管**Init**方法将输出一个服务组指向端口驱动程序，请端口驱动程序可以使用此指针在返回后，才**Init**。

对于 WavePci 端口驱动程序，该端口对象将添加其自己[IServiceSink](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iservicesink)对象从其获取的服务组[ **IMiniportWavePci::NewStream** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepci-newstream)调用。 当微型端口驱动程序的 ISR 更高版本调用**通知**为了将通知发送到该服务组，服务组在将转发到端口驱动程序的 IServiceSink 对象，这反过来会执行以下通知 DPC:

-   通过调用服务方法转发到微型端口流的通知[ **IMiniportWavePciStream::Service**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepcistream-service)。

-   触发插针现在即可激发任何位置和/或时钟的事件。

[IServiceSink](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iservicesink)接口支持的一个方法：

[**IServiceSink::RequestService**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iservicesink-requestservice)

[IServiceGroup](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iservicegroup)接口支持以下方法：

[**IServiceGroup::AddMember**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iservicegroup-addmember)

[**IServiceGroup::CancelDelayedService**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iservicegroup-canceldelayedservice)

[**IServiceGroup::RequestDelayedService**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iservicegroup-requestdelayedservice)

[**IServiceGroup::RemoveMember**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iservicegroup-removemember)

[**IServiceGroup::SupportDelayedService**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iservicegroup-supportdelayedservice)

此外，还提供 PortCls 系统驱动程序[ **PcNewServiceGroup** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcnewservicegroup)函数来创建新的服务组对象。 但是，没有类似的函数用于创建服务的接收器对象存在。 端口驱动程序只需将添加[IServiceSink](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iservicesink)接口到其主端口对象-的实现时创建对象，因此是服务接收器。 端口驱动程序可以将端口对象的 IServiceSink 接口添加到其接收来自微型端口驱动程序的服务组**Init**或**NewStream**方法。 为方便起见，定义标头文件 Portcls.h **IMP\_IServiceSink**并**IMP\_IServiceGroup**添加 IServiceSink 常量和[IServiceGroup](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iservicegroup)驱动程序对象的接口。

 

 




