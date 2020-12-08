---
title: PnP 驱动程序的 Unload 例程
description: PnP 驱动程序的 Unload 例程
keywords:
- 卸载例程 WDK 内核，PnP 驱动程序
- PnP 卸载例程 WDK 内核
- 即插即用卸载例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37d2755b36f09c32930691397b8557e0470ad06a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837997"
---
# <a name="pnp-drivers-unload-routine"></a>PnP 驱动程序的 Unload 例程





PnP 驱动程序必须具有 [*卸载*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload) 例程，该例程会删除由 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程创建的任何特定于驱动程序的资源，例如内存、线程和事件。 如果没有要删除的特定于驱动程序的资源，驱动程序仍然必须具有 *卸载* 例程，但它可以只返回。

删除所有驱动程序的设备后，可以随时调用驱动程序的 *Unload* 例程。 PnP 管理器在系统线程的上下文中以 IRQL = 被动级别调用驱动程序的 *卸载* 例程 \_ 。

PnP 驱动程序可免费用于特定于设备的资源和设备对象，以响应 PnP 设备-删除 Irp。 PnP 管理器代表其枚举的每个 PnP 设备发送这些 Irp，以及使用 [**IoReportDetectedDevice**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioreportdetecteddevice)的驱动程序报告的任何根枚举的旧式设备。

因此，PnP 驱动程序的 *卸载* 例程通常是简单的，通常只包含一个 **返回** 语句。 但是，如果驱动程序在其 **DriverEntry** 例程中分配了任何驱动程序范围的资源，则必须在其 *卸载* 例程中解除分配这些资源，除非它已执行此操作。 通常，卸载 PnP 驱动程序的过程是同步操作。

I/o 管理器使用 [**IoAllocateDriverObjectExtension**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatedriverobjectextension)释放驱动程序对象和任何驱动程序对象扩展。

 

