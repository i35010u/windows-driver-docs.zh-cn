---
title: DualView 高级实施详细信息
description: DualView 高级实施详细信息
ms.assetid: 07fb7640-d723-4dc0-9403-9f70a75518f1
keywords:
- 双屏显示 WDK 视频微型端口
- SingleView WDK 视频微型端口
- 逻辑子关系 WDK 视频微型端口
- 物理子关系 WDK 视频微型端口
- 子设备 WDK 视频微型端口
- 内存 WDK 双屏
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5cd436932451a292f402cb3e4c89c0e28899252b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839746"
---
# <a name="dualview-advanced-implementation-details"></a>DualView 高级实施详细信息


## <span id="ddk_dualview_advanced_implementation_details_gg"></span><span id="DDK_DUALVIEW_ADVANCED_IMPLEMENTATION_DETAILS_GG"></span>


当启用或禁用其辅助视图时，理想的双屏实现应会识别。 禁用辅助视图后，主视图的行为应与未启用双屏显示的行为相同。 这意味着：

-   主显示器可以访问视频内存的所有部分。

-   在便携式计算机上，可以将主显示器切换到任何子显示设备。

### <a name="span-idvideo_memory_arrangementspanspan-idvideo_memory_arrangementspanspan-idvideo_memory_arrangementspanvideo-memory-arrangement"></a><span id="Video_Memory_Arrangement"></span><span id="video_memory_arrangement"></span><span id="VIDEO_MEMORY_ARRANGEMENT"></span>视频内存排列

在理想的双屏实现中，内存缓冲区使用率经过优化，以便在禁用辅助显示器时主显示器使用整个视频内存。 但这种优化是可选的;要使用的视频内存分配策略完全取决于驱动程序编写器。

禁用辅助视图后，主视图应能够访问视频内存的所有部分，以最大程度地提高系统性能。 但是，当启用辅助视图时，微型端口驱动程序不应只适合主视图的内存。 相反，微型端口驱动程序应在更改为双屏模式之前为辅助视图保留视频内存。 从 Windows XP 开始（并继续使用更高版本的操作系统），会出现一个新的视频请求， [**IOCTL\_视频\_开关\_双屏**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_switch_dualview)，以帮助驱动程序编写器处理视频内存排列。 当 Windows XP （及更高版本）处理对**ChangeDisplaySettings**函数的调用（如 Windows SDK 文档中所述）时，它会将 IOCTL 发送\_视频\_\_向每个双屏相关的视图的双屏请求尝试更改模式。 驱动程序可以使用这些信息在需要时预先进行视频内存排列。

下图说明了显示禁用了双屏的视频内存的排列方式。

![阐释禁用了双屏的内存排列的关系图](images/memfig1.png)

下图说明了启用了双屏显示的视频内存的建议排列方式。 每个视图都有自己的屏幕缓冲区和屏幕外堆。

![说明启用了双屏的内存排列的关系图](images/memfig2.png)

### <a name="span-idchild_relationshipsspanspan-idchild_relationshipsspanspan-idchild_relationshipsspanchild-relationships"></a><span id="Child_Relationships"></span><span id="child_relationships"></span><span id="CHILD_RELATIONSHIPS"></span>子关系

典型的移动视频芯片具有多个子设备，如 LCD、CRT 和电视。 在 SingleView 模式下，如下图所示，主视图拥有所有这些子设备，而辅助视图不拥有任何子设备。 用户可以将主视图从一个子设备切换到另一个。 一次只能有一个设备处于活动状态。

![说明 singleview 模式的关系图](images/childfig1.png)

但在双屏模式下，每个子对象都可以分配给不同的视图;问题在于哪个视图与哪个子级关联。 可以通过两种方式描述视图与设备之间的关系：在*物理子关系*和*逻辑子关系*方面。

*物理子关系*反映了适配器的视频芯片及其显示设备之间的关系。 系统启动后，视频芯片与显示设备之间的物理关系永远不会改变。 在上图和下图中，视频芯片拥有 LCD、CRT 和电视显示设备;因此，所有三个显示设备都是视频芯片的物理子级。

*逻辑子关系*反映视图和显示设备之间的动态关系。 在下图中，已启用了双屏，这种情况是主视图（视图1）拥有 LCD 设备，而辅助视图（视图2）拥有 CRT 设备和电视设备。 另一种方法是，LCD 设备是主视图的逻辑子级，而 CRT 和电视设备是辅助视图的逻辑子级。 微型端口驱动程序通过 IOCTL\_视频报告逻辑子关系[ **\_获取\_子\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_get_child_state)请求。

![演示双屏模式的关系图](images/childfig2.png)

还有一个附加点。 启用 "双屏显示" 后，主视图可能会自动切换子节点。 在 SingleView 模式下，只有与主视图（仅限）关联的 CRT 处于活动状态。 所有其他显示设备都处于非活动状态。 启用了双屏后，上图显示了主视图切换到 LCD 设备上的显示，而 CRT 是辅助视图的子节点。 此开关对于便携式计算机可能是必需的，因为辅助视图是可移动的，这意味着无法将 LCD 设备与该视图相关联。 是否以及如何使此开关完全受微型端口驱动程序的控制。

 

 





