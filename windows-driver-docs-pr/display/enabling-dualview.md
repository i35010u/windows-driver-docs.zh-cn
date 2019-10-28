---
title: 启用 DualView
description: 启用 DualView
ms.assetid: 7779c74d-2076-419d-94e4-07c36501524e
keywords:
- 双屏显示 WDK 视频微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7192a93d4a366a69ad350cf14eee0d3b81ea1652
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838958"
---
# <a name="enabling-dualview"></a>启用 DualView


## <span id="ddk_enabling_dualview_gg"></span><span id="DDK_ENABLING_DUALVIEW_GG"></span>


对于最小的双屏实现，请执行以下操作：

-   在微型端口驱动程序的[*HwVidFindAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_find_adapter)返回之前，调用新的视频端口驱动程序入口点[**VideoPortCreateSecondaryDisplay**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportcreatesecondarydisplay)，为辅助视图生成设备扩展。 在 "辅助设备扩展" 中，添加两个新的私有成员：

    1.  一个标志，用于指示设备扩展适用于辅助显示器
    2.  一个指针，其中包含主显示器的设备扩展的地址
-   必须在微型端口驱动程序的[*HwVidStartIO*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_start_io)回调例程中进行四项更改，修改它响应显示的四个 IOCTL 请求的方式。 以下列表中的第四项提供了两种方法来实现相同的结果。

    1.  为了响应[**IOCTL\_视频\_MAP\_视频\_内存**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_map_video_memory)请求，应正确设置每个视图的帧缓冲区指针和长度。
    2.  应将对[**IOCTL\_视频的响应\_集\_当前\_模式请求设置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_set_current_mode)为特定于辅助视图。
    3.  对[**IOCTL\_视频的响应\_重置\_设备**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_reset_device)请求取决于设备是主显示器还是辅助显示器。 如果设备是主显示器，则执行任何所需的操作。 但是，如果设备为辅助显示器，则建议不要执行任何操作。
    4.  更改对[**IOCTL\_视频的响应\_共享\_视频\_内存**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_share_video_memory)请求，以获取两个视图的正确映射。 请注意，对于 DirectDraw 实现，可以修改 DirectDraw 函数[*DdMapMemory*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mapmemory)以获取两个视图的正确映射。
-   显示驱动程序应负责逻辑帧缓冲区地址和物理视频内存偏移量之间的调整。 这对于 DirectDraw 实现尤其重要，因为在双屏显示中，主表面可能会从内存位置0以外的任何位置启动。 显示驱动程序应通过在处理[**vmiData**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgetdirectdrawinfo)时使用相应的视频内存偏移量填充 **&gt;pHalInfo vmiData PvPrimary**和 **&gt;pHalInfo FpPrimary DrvGetDirectDrawInfo** ，来通知 DirectDraw。

### <a name="span-idadditional_implementation_notesspanspan-idadditional_implementation_notesspanspan-idadditional_implementation_notesspanadditional-implementation-notes"></a><span id="Additional_Implementation_Notes"></span><span id="additional_implementation_notes"></span><span id="ADDITIONAL_IMPLEMENTATION_NOTES"></span>其他实现注释

-   对于主要设备对象，只调用[*HwVidInitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_initialize)一次。 所有辅助设备对象都必须在此调用中进行初始化。

-   对于将*bEnable*设置为**FALSE**的[**DrvAssertMode**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvassertmode)调用，微型端口驱动程序应检查其他视图的状态。 它应避免关闭视频芯片，而其他视图仍处于活动状态。

-   永远不会假设绘图操作具有相同的绘图上下文（例如，色深度和跨距）。 这对于使用磁贴帧缓冲区的芯片尤其重要。

-   GDI 只能在内置设备上设置主视图。 某些系统（如便携式计算机）有内置的监视设备（Lcd），但也可以连接到外部监视器。 微型端口驱动程序应将视图标记为可移动，方法是在调用[**VideoPortCreateSecondaryDisplay**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportcreatesecondarydisplay)时将视频传递\_双屏\_可移动标志。

-   在双屏模式下的便携式计算机上，应禁用热键开关。 在启用了 ACPI 的视频系统上，微型端口驱动程序应拒绝[**IOCTL\_视频\_验证\_子\_状态\_配置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_validate_child_state_configuration)请求。

-   对于支持 multichild 设备的便携式计算机，微型端口驱动程序应处理[**IOCTL\_视频\_获取\_子\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_get_child_state)请求并返回逻辑子关系（在下一节中讨论）。

 

 





