---
title: 存储类驱动程序 ReleaseQueue 例程
description: 存储类驱动程序 ReleaseQueue 例程
ms.assetid: 4d0f74f2-6c98-4de1-bc28-dfff3c01e319
keywords:
- ReleaseQueue
- 队列 WDK 存储
- 冻结队列 WDK 存储
- 已冻结的队列 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24c9f2be59fc652ae3e9b262b6a8bcc0f66eea0d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545236"
---
# <a name="storage-class-drivers-releasequeue-routine"></a>存储类驱动程序 ReleaseQueue 例程


## <span id="ddk_storage_class_drivers_releasequeue_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_RELEASEQUEUE_ROUTINE_KG"></span>


除非存储类驱动程序 ORs **SrbFlags**针对给定请求与 SRB\_标志\_否\_队列\_冻结，系统端口驱动程序为一个给定逻辑单元后冻结队列以下任何：

-   逻辑单元已执行请求时发生总线重置。

-   逻辑单元返回 SCSISTAT\_检查\_条件或 SCSISTAT\_命令\_已终止，类驱动程序可以找到在 SRB **ScsiStatus**成员。

-   请求已超时。

-   请求已终止的总线邮件命令如 SCSIMESS\_中止。

端口驱动程序指示特定于 LU 的队列已被冻结通过返回的请求 SRB\_状态\_队列\_冻结在**SrbStatus**成员。 从类驱动程序的新请求可以插入到队列，但是仅自动感知请求发送到逻辑单元，只要其队列已被冻结。

冻结在这些情况下的队列使每个存储类驱动程序有机会执行其他已排队的作业之前分析错误。 例如，已排队的作业可能需要取消如果媒体已更改。 若要刷新的队列，驱动程序可以发送的请求**SrbFlags**或运算使用 SRB\_标志\_绕过\_冻结\_队列。

一个*ReleaseQueue*例程分配并设置 IRP 和 SRB 以发布或刷新冻结的队列。 **函数**SRB 成员必须设置为 SRB\_函数\_发行\_队列或 SRB\_函数\_刷新\_队列中，这两个版本冻结的队列并取消所有当前排队的请求的目标逻辑单元。 端口驱动程序完成刷新队列中的所有请求其**SrbStatus**成员设置为 SRB\_状态\_请求\_刷新。

未能解除冻结的队列可让设备不可访问，因此驱动程序的*ReleaseQueue*例程应设计为可成功甚至在内存不足的情况。 一个*ReleaseQueue*例程应首先尝试通过调用为 SRB 分配内存[ **ExAllocatePool** ](https://msdn.microsoft.com/library/windows/hardware/ff544501)与**非分页池**内存类型，然后该分配失败时，如果使用已预先分配驱动程序初始化期间 SRB。 如果该驱动程序分配用于保留时保存初始化其设备扩展，如中所述 SRB[设置了存储类驱动程序的设备扩展](setting-up-a-storage-class-driver-s-device-extension.md)，将其*ReleaseQueue*如果可以使用该 SRB在多个并发发布操作可能需要的情况下，内存池较低，用适当的同步机制。

请注意，类驱动程序*ReleaseQueue*以异步方式调用例程通常从其*IoCompletion*例程。 类驱动程序*IoCompletion*不能调用例程*ReleaseQueue*刷新是否未被冻结的队列。 但是，它可以调用*ReleaseQueue*释放未冻结的队列和端口驱动程序只需将忽略此类请求。

 

 




