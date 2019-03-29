---
title: 资源列表对象
description: 资源列表对象
ms.assetid: a7f18d28-b78f-4b00-8cbb-9f62f5e88dfd
keywords:
- 帮助程序对象 WDK 音频，资源列表对象
- 资源列表对象 WDK 音频
- IResourceList
- 配置资源列出了 WDK 音频
- 启动时间资源分配 WDK 音频
- 硬件资源分配 WDK 音频
- 启动资源分配 WDK 音频
- 启动设备例程 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00f781a3ab77ca2e7fcd74e3b4a1cb2f4b5b697b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567830"
---
# <a name="resource-list-objects"></a>资源列表对象


## <span id="resource_list_objects"></span><span id="RESOURCE_LIST_OBJECTS"></span>


PortCls 系统驱动程序实现[IResourceList](https://msdn.microsoft.com/library/windows/hardware/ff536976)为了方便微型端口驱动程序的接口。 IResourceList 对象表示一个配置资源列表，它是插管理器在设备启动时将分配给设备的系统硬件资源的列表。 有关在启动时的资源分配的详细信息，请参阅[功能驱动程序中启动设备](https://msdn.microsoft.com/library/windows/hardware/ff563856)。

资源列表包含以下类型的资源：

-   中断向量

-   DMA 通道

-   I/O 端口地址

-   总线相对内存地址的

有关资源类型的信息，请参阅[硬件资源](https://msdn.microsoft.com/library/windows/hardware/ff547012)。

[IResourceList](https://msdn.microsoft.com/library/windows/hardware/ff536976)对象所封装的资源列表的已翻译和未转换 （或"原始"） 版本。 有关转换和翻译资源的详细信息，请参阅[映射到的虚拟地址的总线相对地址](https://msdn.microsoft.com/library/windows/hardware/ff554399)。

[IResourceList](https://msdn.microsoft.com/library/windows/hardware/ff536976)接口支持以下方法：

[**IResourceList::AddEntry**](https://msdn.microsoft.com/library/windows/hardware/ff536978)

[**IResourceList::AddEntryFromParent**](https://msdn.microsoft.com/library/windows/hardware/ff536981)

[**IResourceList::FindTranslatedEntry**](https://msdn.microsoft.com/library/windows/hardware/ff536982)

[**IResourceList::FindUntranslatedEntry**](https://msdn.microsoft.com/library/windows/hardware/ff536984)

[**IResourceList::NumberOfEntries**](https://msdn.microsoft.com/library/windows/hardware/ff536986)

[**IResourceList::NumberOfEntriesOfType**](https://msdn.microsoft.com/library/windows/hardware/ff536988)

[**IResourceList::TranslatedList**](https://msdn.microsoft.com/library/windows/hardware/ff536990)

[**IResourceList::UntranslatedList**](https://msdn.microsoft.com/library/windows/hardware/ff536991)

标头文件 Portcls.h 定义宏，以简化资源的列表对象的处理组。 这些宏生成调用到[IResourceList](https://msdn.microsoft.com/library/windows/hardware/ff536976)方法。 有关详细信息，请参阅 IResourceList。

此外，Portcls.h 定义一对函数来创建资源的列表：

[**PcNewResourceList**](https://msdn.microsoft.com/library/windows/hardware/ff537717)

[**PcNewResourceSublist**](https://msdn.microsoft.com/library/windows/hardware/ff537718)

若要启动音频适配器卡上的设备时，操作系统将调用适配器驱动程序的启动设备例程 (请参阅[启动序列](startup-sequence.md)) 并在资源列表对象作为输入参数中传递。 此列表包含操作系统已分配给适配器驱动程序的所有系统资源。

在开始设备例程中，适配器驱动程序启动的所有适配器驱动程序的设备 （波形设备、 MIDI 设备等）。 若要管理的每个设备，适配器驱动程序创建一个微型端口驱动程序对象和其关联的端口驱动程序对象。 适配器驱动程序将划分了资源之间的适配器卡中的各种设备的资源列表中。 为此，该驱动程序通常会调用[ **PcNewResourceSublist** ](https://msdn.microsoft.com/library/windows/hardware/ff537718)若要创建的每个设备的资源列表对象。 然后，该驱动程序调用[ **IResourceList::AddEntryFromParent** ](https://msdn.microsoft.com/library/windows/hardware/ff536981)为根据需要将所选的资源从父列表复制到各个子列表。 此外，适配器驱动程序可能会分配到其自身的一些资源。

接下来，开始设备例程调用每个端口驱动程序[ **IPort::Init** ](https://msdn.microsoft.com/library/windows/hardware/ff536943)方法，并在设备的资源列表对象中 （其中包含的子列表） 作为输入参数传递。 每个端口驱动程序**IPort::Init**方法将调用相应微型端口驱动程序的 IMiniport*Xxx*:: Init 方法中，这是以下之一：

[**IMiniportDMus::Init**](https://msdn.microsoft.com/library/windows/hardware/ff536700)

[**IMiniportMidi::Init**](https://msdn.microsoft.com/library/windows/hardware/ff536709)

[**IMiniportTopology::Init**](https://msdn.microsoft.com/library/windows/hardware/ff536713)

[**IMiniportWaveCyclic::Init**](https://msdn.microsoft.com/library/windows/hardware/ff536722)

[**IMiniportWavePci::Init**](https://msdn.microsoft.com/library/windows/hardware/ff536734)

[ **IPort::Init** ](https://msdn.microsoft.com/library/windows/hardware/ff536943)方法将其资源的列表对象传递给 IMiniport*Xxx*:: Init 方法作为输入参数。 微型端口驱动程序然后可以使用 DMA 通道、 中断和资源列表中的其他系统资源。

有关代码示例，请参阅 Sb16 示例音频驱动程序中 Microsoft Windows Driver Kit (WDK)。

 

 




