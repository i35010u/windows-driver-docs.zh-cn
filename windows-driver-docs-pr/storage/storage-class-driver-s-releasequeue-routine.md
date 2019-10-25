---
title: 存储类驱动程序的 ReleaseQueue 例程
description: 存储类驱动程序的 ReleaseQueue 例程
ms.assetid: 4d0f74f2-6c98-4de1-bc28-dfff3c01e319
keywords:
- ReleaseQueue
- 队列 WDK 存储
- 冻结队列 WDK 存储
- 冻结队列 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78ecd9c93fef7e85afb649fa6f1c346e0ed4bd79
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845630"
---
# <a name="storage-class-drivers-releasequeue-routine"></a>存储类驱动程序的 ReleaseQueue 例程


## <span id="ddk_storage_class_drivers_releasequeue_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_RELEASEQUEUE_ROUTINE_KG"></span>


除非存储类驱动程序使用 SRB\_标志为给定请求 Or **SrbFlags** ，否则\_不\_队列\_冻结，系统端口驱动程序会在以下任何一项后冻结给定逻辑单元的队列：:

-   逻辑单元执行请求时发生总线重置。

-   逻辑单元返回了 SCSISTAT\_检查\_条件或 SCSISTAT\_命令\_终止，该类驱动程序可以在 SRB 的**ScsiStatus**成员中找到该命令。

-   请求已超时。

-   请求已由总线消息命令终止，如 SCSIMESS\_ABORT。

端口驱动程序通过在**SrbStatus**成员中返回具有 SRB\_状态\_QUEUE\_冻结的请求来指示 LU 特定的队列已冻结。 可以将来自类驱动程序的新请求插入到队列中，但只要其队列已冻结，就只会将自动感知请求发送到逻辑单元。

在这些情况下冻结队列使每个存储类驱动程序在执行其他排队作业之前有机会分析错误。 例如，如果媒体发生了更改，则可能需要取消排队作业。 若要刷新队列，驱动程序可以使用**SrbFlags**运算和 SRB\_标志发送请求，\_绕过\_冻结\_队列。

*ReleaseQueue*例程分配并设置 IRP，并设置 SRB 以释放或刷新冻结队列。 SRB 的**函数**成员必须设置为 SRB\_函数\_RELEASE\_QUEUE 或 SRB\_函数\_FLUSH\_queue，这两个队列都释放冻结队列并取消目标的所有当前排队的请求逻辑单元。 端口驱动程序完成刷新队列中的所有请求，并将其**SrbStatus**成员设置为 SRB\_状态\_请求\_刷新。

无法释放冻结队列会使设备不可访问，因此，驱动程序的*ReleaseQueue*例程应设计为即使在内存不足的情况下也能成功。 *ReleaseQueue*例程应该首先尝试为 SRB 分配内存，方法是将[**ExAllocatePool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepool)与**非分页池**内存类型一起调用，如果该分配失败，则使用驱动程序初始化期间预分配的 SRB。 如在设置存储类驱动程序的设备扩展时，如果驱动程序分配了 SRB 以保留保留，则在[设置存储类驱动程序的设备扩展](setting-up-a-storage-class-driver-s-device-extension.md)时，它的*ReleaseQueue*可以使用该 SRB，并将适当的可能需要多个并发发布操作时的同步机制。

请注意，类驱动程序的*ReleaseQueue*例程通常是从其*IoCompletion*例程异步调用的。 类驱动程序的*IoCompletion*例程无法调用*ReleaseQueue*来刷新未冻结的队列。 但是，它可以调用*ReleaseQueue*来释放未冻结的队列，而端口驱动程序只是忽略此类请求。

 

 




