---
title: 存储类驱动程序的 ReleaseQueue 例程
description: 存储类驱动程序的 ReleaseQueue 例程
keywords:
- ReleaseQueue
- 队列 WDK 存储
- 冻结队列 WDK 存储
- 冻结队列 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb244a235e0a6acacc115a4173e2430cc237c128
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839979"
---
# <a name="storage-class-drivers-releasequeue-routine"></a>存储类驱动程序的 ReleaseQueue 例程


## <span id="ddk_storage_class_drivers_releasequeue_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_RELEASEQUEUE_ROUTINE_KG"></span>


除非存储类驱动程序 Or 具有 **SrbFlags** SRB 标志的给定请求的 SrbFlags \_ \_ ，否则 \_ \_ ，系统端口驱动程序将在以下任何一项后冻结给定逻辑单元的队列：

-   逻辑单元执行请求时发生总线重置。

-   逻辑单元返回了 SCSISTAT \_ 检查 \_ 条件或 SCSISTAT \_ 命令 \_ 终止，该类驱动程序可在 SRB 的 **ScsiStatus** 成员中找到该命令。

-   请求已超时。

-   请求已由总线消息命令终止，如 SCSIMESS \_ 中止。

端口驱动程序通过返回 \_ \_ \_ 在 **SrbStatus** 成员中已冻结 SRB 状态队列的请求，指示 LU 特定的队列已冻结。 可以将来自类驱动程序的新请求插入到队列中，但只要其队列已冻结，就只会将自动感知请求发送到逻辑单元。

在这些情况下冻结队列使每个存储类驱动程序在执行其他排队作业之前有机会分析错误。 例如，如果媒体发生了更改，则可能需要取消排队作业。 若要刷新队列，驱动程序可以使用 **SrbFlags** 运算发送请求，并使用 SRB \_ 标志 \_ 绕过 \_ 冻结 \_ 队列。

*ReleaseQueue* 例程分配并设置 IRP，并设置 SRB 以释放或刷新冻结队列。 SRB 的 **函数** 成员必须设置为 SRB \_ 函数 \_ RELEASE \_ queue 或 SRB \_ 函数 \_ FLUSH \_ queue，这两个队列都释放冻结队列并取消目标逻辑单元的所有当前排队的请求。 端口驱动程序完成刷新队列中的所有请求，并将其 **SrbStatus** 成员设置为刷新的 SRB \_ 状态 \_ 请求 \_ 。

无法释放冻结队列会使设备不可访问，因此，驱动程序的 *ReleaseQueue* 例程应设计为即使在内存不足的情况下也能成功。 *ReleaseQueue* 例程应该首先尝试为 SRB 分配内存，方法是将 [**ExAllocatePool**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepool)与 **非分页池** 内存类型一起调用，如果该分配失败，则使用驱动程序初始化期间预分配的 SRB。 如果驱动程序在初始化其设备扩展时分配了 SRB 以保留保留，如 [设置存储类驱动程序的设备扩展](setting-up-a-storage-class-driver-s-device-extension.md)中所述，在使用适当的同步机制时，它的 *ReleaseQueue* 可以使用该 SRB，这种情况下，可能需要多个并发发布操作。

请注意，类驱动程序的 *ReleaseQueue* 例程通常是从其 *IoCompletion* 例程异步调用的。 类驱动程序的 *IoCompletion* 例程无法调用 *ReleaseQueue* 来刷新未冻结的队列。 但是，它可以调用 *ReleaseQueue* 来释放未冻结的队列，而端口驱动程序只是忽略此类请求。

 

