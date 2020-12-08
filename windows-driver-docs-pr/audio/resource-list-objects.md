---
title: 资源列表对象
description: 资源列表对象
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
ms.openlocfilehash: d7834111df56f2732c687fbf57c6a7d77edb772f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800703"
---
# <a name="resource-list-objects"></a>资源列表对象


## <span id="resource_list_objects"></span><span id="RESOURCE_LIST_OBJECTS"></span>


PortCls 系统驱动程序实现 [IResourceList](/windows-hardware/drivers/ddi/portcls/nn-portcls-iresourcelist) 接口，以获得微型端口驱动程序的优势。 IResourceList 对象表示一个配置资源列表，该列表是即插即用 manager 在设备启动时分配给设备的系统硬件资源的列表。 有关启动时资源分配的详细信息，请参阅 [在函数驱动程序中启动设备](../kernel/starting-a-device-in-a-function-driver.md)。

资源列表包含以下类型的资源：

-   中断向量

-   DMA 通道

-   I/o 端口地址

-   总线相对内存地址块

有关资源类型的信息，请参阅 [硬件资源](../kernel/hardware-resources.md)。

[IResourceList](/windows-hardware/drivers/ddi/portcls/nn-portcls-iresourcelist)对象封装资源列表的已翻译和未翻译的 (或 "原始" ) 版本。 有关转换和未转换资源的详细信息，请参阅 [将 Bus-Relative 地址映射到虚拟地址](../kernel/mapping-bus-relative-addresses-to-virtual-addresses.md)。

[IResourceList](/windows-hardware/drivers/ddi/portcls/nn-portcls-iresourcelist)接口支持以下方法：

[**IResourceList::AddEntry**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iresourcelist-addentry)

[**IResourceList::AddEntryFromParent**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iresourcelist-addentryfromparent)

[**IResourceList::FindTranslatedEntry**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iresourcelist-findtranslatedentry)

[**IResourceList::FindUntranslatedEntry**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iresourcelist-finduntranslatedentry)

[**IResourceList::NumberOfEntries**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iresourcelist-numberofentries)

[**IResourceList::NumberOfEntriesOfType**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iresourcelist-numberofentriesoftype)

[**IResourceList::TranslatedList**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iresourcelist-translatedlist)

[**IResourceList::UntranslatedList**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iresourcelist-untranslatedlist)

标头文件 Portcls 定义宏集以简化资源列表对象的处理。 这些宏将生成对 [IResourceList](/windows-hardware/drivers/ddi/portcls/nn-portcls-iresourcelist) 方法的调用。 有关详细信息，请参阅 IResourceList。

此外，Portcls 定义了一对用于创建资源列表的函数：

[**PcNewResourceList**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewresourcelist)

[**PcNewResourceSublist**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewresourcesublist)

若要启动音频适配器卡上的设备，操作系统会调用适配器驱动程序的启动设备例程 (参阅 [启动序列](startup-sequence.md)) 并传入资源列表对象作为输入参数。 此列表包含操作系统已分配给适配器驱动程序的所有系统资源。

在启动设备例程中，适配器驱动程序将启动所有适配器驱动程序的设备 (wave 设备、MIDI 设备等) 。 为了管理每个设备，适配器驱动程序会创建一个微型端口驱动程序对象及其关联的端口驱动程序对象。 适配器驱动程序将资源列表中不同设备的资源列表中的资源。 出于此目的，驱动程序通常会调用 [**PcNewResourceSublist**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewresourcesublist) 为每个设备创建一个资源列表对象。 然后，驱动程序从父列表中将所选资源复制到不同的子列表，并尽可能多地调用 [**IResourceList：： AddEntryFromParent**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iresourcelist-addentryfromparent) 。 此外，适配器驱动程序可能会将某些资源分配给其自身。

接下来，启动设备例程调用每个端口驱动程序的 [**IPort：： Init**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iport-init) 方法，并传入设备的资源列表对象 (包含子列表的) 作为输入参数。 每个端口驱动程序的 **IPort：： init** 方法会调用相应的微型端口驱动程序的 IMiniport *Xxx*：： init 方法，这是以下内容之一：

[**IMiniportDMus：： Init**](/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iminiportdmus-init)

[**IMiniportMidi：： Init**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportmidi-init)

[**IMiniportTopology：： Init**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiporttopology-init)

[**IMiniportWaveCyclic：： Init**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavecyclic-init)

[**IMiniportWavePci：： Init**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-init)

[**IPort：： init**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iport-init)方法将其资源列表对象作为输入参数传递到 IMiniport *Xxx*：： init 方法。 然后，微型端口驱动程序可以使用资源列表中的 DMA 通道、中断和其他系统资源。

有关代码示例，请参阅 Microsoft Windows 驱动程序工具包 (WDK) 中的 Sb16 示例音频驱动程序。

 

