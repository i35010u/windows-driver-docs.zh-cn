---
title: 双视图高级实现详细信息
description: 双视图高级实现详细信息
ms.assetid: 07fb7640-d723-4dc0-9403-9f70a75518f1
keywords:
- 双视图 WDK 微型端口
- SingleView WDK 微型端口
- 逻辑子关系 WDK 微型端口
- 物理子关系 WDK 微型端口
- 子设备 WDK 微型端口
- 内存 WDK 双视图
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e685b11746d2a58440d7634b1303727b1cd3f59
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524423"
---
# <a name="dualview-advanced-implementation-details"></a>双视图高级实现详细信息


## <span id="ddk_dualview_advanced_implementation_details_gg"></span><span id="DDK_DUALVIEW_ADVANCED_IMPLEMENTATION_DETAILS_GG"></span>


启用或禁用其辅助视图时，应识别理想双视图实现。 当辅助视图都被禁用时，而启用的双视图不像行为主视图。 这意味着：

-   主显示器可以访问视频内存的所有的部分。

-   便携式计算机在计算机上，主显示器可以切换到的任何子显示设备。

### <a name="span-idvideomemoryarrangementspanspan-idvideomemoryarrangementspanspan-idvideomemoryarrangementspanvideo-memory-arrangement"></a><span id="Video_Memory_Arrangement"></span><span id="video_memory_arrangement"></span><span id="VIDEO_MEMORY_ARRANGEMENT"></span>视频内存排列方式

在理想的双视图实现中，内存缓冲区使用情况进行优化，以便辅助显示处于禁用状态时使用的主显示整个视频内存。 这种优化是可选的但是;要使用的视频内存分配策略完全由驱动程序编写器。

禁用辅助视图后，主视图应能够访问的视频内存，以使系统性能最大化所有部分。 启用辅助视图后，但是，微型端口驱动程序应只需相应的主视图的内存。 相反，微型端口驱动程序应保留为辅助视图，再更改为双视图模式的视频内存。 从 Windows XP （和更高版本的操作系统版本继续执行），还有新的视频请求时， [ **IOCTL\_视频\_交换机\_双视图**](https://msdn.microsoft.com/library/windows/hardware/ff568151)到帮助驱动程序编写器处理视频内存排列方式。 时 Windows XP （和更高版本） 处理调用**ChangeDisplaySettings**函数 （Windows SDK 文档中介绍），它将发送 IOCTL\_视频\_交换机\_双视图请求到每个双视图相关视图之前它会尝试更改的模式。 驱动程序可以使用该信息以使之前其需要的视频内存排列方式。

下图演示双视图禁用了视频内存的排列方式。

![说明内存排列方式与禁用的双视图的关系图](images/memfig1.png)

下图演示双视图启用了视频内存的建议的排列。 每个视图都有其自己的屏幕缓冲区和屏幕外的堆。

![说明内存排列方式与启用双视图的关系图](images/memfig2.png)

### <a name="span-idchildrelationshipsspanspan-idchildrelationshipsspanspan-idchildrelationshipsspanchild-relationships"></a><span id="Child_Relationships"></span><span id="child_relationships"></span><span id="CHILD_RELATIONSHIPS"></span>子关系

典型的移动视频芯片具有多个子设备，如 LCD、 CRT 和电视节目。 在 SingleView 模式下下, 图中所示的主视图拥有所有这些子设备，而辅助视图拥有其中任何一个。 用户可以切换到另一个子设备中的主视图。 只能一次，一台设备可处于活动状态。

![关系图演示 singleview 模式](images/childfig1.png)

在双视图模式中，但是，每个子级可以分配到不同的视图;现在的问题是哪种视图是哪个子与相关联。 可以通过两种方式描述视图和设备之间的关系： 按照*物理子关系*和的*逻辑子关系*。

*物理子关系*反映适配器的视频芯片和其显示设备之间的关系。 在系统启动后，永远不会更改视频的芯片和显示设备之间的物理关系。 在前面的图和下图中，视频芯片拥有 LCD、 CRT 和电视显示设备;因此，所有三个显示设备是物理的视频芯片的子级。

*逻辑子关系*反映在视图和显示设备之间的动态关系。 在下图中，已启用双视图，且这种情况是主视图 (视图 1) 拥有 LCD 设备，而辅助视图 (视图 2) 拥有 CRT 和电视节目的设备。 另一种说法是 LCD 设备的主视图的逻辑子 CRT 和电视节目设备时的逻辑子级的辅助视图。 微型端口驱动程序报告通过逻辑子关系[ **IOCTL\_视频\_获取\_子\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567801)请求。

![关系图演示双视图模式](images/childfig2.png)

还有一点保持。 启用双视图后，主视图可能会自动切换子级。 在 SingleView 模式下，仅 CRT，这是与主 （并且只有一个） 视图相关联，处于活动状态。 所有其他显示设备处于非活动状态。 已启用双视图后，上图显示了已切换主视图以显示 LCD 设备上的辅助视图子 CRT 时。 此开关可能所需的便携式计算机由于，辅助视图是可移除，这意味着 LCD 设备不能为与该视图相关联。 是否以及如何使此开关是完全受控制的微型端口驱动程序。

 

 





