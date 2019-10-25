---
title: 资源列表对象
description: 资源列表对象
ms.assetid: a7f18d28-b78f-4b00-8cbb-9f62f5e88dfd
keywords:
- helper 对象 WDK 音频、资源列表对象
- 资源列表对象 WDK 音频
- IResourceList
- 配置资源列出 WDK 音频
- 启动时间资源分配 WDK 音频
- 硬件资源分配 WDK 音频
- 启动资源分配 WDK 音频
- 启动-设备例程 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 560cdc51eed20bf224f38a58a8726778193a149d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832434"
---
# <a name="resource-list-objects"></a>资源列表对象


## <span id="resource_list_objects"></span><span id="RESOURCE_LIST_OBJECTS"></span>


PortCls 系统驱动程序实现[IResourceList](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iresourcelist)接口，以获得微型端口驱动程序的优势。 IResourceList 对象表示一个配置资源列表，该列表是即插即用 manager 在设备启动时分配给设备的系统硬件资源的列表。 有关启动时资源分配的详细信息，请参阅[在函数驱动程序中启动设备](https://docs.microsoft.com/windows-hardware/drivers/kernel/starting-a-device-in-a-function-driver)。

资源列表包含以下类型的资源：

-   中断向量

-   DMA 通道

-   I/o 端口地址

-   总线相对内存地址块

有关资源类型的信息，请参阅[硬件资源](https://docs.microsoft.com/windows-hardware/drivers/kernel/hardware-resources)。

[IResourceList](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iresourcelist)对象封装资源列表的已翻译和未翻译（或原始）版本。 有关转换和未转换资源的详细信息，请参阅[将与总线相关的地址映射到虚拟地址](https://docs.microsoft.com/windows-hardware/drivers/kernel/mapping-bus-relative-addresses-to-virtual-addresses)。

[IResourceList](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iresourcelist)接口支持以下方法：

[**IResourceList::AddEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iresourcelist-addentry)

[**IResourceList::AddEntryFromParent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iresourcelist-addentryfromparent)

[**IResourceList::FindTranslatedEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iresourcelist-findtranslatedentry)

[**IResourceList::FindUntranslatedEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iresourcelist-finduntranslatedentry)

[**IResourceList::NumberOfEntries**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iresourcelist-numberofentries)

[**IResourceList::NumberOfEntriesOfType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iresourcelist-numberofentriesoftype)

[**IResourceList::TranslatedList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iresourcelist-translatedlist)

[**IResourceList::UntranslatedList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iresourcelist-untranslatedlist)

标头文件 Portcls 定义宏集以简化资源列表对象的处理。 这些宏将生成对[IResourceList](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iresourcelist)方法的调用。 有关详细信息，请参阅 IResourceList。

此外，Portcls 定义了一对用于创建资源列表的函数：

[**PcNewResourceList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewresourcelist)

[**PcNewResourceSublist**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewresourcesublist)

为了启动音频适配器卡上的设备，操作系统会调用适配器驱动程序的启动设备例程（请参阅[启动序列](startup-sequence.md)），并传入资源列表对象作为输入参数。 此列表包含操作系统已分配给适配器驱动程序的所有系统资源。

在启动设备例程中，适配器驱动程序将启动所有适配器驱动程序的设备（wave 设备、MIDI 设备，等等）。 为了管理每个设备，适配器驱动程序会创建一个微型端口驱动程序对象及其关联的端口驱动程序对象。 适配器驱动程序将资源列表中不同设备的资源列表中的资源。 出于此目的，驱动程序通常会调用[**PcNewResourceSublist**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewresourcesublist)为每个设备创建一个资源列表对象。 然后，驱动程序从父列表中将所选资源复制到不同的子列表，并尽可能多地调用[**IResourceList：： AddEntryFromParent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iresourcelist-addentryfromparent) 。 此外，适配器驱动程序可能会将某些资源分配给其自身。

接下来，启动设备例程调用每个端口驱动程序的[**IPort：： Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iport-init)方法，并传入设备的资源列表对象（包含子列表）作为输入参数。 每个端口驱动程序的**IPort：： init**方法会调用相应的微型端口驱动程序的 IMiniport*Xxx*：： init 方法，这是以下内容之一：

[**IMiniportDMus：： Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iminiportdmus-init)

[**IMiniportMidi：： Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportmidi-init)

[**IMiniportTopology：： Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiporttopology-init)

[**IMiniportWaveCyclic：： Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavecyclic-init)

[**IMiniportWavePci：： Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-init)

[**IPort：： init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iport-init)方法将其资源列表对象作为输入参数传递到 IMiniport*Xxx*：： init 方法。 然后，微型端口驱动程序可以使用资源列表中的 DMA 通道、中断和其他系统资源。

有关代码示例，请参阅 Microsoft Windows 驱动程序工具包（WDK）中的 Sb16 示例音频驱动程序。

 

 




