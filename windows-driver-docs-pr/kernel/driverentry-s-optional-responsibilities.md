---
title: DriverEntry 的可选责任
description: DriverEntry 的可选责任
ms.assetid: 859282f7-6b40-47a8-b845-cdb7c26585dd
keywords:
- DriverEntry WDK 内核，可选责任
- 申报硬件资源
- executive 工作线程 WDK 内核
- 工作线程 WDK 内核
- 系统空间内存分配 WDK 内核
- 系统资源存储 WDK 内核
- 存储系统资源
- 声称 WDK 内核的硬件资源
- 资源申报 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14d9183bc620d54ca0de824a09be4e87d941a415
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838716"
---
# <a name="driverentrys-optional-responsibilities"></a>DriverEntry 的可选责任





根据分层驱动程序链中特定驱动程序的位置、基础设备的性质以及驱动程序的设计， [**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程还可以负责以下操作：

-   如果驱动程序需要对整个驱动程序的数据进行存储，则调用[**IoAllocateDriverObjectExtension**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatedriverobjectextension)来创建和初始化驱动程序对象扩展。 驱动程序对象扩展是特定于驱动程序的数据结构。 例如，驱动程序可能使用其驱动程序对象扩展来存储注册表路径或其他全局信息。

-   如果驱动程序是使用此类线程的最高级别的驱动程序（如文件系统驱动程序），则调用[**PsCreateSystemThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pscreatesystemthread)来创建 executive 工作线程。 在这种情况下，驱动程序还必须具有 WORKER\_线程\_例程的回调例程，该例程使用单个输入 PVOID*参数*。

-   注册重新[*初始化*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-driver_reinitialize)例程。 （请参阅[编写重新初始化例程](writing-a-reinitialize-routine.md)。）

-   处理特定于类的初始化要求，这些要求不同于本文所讨论的特定要求，例如，与端口或类驱动程序一起工作的特定于设备的微型端口或 miniclass 驱动程序可能具有。 有关详细信息，请参阅 Windows 驱动程序工具包（WDK）中的设备类型特定文档。

### <a name="providing-storage-for-system-resources"></a>为系统资源提供存储

每个设备对象应在[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程中分配，或在处理 PnP [**IRP\_MN\_START\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)请求而不是**DriverEntry**中的调度例程中分配。

但是，驱动程序可能需要为其他驱动程序范围的使用分配额外的系统空间内存。 如果是这样， **DriverEntry**例程可以调用以下一个或多个例程：

-   **IoAllocateDriverObjectExtension**，用于创建与驱动程序对象关联的上下文区域

-   分页或非分页的系统空间内存[**ExAllocatePoolWithTag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)

-   用于缓存对齐的非分页系统空间内存（用于 i/o 缓冲区）的[**MmAllocateNonCachedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmallocatenoncachedmemory)或[**MmAllocateContiguousMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousmemory)

每个**DriverEntry**例程在系统线程的上下文中运行，以 IRQL = 被动\_级别。 因此，只要该驱动程序不控制包含系统页面文件的设备，则在初始化期间使用**ExAllocatePoolWithTag**分配的任何内存都可以来自页面缓冲池。 在**DriverEntry**返回 control 之前，必须用[**ExFreePool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)释放已分配的内存。 但是，在调用[**IoRegisterDriverReinitialization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioregisterdriverreinitialization)时设置重新*初始化*例程的驱动程序可以将指针传递给此内存，从而使驱动程序的*初始化*例程负责释放内存分配。

### <a href="" id="claiming-hardware-resources-"></a>申报硬件资源

旧的非 PnP 驱动程序从注册表中声明资源。 另一方面，PnP 驱动程序不会从中声明设备资源，也不会直接向注册表写入资源要求。 相反，这些驱动程序会报告要求，以响应特定 PnP Irp，作为 PnP 管理器的枚举过程的一部分。 PnP 驱动程序在 PnP **IRP\_MN\_START\_设备**请求中接收已分配的资源。

与 pnp 管理器不直接交互的驱动程序（例如某些微型端口驱动程序）可能具有与 PnP 管理器进行交互的类或端口驱动程序的不同报告要求。 此类要求是特定于设备类的。 有关特定于设备的详细信息，请参阅 Windows 驱动程序工具包（WDK）中相关设备类的文档。

### <a name="using-the-registry"></a>使用注册表

**DriverEntry**例程可能使用注册表获取初始化驱动程序所需的某些信息，或者可能会在注册表中为其他驱动程序或受保护的子系统设置信息以供使用。 信息的性质取决于设备的类型。 驱动程序可以使用**Zw * xxx*** 和**Rtl * xxx*** 例程访问注册表。 **DriverEntry**例程的*RegistryPath*参数指向一个计数的 Unicode 字符串，该字符串指定驱动程序的注册表项的路径， <strong>\\注册表\\Machine\\System\\CurrentControlSet\\Services\\* DriverName</strong><em>。例程应保存字符串的副本，而不是保存指针本身，因为在 **DriverEntry</em>返回后指针不再有效*。

 

 




