---
title: 存储类驱动程序的常规功能
description: 存储类驱动程序的常规功能
keywords:
- 存储类驱动程序 WDK，功能
- 类驱动程序 WDK 存储，功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eac83fe4169d034f51c96fe578ba5f4e323f17f0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806673"
---
# <a name="storage-class-drivers-general-functionality"></a>存储类驱动程序的常规功能


## <span id="ddk_storage_class_drivers_general_functionality_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_GENERAL_FUNCTIONALITY_KG"></span>


对于存储端口驱动程序，存储类驱动程序是具有内置的设备类型特定功能的较高级别的驱动程序。 通常，每个存储类驱动程序都负责以下各项：

-   通过 PnP 管理器将 () PDO 传递到其 *AddDevice* 例程的物理设备对象表示的每个设备声明

-   对于每个此类 PDO， (FDO 创建功能设备对象) 并将其附加到设备堆栈

-   如果驱动程序控制分区设备，则创建 (PDOs) 的物理设备对象，以表示每个分区并响应枚举请求

-    (Irp 解释系统 i/o 请求) 

-   将 Irp 映射到 SCSI 类/端口接口请求 (SRBs 与 SCSI CDBs) 

-   为请求建立超时值

-   限制数据传输的大小以适应基础 HBA 的限制

-   处理存储端口驱动程序尚未处理的错误条件，如检查条件状态或总线重置

 

 




