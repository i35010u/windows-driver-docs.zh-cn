---
title: 文件系统筛选器驱动程序与设备驱动程序的差异在哪里
description: 文件系统筛选器驱动程序与设备驱动程序的差异在哪里
ms.assetid: 64a59564-a4d7-4174-82d3-60bd1a30b2d8
keywords:
- 筛选器驱动程序 WDK 文件系统，与设备驱动程序
- 文件系统筛选器驱动程序 WDK，与设备驱动程序
- 设备驱动程序 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8212824fced83564cab1400c9cd5c5aa0b82dee
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379072"
---
# <a name="how-file-system-filter-drivers-are-different-from-device-drivers"></a>文件系统筛选器驱动程序与设备驱动程序的差异在哪里


## <span id="ddk_how_file_system_filter_drivers_are_different_from_device_drivers_i"></span><span id="DDK_HOW_FILE_SYSTEM_FILTER_DRIVERS_ARE_DIFFERENT_FROM_DEVICE_DRIVERS_I"></span>


以下各小节介绍了一些文件系统筛选器驱动程序和设备驱动程序之间的差异。

### <a name="span-idnopowermanagementspanspan-idnopowermanagementspanspan-idnopowermanagementspanno-power-management"></a><span id="No_Power_Management"></span><span id="no_power_management"></span><span id="NO_POWER_MANAGEMENT"></span>无电源管理

由于文件系统筛选器驱动程序不是设备驱动程序，并且因此并不直接控制硬件设备，它们不接收[ **IRP\_MJ\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff550784)请求。 相反，power Irp 直接发送到存储设备堆栈。 在极少数情况下，但是，文件系统筛选器驱动程序可能会干扰电源管理。 出于此原因，文件系统筛选器驱动程序不应注册调度例程的 IRP\_MJ\_中的 POWER **DriverEntry**例程中，并且它们不应调用[PoXxx](https://msdn.microsoft.com/library/windows/hardware/ff559835)例程。

### <a name="span-idnowdmspanspan-idnowdmspanspan-idnowdmspanno-wdm"></a><span id="No_WDM"></span><span id="no_wdm"></span><span id="NO_WDM"></span>No WDM

文件系统筛选器驱动程序不能为 Windows 驱动程序模型 (WDM) 驱动程序。 在 Microsoft [Windows 驱动程序模型](https://msdn.microsoft.com/library/windows/hardware/ff565698)仅适用于设备驱动程序。 有关在 Windows Me、 Windows 98 和 Windows 95 文件系统驱动程序开发的详细信息，请参阅 Windows Me 驱动程序开发工具包 (DDK)。

### <a name="span-idnoadddeviceorstartiospanspan-idnoadddeviceorstartiospanspan-idnoadddeviceorstartiospanno-adddevice-or-startio"></a><span id="No_AddDevice_or_StartIo"></span><span id="no_adddevice_or_startio"></span><span id="NO_ADDDEVICE_OR_STARTIO"></span>没有 AddDevice 或 StartIo

由于文件系统筛选器驱动程序不是设备驱动程序，并且因此并不直接控制硬件设备，不应这样做[ **AddDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff540521)或[ **StartIo**](https://msdn.microsoft.com/library/windows/hardware/ff563858)例程。

### <a name="span-iddifferentdeviceobjectscreatedspanspan-iddifferentdeviceobjectscreatedspanspan-iddifferentdeviceobjectscreatedspandifferent-device-objects-created"></a><span id="Different_Device_Objects_Created"></span><span id="different_device_objects_created"></span><span id="DIFFERENT_DEVICE_OBJECTS_CREATED"></span>创建不同的设备对象

尽管文件系统筛选器驱动程序和设备驱动程序都创建设备对象，但它们的区别在于的数量和他们创建的设备对象的种类。

设备驱动程序创建物理和功能的设备对象表示的设备。 Plug and Play (PnP) 管理器建立和维护一个包含所有设备的全局设备树对象的创建的设备驱动程序。 文件系统筛选器驱动程序创建的设备对象不包含在此设备树中。

文件系统筛选器驱动程序不会创建物理或功能的设备对象。 相反，它们创建设备对象的控件和筛选设备对象。 *控制设备对象*表示筛选器驱动程序与系统和用户模式应用程序。 *筛选设备对象*执行实际工作的筛选特定文件系统或卷。 文件系统筛选器驱动程序通常将创建一个控制设备对象和一个或多个筛选设备对象。

### <a name="span-idotherdifferencesspanspan-idotherdifferencesspanspan-idotherdifferencesspanother-differences"></a><span id="Other_Differences"></span><span id="other_differences"></span><span id="OTHER_DIFFERENCES"></span>其他差异

由于文件系统筛选器驱动程序不是设备驱动程序，它们不会执行[直接内存访问 (DMA)](https://msdn.microsoft.com/library/windows/hardware/ff565374)。

与不同的设备筛选器驱动程序，它可以将附加高于或低于目标设备的功能驱动程序，文件系统筛选器驱动程序可以将附加仅上面的目标文件系统驱动程序。 因此，在设备驱动程序术语中，文件系统筛选器驱动程序可以是仅一个上限筛选器，永远不会较低的筛选器。

 

 




