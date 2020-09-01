---
title: ERESOURCE 例程简介
description: ERESOURCE 例程简介
ms.assetid: 5c7759db-aeb5-47f3-8adc-ddedb74b5cb4
keywords:
- ERESOURCE 结构
- 专用等待进程 WDK 内核
- 共享等待进程 WDK 内核
- 排除或共享同步 WDK 内核
- 同步 WDK 内核，专用/共享
- 等待进程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bbcc530648c108d4353be53e08b94076272c255f
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188867"
---
# <a name="introduction-to-eresource-routines"></a>ERESOURCE 例程简介





系统提供了用于获取和释放 ERESOURCE 结构以及检查其当前状态的例程。

### <a name="acquiring-and-releasing-an-eresource-structure"></a>获取和释放 ERESOURCE 结构

驱动程序可以使用 ERESOURCE 结构来实现 *独占/共享同步*。 异或 shared 同步的工作原理如下所示：

-   任意数量的线程都可以获取共享的 ERESOURCE。

-   只有一个线程可以专门获取 ERESOURCE。 仅当没有线程获取共享的线程时，才能独占获取 ERESOURCE。

当前无法获取 ERESOURCE 的线程可以选择置于等待状态，直到可以获取 ERESOURCE。 系统维护两个等待 ERESOURCE 的线程列表：一个 *独占等待进程* 列表和一个 *共享等待进程*列表。

专用或共享同步的典型用途是实现读/写锁定。 读/写锁允许多个线程执行读取操作，但是一次只能写入一个线程。 这可以直接在获取 ERESOURCE 时实现。

驱动程序为 ERESOURCE 分配存储并使用 [**ExInitializeResourceLite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializeresourcelite)对其进行初始化。 系统维护所有正在使用的 ERESOURCE 结构的列表。 当驱动程序不再需要特定的 ERESOURCE 时，它必须调用 [**ExDeleteResourceLite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeleteresourcelite) 将其从系统列表中删除。 驱动程序还可以通过调用 [**ExReinitializeResourceLite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exreinitializeresourcelite)重复使用 ERESOURCE。

驱动程序可以对 ERESOURCE 执行以下基本操作：

-   获取与 [**ExAcquireResourceSharedLite**](/previous-versions/ff544363(v=vs.85))共享的 ERESOURCE。 仅当资源尚未独占获取并且没有独占等待进程时，此例程才获取资源。

-   以独占方式获取使用 [**ExAcquireResourceExclusiveLite**](/previous-versions/ff544351(v=vs.85))的 ERESOURCE。 只要资源未以独占方式获取或为共享，此例程就会获取资源。

-   使用 [**ExConvertExclusiveToSharedLite**](/previous-versions/ff544558(v=vs.85))将专用购置转换为共享购置。

-   使用 [**ExReleaseResourceLite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exreleaseresourcelite)发布获取的资源。

[**ExAcquireResourceSharedLite**](/previous-versions/ff544363(v=vs.85))和[**ExAcquireResourceExclusiveLite**](/previous-versions/ff544351(v=vs.85))的*Wait*参数确定当前线程是否等待获取 ERESOURCE。 如果指定的值为 **false** ，并且无法获取 ERESOURCE，则例程将返回 **false**。 如果指定的值为 **TRUE**，则当前线程将放在 ERESOURCE 的相应等待列表中。

### <a name="examining-the-state-of-an-eresource-structure"></a>检查 ERESOURCE 结构的状态

驱动程序还可以确定 ERESOURCE 的当前状态，如下所示：

-   使用 [**ExIsResourceAcquiredLite**](/previous-versions/windows/hardware/drivers/ff545466(v=vs.85)) 或 [**ExIsResourceAcquiredSharedLite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredsharedlite) 来确定是否已将 ERESOURCE 作为共享或独占方式获取。 使用 [**ExIsResourceAcquiredExclusiveLite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredexclusivelite) 检查是否专门获取了 ERESOURCE。

-   使用 [**ExGetSharedWaiterCount**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exgetsharedwaitercount) 确定 ERESOURCE 的共享等待进程的数目，并使用 [**EXGETEXCLUSIVEWAITERCOUNT**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exgetexclusivewaitercount) 来确定等待进程的独占 ERESOURCE 数。

 

