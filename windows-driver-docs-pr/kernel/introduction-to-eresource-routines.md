---
title: ERESOURCE 例程简介
description: ERESOURCE 例程简介
ms.assetid: 5c7759db-aeb5-47f3-8adc-ddedb74b5cb4
keywords:
- ERESOURCE 结构
- 独占等待者 WDK 内核
- 共享的等待程序 WDK 内核
- 排他共享/同步 WDK 内核
- 同步 WDK 内核，排他/共享
- 等待程序 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 609800a2fee6db3c167f973a2c3d28b003a7d94c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369735"
---
# <a name="introduction-to-eresource-routines"></a>ERESOURCE 例程简介





系统提供的例程来获取和释放 ERESOURCE 结构并检查其当前状态。

### <a name="acquiring-and-releasing-an-eresource-structure"></a>获取和释放 ERESOURCE 结构

驱动程序可以使用 ERESOURCE 结构来实现*排他共享/同步*。 排他/共享同步的工作原理，如下所示：

-   任意数量的线程可以获取作为共享 ERESOURCE。

-   只有一个线程可以以独占方式获取 ERESOURCE。 以独占方式如果没有线程已获得为共享它，可以仅获取 ERESOURCE。

目前无法获取 ERESOURCE 的线程 （可选） 可以放处于等待状态，直到可以获取 ERESOURCE。 系统会维护两个列表的线程正在等待 ERESOURCE： 一系列*独占等待者*和一系列*共享等待者*。

排他/共享同步的典型用法是实现读/写锁。 读/写锁允许多个线程执行读取的操作，但只有一个线程可以编写一次。 这可以实现直接在获取 ERESOURCE 方面。

驱动程序为 ERESOURCE 分配存储并初始化与该[ **ExInitializeResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinitializeresourcelite)。 系统会维护所有 ERESOURCE 结构中使用的列表。 当驱动程序不再需要特定 ERESOURCE 时，它必须调用[ **ExDeleteResourceLite** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exdeleteresourcelite)要从系统的列表中删除。 该驱动程序还可以通过调用重用 ERESOURCE [ **ExReinitializeResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exreinitializeresourcelite)。

驱动程序可以执行 ERESOURCE 上的以下基本操作：

-   获取作为与共享 ERESOURCE [ **ExAcquireResourceSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544363)。 此例程仅当不以独占方式获取资源，且没有独占等待获取资源。

-   获取以独占方式使用 ERESOURCE [ **ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351)。 此例程将获取该资源，只要它尚未获取以独占方式或作为共享。

-   转换为具有共享获取的排他获取[ **ExConvertExclusiveToSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544558)。

-   发布一获取的资源，具有[ **ExReleaseResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exreleaseresourcelite)。

*等待*的参数[ **ExAcquireResourceSharedLite** ](https://msdn.microsoft.com/library/windows/hardware/ff544363)并[ **ExAcquireResourceExclusiveLite** ](https://msdn.microsoft.com/library/windows/hardware/ff544351)确定当前线程是否等待 ERESOURCE 来获取。 如果指定的值**FALSE**和 ERESOURCE 句柄，则例程将返回**FALSE**。 如果指定的值 **，则返回 TRUE**，则当前线程置于 ERESOURCE 为相应的等待列表。

### <a name="examining-the-state-of-an-eresource-structure"></a>检查 ERESOURCE 结构的状态

驱动程序还可以按如下所示确定 ERESOURCE 的当前状态：

-   使用[ **ExIsResourceAcquiredLite** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545466(v=vs.85))或[ **ExIsResourceAcquiredSharedLite** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exisresourceacquiredsharedlite)来确定 ERESOURCE 并且尚未获取为共享或排他。 使用[ **ExIsResourceAcquiredExclusiveLite** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exisresourceacquiredexclusivelite)来检查是否 ERESOURCE 已专门获取以独占方式。

-   使用[ **ExGetSharedWaiterCount** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exgetsharedwaitercount)若要确定共享 ERESOURCE，等待数，并使用[ **ExGetExclusiveWaiterCount** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exgetexclusivewaitercount)来确定的排他 ERESOURCE 等待数。

 

 




