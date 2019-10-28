---
title: 文件系统筛选器驱动程序与设备驱动程序的类似程度如何
description: 文件系统筛选器驱动程序与设备驱动程序的类似程度如何
ms.assetid: 7797239e-e0cc-4422-bcc6-31cfe6efd8e4
keywords:
- 筛选器驱动程序 WDK 文件系统和设备驱动程序
- 文件系统筛选器驱动程序（WDK）和设备驱动程序
- 设备驱动程序 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06d640ff0c33546389bf0c752658cedd9492e047
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841216"
---
# <a name="how-file-system-filter-drivers-are-similar-to-device-drivers"></a>文件系统筛选器驱动程序与设备驱动程序的类似程度如何


## <span id="ddk_how_file_system_filter_drivers_are_similar_to_device_drivers_if"></span><span id="DDK_HOW_FILE_SYSTEM_FILTER_DRIVERS_ARE_SIMILAR_TO_DEVICE_DRIVERS_IF"></span>


以下小节介绍了 Microsoft Windows 操作系统中的文件系统筛选器驱动程序和设备驱动程序之间的一些相似性。

### <a name="span-idsimilar_structurespanspan-idsimilar_structurespanspan-idsimilar_structurespansimilar-structure"></a><span id="Similar_Structure"></span><span id="similar_structure"></span><span id="SIMILAR_STRUCTURE"></span>类似结构

与设备驱动程序一样，文件系统筛选器驱动程序具有[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)、[调度](https://docs.microsoft.com/windows-hardware/drivers/kernel/writing-dispatch-routines)和[i/o 完成](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-iocompletion-routines)例程。 它们调用设备驱动程序调用的许多相同内核模式例程，并筛选与它们关联的设备（即文件系统卷）的 i/o 请求。

### <a name="span-idsimilar_functionalityspanspan-idsimilar_functionalityspanspan-idsimilar_functionalityspansimilar-functionality"></a><span id="Similar_Functionality"></span><span id="similar_functionality"></span><span id="SIMILAR_FUNCTIONALITY"></span>类似的功能

由于文件系统筛选器驱动程序和设备驱动程序是 i/o 系统的一部分，因此它们都接收[i/o 请求数据包](https://docs.microsoft.com/windows-hardware/drivers/kernel/packet-driven-i-o-with-reusable-irps)（irp），并对其执行操作。

与设备驱动程序一样，文件系统筛选器驱动程序还可以创建自己的 Irp，并将其发送到较低级别的驱动程序。

两种类型的驱动程序都可以注册各种系统事件的通知（通过使用回调函数）。

### <a name="span-idother_similaritiesspanspan-idother_similaritiesspanspan-idother_similaritiesspanother-similarities"></a><span id="Other_Similarities"></span><span id="other_similarities"></span><span id="OTHER_SIMILARITIES"></span>其他相似性

与设备驱动程序一样，文件系统筛选器驱动程序可能会收到[I/o 控制代码](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-i-o-control-codes)（IOCTLs）的简介。 但是，文件系统筛选器驱动程序还可以接收--并定义--[文件系统控制代码](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)（FSCTLs）。

与设备驱动程序一样，文件系统筛选器驱动程序可以配置为在系统启动时加载，或在系统启动过程完成后再加载。

 

 




