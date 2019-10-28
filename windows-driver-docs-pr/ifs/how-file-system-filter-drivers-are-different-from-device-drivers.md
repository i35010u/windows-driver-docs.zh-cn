---
title: 文件系统筛选器驱动程序与设备驱动程序的差异在哪里
description: 文件系统筛选器驱动程序与设备驱动程序的差异在哪里
ms.assetid: 64a59564-a4d7-4174-82d3-60bd1a30b2d8
keywords:
- 筛选器驱动程序 WDK 文件系统和设备驱动程序
- 文件系统筛选器驱动程序（WDK）和设备驱动程序
- 设备驱动程序 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be82c51832c5ff1a7eef2a0f00378030d560c608
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841218"
---
# <a name="how-file-system-filter-drivers-are-different-from-device-drivers"></a>文件系统筛选器驱动程序与设备驱动程序的差异在哪里


## <span id="ddk_how_file_system_filter_drivers_are_different_from_device_drivers_i"></span><span id="DDK_HOW_FILE_SYSTEM_FILTER_DRIVERS_ARE_DIFFERENT_FROM_DEVICE_DRIVERS_I"></span>


以下小节介绍了文件系统筛选器驱动程序和设备驱动程序之间的一些差异。

### <a name="span-idno_power_managementspanspan-idno_power_managementspanspan-idno_power_managementspanno-power-management"></a><span id="No_Power_Management"></span><span id="no_power_management"></span><span id="NO_POWER_MANAGEMENT"></span>无电源管理

由于文件系统筛选器驱动程序不是设备驱动程序，因此不会直接控制硬件设备，它们不会接收[**IRP\_MJ\_电源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)请求。 相反，电源 Irp 会直接发送到存储设备堆栈。 但在极少数情况下，文件系统筛选器驱动程序可能会干扰电源管理。 出于此原因，文件系统筛选器驱动程序不应为 IRP\_MJ 注册调度例程，\_**DriverEntry**例程中的 POWER，并且它们不应调用[PoXxx](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)例程。

### <a name="span-idno_wdmspanspan-idno_wdmspanspan-idno_wdmspanno-wdm"></a><span id="No_WDM"></span><span id="no_wdm"></span><span id="NO_WDM"></span>无 WDM

文件系统筛选器驱动程序不能 Windows 驱动模型（WDM）驱动程序。 Microsoft [Windows 驱动模型](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model)仅适用于设备驱动程序。 有关 Windows Me、Windows 98 和 Windows 95 中的文件系统驱动程序开发的详细信息，请参阅 Windows Me 驱动程序开发工具包（DDK）。

### <a name="span-idno_adddevice_or_startiospanspan-idno_adddevice_or_startiospanspan-idno_adddevice_or_startiospanno-adddevice-or-startio"></a><span id="No_AddDevice_or_StartIo"></span><span id="no_adddevice_or_startio"></span><span id="NO_ADDDEVICE_OR_STARTIO"></span>无 AddDevice 或 StartIo

由于文件系统筛选器驱动程序不是设备驱动程序，因此不会直接控制硬件设备，它们不应具有[**AddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)或[**StartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)例程。

### <a name="span-iddifferent_device_objects_createdspanspan-iddifferent_device_objects_createdspanspan-iddifferent_device_objects_createdspandifferent-device-objects-created"></a><span id="Different_Device_Objects_Created"></span><span id="different_device_objects_created"></span><span id="DIFFERENT_DEVICE_OBJECTS_CREATED"></span>已创建不同的设备对象

尽管文件系统筛选器驱动程序和设备驱动程序都创建设备对象，但它们在创建的设备对象的数量和种类上有所不同。

设备驱动程序创建物理和功能设备对象来表示设备。 即插即用（PnP）管理器构建并维护一个全局设备树，其中包含设备驱动程序创建的所有设备对象。 文件系统筛选器驱动程序创建的设备对象不包含在此设备树中。

文件系统筛选器驱动程序不创建物理或功能设备对象。 而是创建控制设备对象并筛选设备对象。 *控制设备对象*表示系统和用户模式应用程序的筛选器驱动程序。 *筛选器设备对象*执行筛选特定文件系统或卷的实际工作。 文件系统筛选器驱动程序通常会创建一个控制设备对象和一个或多个筛选器设备对象。

### <a name="span-idother_differencesspanspan-idother_differencesspanspan-idother_differencesspanother-differences"></a><span id="Other_Differences"></span><span id="other_differences"></span><span id="OTHER_DIFFERENCES"></span>其他差异

因为文件系统筛选器驱动程序不是设备驱动程序，所以它们不执行[直接内存访问（DMA）](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-direct-i-o-with-dma)。

不同于设备筛选器驱动程序（可附加在目标设备的功能驱动程序之上或之下），文件系统筛选器驱动程序只能附加在目标文件系统驱动程序之上。 因此，在设备驱动程序条款中，文件系统筛选器驱动程序只能是上限筛选器，而不能是较低的筛选器。

 

 




