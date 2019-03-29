---
title: DriverEntry 的可选责任
description: DriverEntry 的可选责任
ms.assetid: 859282f7-6b40-47a8-b845-cdb7c26585dd
keywords:
- DriverEntry WDK 内核，可选的职责
- 声明的硬件资源
- executive 辅助线程 WDK 内核
- 辅助角色线程 WDK 内核
- 系统空间内存分配 WDK 内核
- 系统资源存储 WDK 内核
- 存储系统资源
- 硬件资源申报 WDK 内核
- 资源申报 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 468c0144e45f6ee1688e0b231867528615f2d2f6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575528"
---
# <a name="driverentrys-optional-responsibilities"></a>DriverEntry 的可选责任





具体取决于在分层驱动程序，基础设备的性质和驱动程序，设计一个链中的特定驱动程序的位置[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程还可以负责以下：

-   调用[ **IoAllocateDriverObjectExtension** ](https://msdn.microsoft.com/library/windows/hardware/ff548233)来创建和初始化对象扩展名为驱动程序，如果驱动程序需要存储在驱动程序范围的基础上的数据。 驱动程序对象扩展是特定于驱动程序的数据结构。 例如，驱动程序可能会使用其驱动程序对象扩展将存储注册表路径，或者其他全局信息。

-   调用[ **PsCreateSystemThread** ](https://msdn.microsoft.com/library/windows/hardware/ff559932)创建 executive 工作线程，如果驱动程序 （如文件系统驱动程序） 使用此类线程的最高级别的驱动程序。 在这种情况下，该驱动程序还必须具有类型工作线程的回调例程\_线程\_例程，采用单个输入 PVOID*参数*。

-   注册[*重新初始化*](https://msdn.microsoft.com/library/windows/hardware/ff561022)例程。 (请参阅[写入的重新初始化例程](writing-a-reinitialize-routine.md)。)

-   处理与讨论，如那些使用端口或类的驱动程序协同工作的特定于设备的微型端口或 miniclass 驱动程序可能具有不同的特定于类的初始化需求。 请参阅设备类型特定文档的详细信息中 Windows Driver Kit (WDK)。

### <a name="providing-storage-for-system-resources"></a>提供用于系统资源存储空间

应在分配每个设备对象[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)例程或调度例程中用于处理即插即用[ **IRP\_MN\_开始\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551749)请求时，不能在**DriverEntry**。

但是，驱动程序可能需要为其他驱动程序范围内使用分配额外的系统空间内存。 如果是这样， **DriverEntry**例程可以调用一个 （或多个） 下面的例程：

-   **IoAllocateDriverObjectExtension**，若要创建与驱动程序对象相关联的上下文区域

-   [**ExAllocatePoolWithTag** ](https://msdn.microsoft.com/library/windows/hardware/ff544520)分页或非分页系统空间内存

-   [**MmAllocateNonCachedMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff554479)或[ **MmAllocateContiguousMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff554460)缓存对齐非分页的系统的空间内存 （用于 I/O 缓冲区）

每个**DriverEntry**例程在 IRQL 在系统线程的上下文中运行 = 被动\_级别。 因此，与分配任何内存**ExAllocatePoolWithTag**在初始化过程中以独占方式使用可以是从页面缓冲池，只要该驱动程序不会控制保存系统页面文件的设备。 必须具有释放已分配的内存[ **ExFreePool** ](https://msdn.microsoft.com/library/windows/hardware/ff544590)之前**DriverEntry**返回控件。 但是，该设置的驱动程序*重新初始化*例程可以将指针传递到此内存时它将调用[ **IoRegisterDriverReinitialization**](https://msdn.microsoft.com/library/windows/hardware/ff549511)，从而使驱动程序*重新初始化*负责释放的内存分配例程。

### <a href="" id="claiming-hardware-resources-"></a>声明的硬件资源

较旧的、 非 PnP 驱动程序声明注册表中的资源。 即插即用驱动程序，但是，既不声明从设备资源也不直接向注册表写入资源要求。 相反，这些驱动程序报告要求以响应某些 PnP Irp，即插即用管理器的枚举过程的一部分。 即插即用驱动程序收到其已分配的资源中 PnP **IRP\_MN\_启动\_设备**请求。

不直接与即插即用的管理器中，某些微型端口驱动程序，如交互的驱动程序可能具有不同的报表要求规定 does 与 PnP 管理器进行交互的类或端口驱动程序。 此类要求是特定于设备类。 有关特定于设备的和特定于类的详细信息，请参阅相关设备类 Windows Driver Kit (WDK) 中的文档。

### <a name="using-the-registry"></a>使用注册表

一个**DriverEntry**例程可以使用注册表以获取所需的信息，以便初始化的驱动程序，或它的其他驱动程序在注册表中设置的信息或受保护的子系统来使用。 信息的性质取决于设备的类型。 驱动程序可以访问注册表使用**Zw * Xxx*** 和**Rtl * Xxx*** 例程。 **DriverEntry**例程的*RegistryPath*参数指向一个计数的 Unicode 字符串，指定驱动程序的注册表项的路径<strong>\\注册表\\机\\系统\\CurrentControlSet\\Services\\* DriverName</strong><em>。由于指针不再有效之后，该例程应保存一份的字符串指针本身，**DriverEntry</em>* 返回。

 

 




