---
title: AGP 的视频端口驱动程序支持
description: AGP 的视频端口驱动程序支持
keywords:
- 视频微型端口驱动程序 WDK Windows 2000，AGP
- AGP WDK 视频微型端口
- 内存 WDK 视频微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a3f2a21141d2cf30994930e90bcf345f22707fc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816297"
---
# <a name="video-port-driver-support-for-agp"></a>AGP 的视频端口驱动程序支持


## <span id="ddk_video_port_driver_support_for_agp_gg"></span><span id="DDK_VIDEO_PORT_DRIVER_SUPPORT_FOR_AGP_GG"></span>


视频端口驱动程序实现以下功能，以支持 (AGP) 的加速图形端口。

[**AgpReservePhysical**](/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_reserve_physical)

[**AgpCommitPhysical**](/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_commit_physical)

[**AgpReserveVirtual**](/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_reserve_virtual)

[**AgpCommitVirtual**](/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_commit_virtual)

[**AgpFreeVirtual**](/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_free_virtual)

[**AgpReleaseVirtual**](/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_release_virtual)

[**AgpFreePhysical**](/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_free_physical)

[**AgpReleasePhysical**](/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_release_physical)

[**AgpSetRate**](/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_set_rate)

在视频微型端口驱动程序调用前面列表中的函数之前，它必须通过调用 [**VideoPortQueryServices**](/windows-hardware/drivers/ddi/video/nf-video-videoportqueryservices)获取函数指针。 有关获得 AGP 函数的指针的详细信息，请参阅 [由视频端口驱动程序实现的 Agp 函数](/windows-hardware/drivers/ddi/videoagp/)。

视频微型端口驱动程序执行以下步骤，以便预留和提交显示适配器可用于访问系统内存的 AGP 口径的一部分：

1.  调用 [**AgpReservePhysical**](/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_reserve_physical) 可以在 AGP 口径中保留一系列连续的物理地址。

2.  调用 [**AgpCommitPhysical**](/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_commit_physical) ，将由 *AgpReservePhysical* 返回的地址范围的一部分 (或全部) 映射到系统内存中的页面。 系统内存中的页面被锁定，但不一定是连续的。 视频微型端口驱动程序可以多次调用 *AgpCommitPhysical* ，以执行几项小型承诺，而不是一小部分。 但是，驱动程序不能尝试提交已提交的范围。

然后，若要使应用程序能够在系统内存中查看和使用已提交的页面，视频微型端口驱动程序将执行以下步骤：

1.  调用 [**AgpReserveVirtual**](/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_reserve_virtual) ，以在应用程序的地址空间中保留一系列虚拟地址。 视频微型端口驱动程序必须将 *AgpReserveVirtual* 传递给 *AgpReservePhysical* 之前返回的句柄，以便保留的虚拟地址范围可与 *AgpReservePhysical* 创建的物理地址范围相关联。

2.  调用 [**AgpCommitVirtual**](/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_commit_virtual) ，将 *AgpReserveVirtual* 返回的部分虚拟地址范围映射到系统内存中的页面。 *AgpCommitVirtual* 映射的页面之前必须通过调用 *AgpCommitPhysical* 进行映射。 此外，由 *AgpCommitPhysical* 建立的映射仍必须是最新的;也就是说，不能通过调用 [**AgpFreePhysical**](/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_free_physical)释放这些页。

**注意**   无论何时使用 AGP 函数提交或保留 (物理或虚拟) 的地址范围，该范围的大小必须是 64 kb 的倍数。

 

视频微型端口驱动程序负责释放并释放通过调用以下函数保留并提交的所有内存：

-   [**AgpFreeVirtual**](/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_free_virtual) messagebox 取消通过以前对 [**AgpCommitVirtual**](/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_commit_virtual)的调用映射到系统内存的虚拟地址。

-   [**AgpReleaseVirtual**](/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_release_virtual) 释放先前对 [**AgpReserveVirtual**](/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_reserve_virtual)的调用保留的虚拟地址。

-   [**AgpFreePhysical**](/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_free_physical) messagebox 取消通过以前对 [**AgpCommitPhysical**](/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_commit_physical)的调用映射到系统内存的物理地址。

-   [**AgpReleasePhysical**](/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_release_physical) 释放先前对 [**AgpReservePhysical**](/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_reserve_physical)的调用保留的物理地址。

 

