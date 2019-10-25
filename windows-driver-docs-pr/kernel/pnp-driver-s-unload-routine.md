---
title: PnP 驱动程序的 Unload 例程
description: PnP 驱动程序的 Unload 例程
ms.assetid: 71b30a84-d3c7-4674-94a6-b99f83567183
keywords:
- 卸载例程 WDK 内核，PnP 驱动程序
- PnP 卸载例程 WDK 内核
- 即插即用卸载例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf0c226fdd2d78a10d9c4bb4bdcd68d58d71ffd9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827697"
---
# <a name="pnp-drivers-unload-routine"></a>PnP 驱动程序的 Unload 例程





PnP 驱动程序必须具有[*卸载*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)例程，该例程会删除由[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程创建的任何特定于驱动程序的资源，例如内存、线程和事件。 如果没有要删除的特定于驱动程序的资源，驱动程序仍然必须具有*卸载*例程，但它可以只返回。

删除所有驱动程序的设备后，可以随时调用驱动程序的*Unload*例程。 PnP 管理器在系统线程的上下文中调用驱动程序的*卸载*例程，该例程的范围为 IRQL = 被动\_级别。

PnP 驱动程序可免费用于特定于设备的资源和设备对象，以响应 PnP 设备-删除 Irp。 PnP 管理器代表其枚举的每个 PnP 设备发送这些 Irp，以及使用[**IoReportDetectedDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioreportdetecteddevice)的驱动程序报告的任何根枚举的旧式设备。

因此，PnP 驱动程序的*卸载*例程通常是简单的，通常只包含一个**返回**语句。 但是，如果驱动程序在其**DriverEntry**例程中分配了任何驱动程序范围的资源，则必须在其*卸载*例程中解除分配这些资源，除非它已执行此操作。 通常，卸载 PnP 驱动程序的过程是同步操作。

I/o 管理器使用[**IoAllocateDriverObjectExtension**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatedriverobjectextension)释放驱动程序对象和任何驱动程序对象扩展。

 

 




