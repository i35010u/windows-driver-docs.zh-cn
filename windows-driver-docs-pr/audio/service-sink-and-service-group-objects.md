---
title: 服务接收器和服务组对象
description: 服务接收器和服务组对象
ms.assetid: 00e17e01-8889-4fae-a0ff-e110d7a9b21e
keywords:
- helper 对象 WDK 音频，服务接收器对象
- helper 对象 WDK 音频，服务组对象
- 服务接收器对象 WDK 音频
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
ms.openlocfilehash: 2c8308f461877f386518c3c042c07eaef5cf4ec4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830176"
---
# <a name="service-sink-and-service-group-objects"></a>服务接收器和服务组对象


## <span id="service_sink_and_service_group_objects"></span><span id="SERVICE_SINK_AND_SERVICE_GROUP_OBJECTS"></span>


PortCls 系统驱动程序实现了[IServiceSink](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iservicesink)和[IServiceGroup](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iservicegroup)接口，以实现端口和微型端口驱动程序的优势。 端口驱动程序使用这些接口将中断通知分发到其自己的服务例程，微型端口驱动程序可以选择使用这些接口来实现类似的目的。 IServiceSink 对象封装服务例程，IServiceGroup 对象表示 IServiceSink 对象组。 当服务组收到服务请求时，它会将该请求分发给其每个服务接收器。

[IServiceGroup](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iservicegroup)继承自[IServiceSink](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iservicesink)。 因为服务组也是服务接收器，所以服务组能够包含其他服务组，尽管音频驱动程序通常不使用此功能。 端口驱动程序当前使用服务组来 demultiplex 中断服务的请求，尽管服务组的功能大致足以使其对其他用途也有帮助。

微型端口驱动程序的中断服务例程（ISR）在端口驱动程序中调用以下通知方法之一：

[**IPortDMus：： Notify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iportdmus-notify)

[**IPortMidi：： Notify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportmidi-notify)

[**IPortWaveCyclic：： Notify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavecyclic-notify)

[**IPortWavePci：： Notify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepci-notify)

通知方法使用指向服务组的指针作为调用参数。 在此调用过程中，端口驱动程序调用服务组的[**IServiceSink：： RequestService**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iservicesink-requestservice)方法，该方法对延迟的过程调用（DPC）进行排队。 当 DPC 执行时，它会将服务请求转发到服务组中的所有成员对象。

小型端口驱动程序代码通常不需要调用任何[IServiceGroup](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iservicegroup)接口方法。 但是，端口驱动程序调用这些方法将其自己的[IServiceSink](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iservicesink)对象添加到它从微型端口驱动程序中获取的服务组。 微型端口驱动程序根据需要创建服务组对象，并将这些服务组与需要定期维护的微型端口和流对象相关联。 例如，WaveCyclic 微型端口驱动程序将流对象与其指定为 output 参数的服务组关联到[**IMiniportWaveCyclic：： newstream.ischecked**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavecyclic-newstream)方法。

在 WaveCyclic 微型端口驱动程序的上下文中，将所有流与一个服务组相关联会使端口驱动程序基于单个通知为所有流提供服务。 将每个流关联到其自己的服务组后，中断服务例程可以选择将由端口驱动程序在执行 DPC 期间提供服务的流。

当端口驱动程序调用以下初始化方法之一时，微型端口驱动程序会将对其服务组的引用输出到其中：

[**IMiniportDMus：： Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iminiportdmus-init)

[**IMiniportMidi：： Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportmidi-init)

[**IMiniportWavePci：： Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-init)

端口驱动程序将其自己的[IServiceSink](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iservicesink)对象添加到它从**Init**调用获取的服务组。 当微型端口驱动程序的 ISR 稍后调用**通知**发送发送到该服务组的通知时，服务组会将向端口驱动程序的 IServiceSink 对象转发通知的 DPC 排队，后者又通过调用以下服务方法之一：

[**IMiniportDMus：： Service**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iminiportdmus-service) （未使用）

[**IMiniportMidi：： Service**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportmidi-service)

[**IMiniportWavePci：： Service**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-service)

当端口驱动程序调用以下流创建方法之一时，微型端口驱动程序还输出对其服务组的引用：

[**IMiniportDMus：： Newstream.ischecked**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iminiportdmus-newstream)

[**IMiniportMidi：： Newstream.ischecked**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportmidi-newstream)

[**IMiniportWaveCyclic：： Newstream.ischecked**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavecyclic-newstream)

[**IMiniportWavePci：： Newstream.ischecked**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-newstream)

如前文所述，微型端口驱动程序可以选择为每个流创建不同的服务组，也可以在所有流中共享一个服务组。

以下方法可帮助 MIDI 和 Dmu 端口驱动程序避免丢弃硬件中断：

[**IPortMidi::RegisterServiceGroup**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportmidi-registerservicegroup)

[**IPortDMus::RegisterServiceGroup**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iportdmus-registerservicegroup)

在其**Init**方法执行期间，MIDI 或 dmu 微型端口驱动程序通常会在启动合成器之前调用端口驱动程序的**RegisterServiceGroup**方法。 此调用的目的是允许端口驱动程序将其 "服务接收器" 对象（包含其中断处理程序）插入服务组，然后硬件开始生成中断。 虽然**init**方法会将服务组指针输出到端口驱动程序，但端口驱动程序只能在从**Init**返回后使用此指针。

对于 WavePci 端口驱动程序，port 对象会将其自己的[IServiceSink](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iservicesink)对象添加到它从[**IMiniportWavePci：： newstream.ischecked**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-newstream)调用获取的服务组。 当微型端口驱动程序的 ISR 稍后调用**通知**将通知发送到该服务组时，服务组会将向该通知转发到端口驱动程序的 IServiceSink 对象的 DPC 进行排队，这反过来会执行以下操作：

-   通过调用服务方法[**IMiniportWavePciStream：： service**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-service)将通知转发到微型端口流。

-   触发已准备好触发的任何位置和/或时钟事件。

[IServiceSink](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iservicesink)接口支持单一方法：

[**IServiceSink：： RequestService**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iservicesink-requestservice)

[IServiceGroup](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iservicegroup)接口支持以下方法：

[**IServiceGroup::AddMember**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iservicegroup-addmember)

[**IServiceGroup::CancelDelayedService**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iservicegroup-canceldelayedservice)

[**IServiceGroup::RequestDelayedService**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iservicegroup-requestdelayedservice)

[**IServiceGroup::RemoveMember**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iservicegroup-removemember)

[**IServiceGroup::SupportDelayedService**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iservicegroup-supportdelayedservice)

此外，PortCls 系统驱动程序还提供了一个用于创建新服务组对象的[**PcNewServiceGroup**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewservicegroup)函数。 但是，不存在用于创建服务接收器对象的类似函数。 端口驱动程序只是将[IServiceSink](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iservicesink)接口添加到其主端口对象的实现-在创建对象时，它是服务接收器。 端口驱动程序可以将端口对象的 IServiceSink 接口添加到它从微型端口驱动程序的**Init**或**newstream.ischecked**方法接收的服务组。 为方便起见，头文件 Portcls 定义了**IMP\_IServiceSink**和**IMP\_IServiceGroup**常量，用于向驱动程序对象添加 IServiceSink 和[IServiceGroup](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iservicegroup)接口。

 

 




