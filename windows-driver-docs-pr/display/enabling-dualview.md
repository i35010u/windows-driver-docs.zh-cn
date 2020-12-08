---
title: 启用 DualView
description: 启用 DualView
keywords:
- 双屏显示 WDK 视频微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 994a2564d6967ffdcdd0b0b9cbcc59c67a55e006
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832777"
---
# <a name="enabling-dualview"></a>启用 DualView


## <span id="ddk_enabling_dualview_gg"></span><span id="DDK_ENABLING_DUALVIEW_GG"></span>


对于最小的双屏实现，请执行以下操作：

-   在微型端口驱动程序的 [*HwVidFindAdapter*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_find_adapter) 返回之前，调用新的视频端口驱动程序入口点 [**VideoPortCreateSecondaryDisplay**](/windows-hardware/drivers/ddi/video/nf-video-videoportcreatesecondarydisplay)，为辅助视图生成设备扩展。 在 "辅助设备扩展" 中，添加两个新的私有成员：

    1.  一个标志，用于指示设备扩展适用于辅助显示器
    2.  一个指针，其中包含主显示器的设备扩展的地址
-   必须在微型端口驱动程序的 [*HwVidStartIO*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_start_io) 回调例程中进行四项更改，修改它响应显示的四个 IOCTL 请求的方式。 以下列表中的第四项提供了两种方法来实现相同的结果。

    1.  为了响应 [**IOCTL \_ 视频 \_ 映射 \_ 视频 \_ 内存**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_map_video_memory) 请求，应正确设置每个视图的帧缓冲区指针和长度。
    2.  应将对 [**IOCTL \_ 视频 \_ 集 \_ 当前 \_ 模式**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_set_current_mode) 请求的响应设置为特定于辅助视图。
    3.  对 [**IOCTL \_ 视频 \_ 重置 \_ 设备**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_reset_device) 请求的响应取决于设备是主显示器还是辅助显示器。 如果设备是主显示器，则执行任何所需的操作。 但是，如果设备为辅助显示器，则建议不要执行任何操作。
    4.  更改对 [**IOCTL \_ 视频 \_ 共享 \_ 视频 \_ 内存**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_share_video_memory) 请求的响应，以获取两个视图的正确映射。 请注意，对于 DirectDraw 实现，可以修改 DirectDraw 函数 [*DdMapMemory*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mapmemory) 以获取两个视图的正确映射。
-   显示驱动程序应负责逻辑帧缓冲区地址和物理视频内存偏移量之间的调整。 这对于 DirectDraw 实现尤其重要，因为在双屏显示中，主表面可能会从内存位置0以外的任何位置启动。 显示驱动程序应通过在处理 [**vmiData**](/windows/win32/api/winddi/nf-winddi-drvgetdirectdrawinfo)时使用相应的视频内存偏移量填充 **pHalInfo- &gt; VmiData. pvPrimary** 和 **PHalInfo- &gt; fpPrimary** ，来通知 DirectDraw。

### <a name="span-idadditional_implementation_notesspanspan-idadditional_implementation_notesspanspan-idadditional_implementation_notesspanadditional-implementation-notes"></a><span id="Additional_Implementation_Notes"></span><span id="additional_implementation_notes"></span><span id="ADDITIONAL_IMPLEMENTATION_NOTES"></span>其他实现注释

-   对于主要设备对象，只调用 [*HwVidInitialize*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_initialize)一次。 所有辅助设备对象都必须在此调用中进行初始化。

-   对于将 *bEnable* 设置为 **FALSE** 的 [**DrvAssertMode**](/windows/win32/api/winddi/nf-winddi-drvassertmode)调用，微型端口驱动程序应检查其他视图的状态。 它应避免关闭视频芯片，而其他视图仍处于活动状态。

-   永远不会假设绘图操作具有相同的绘图上下文 (例如，颜色深度和跨距) 。 这对于使用磁贴帧缓冲区的芯片尤其重要。

-   GDI 只能在内置设备上设置主视图。 某些系统（如便携式计算机）具有 (Lcd) 的内置监视设备，但也可以连接到外部监视器。 微型端口驱动程序应 \_ \_ 在调用 [**VIDEOPORTCREATESECONDARYDISPLAY**](/windows-hardware/drivers/ddi/video/nf-video-videoportcreatesecondarydisplay)时传递视频双屏可移动标志，以将其标记为可移动。

-   在双屏模式下的便携式计算机上，应禁用热键开关。 在启用了 ACPI 的视频系统上，微型端口驱动程序应拒绝 [**IOCTL \_ 视频 \_ 验证 \_ 子 \_ 状态 \_ 配置**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_validate_child_state_configuration) 请求。

-   对于支持 multichild 设备的便携式计算机，微型端口驱动程序应处理 [**IOCTL \_ 视频 \_ 获取 \_ 子 \_ 状态**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_get_child_state) 请求并返回逻辑子关系 (在) 的以下部分中进行了讨论。

 

