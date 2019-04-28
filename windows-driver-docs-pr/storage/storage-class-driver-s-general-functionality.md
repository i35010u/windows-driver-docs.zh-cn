---
title: 存储类驱动程序的常规功能
description: 存储类驱动程序的常规功能
ms.assetid: 4fc92d20-5570-4680-bc7b-f6e84524a672
keywords:
- 存储类驱动程序 WDK，功能
- 类驱动程序 WDK 存储功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8669a4124f033dad43947321fc7d17ad62b2a533
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339014"
---
# <a name="storage-class-drivers-general-functionality"></a>存储类驱动程序的常规功能


## <span id="ddk_storage_class_drivers_general_functionality_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_GENERAL_FUNCTIONALITY_KG"></span>


存储端口驱动程序存储类驱动程序是具有内置的设备类型特定功能的更高级别的驱动程序。 一般情况下，每个存储类驱动程序是负责执行以下：

-   声明由物理设备对象 (PDO) 表示每个设备传递给其*AddDevice*例程 PnP 管理器

-   对每个此类 PDO，创建功能的设备对象 (FDO) 并将其附加到设备堆栈

-   如果该驱动程序控制可分区的设备，创建物理设备对象 (PDOs) 来表示每个分区和响应的枚举请求

-   解释系统 I/O 请求 (Irp)

-   将 Irp 映射到 SCSI 类/端口接口请求 (使用 SCSI Cdb Srb)

-   建立超时值的请求

-   数据传输，以满足基础 HBA 的限制的大小限制

-   处理错误条件，不能处理的存储端口驱动程序，例如检查条件状态或总线重置

 

 




