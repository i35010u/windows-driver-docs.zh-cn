---
title: 简介
description: 简介
ms.assetid: 0AEFA19D-C270-4777-8C08-E6056FBB6BC5
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: e6ef00ecde147cb9e241651cb9f0b0385aae79c6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56465563"
---
# <a name="storage-driver-design-guide"></a>存储驱动程序设计指南


存储驱动程序包括[类](storage-class-drivers.md)、[端口](storage-port-drivers.md)、[微型端口](storage-miniport-drivers.md)和[筛选器](storage-filter-drivers.md)驱动程序。 通常情况下，设备供应商会为特定的适配器或适配器类型实现微型端口驱动程序。 可以定义一个新的存储类，并为其开发新的类驱动程序，尽管这不常见。 Windows 中的存储类包括磁盘类、CDROM 类、USB 存储类和加密驱动器类。 存储驱动程序开发通常仅限于编写一个适用于 [StorPort](storport-driver.md) 端口驱动程序的微型端口驱动程序。

其他类型的存储设备驱动程序包括安全[接收器](storage-silo-drivers.md)驱动程序和特定于设备且适合多路径 I/O 的模块 (DSM)。 开发 [WMI](https://msdn.microsoft.com/library/windows/hardware/ff567016) 提供程序作为驱动程序的控制接口是为了进行存储管理。

## <a name="span-idstoragedriverwdkresourcesspanspan-idstoragedriverwdkresourcesspanspan-idstoragedriverwdkresourcesspanoverview"></a><span id="Storage_Driver_WDK_Resources"></span><span id="storage_driver_wdk_resources"></span><span id="STORAGE_DRIVER_WDK_RESOURCES"></span>概述
本设计指南包含以下部分：
* [开发 Windows 存储驱动程序的路线图](roadmap-for-developing-storage-drivers.md)  
* [Storport 微型端口驱动程序开发路线图](roadmap-for-developing-storport-miniport-drivers.md)  
* [存储驱动程序](storage-drivers.md)  
* [存储类驱动程序](storage-class-drivers.md)  
* [存储端口驱动程序](storage-port-drivers.md)  
* [存储器微型端口驱动程序](storage-miniport-drivers.md)  
* [存储器虚拟微型端口驱动程序](storage-virtual-miniport-drivers.md)  
* [存储筛选器驱动程序](storage-filter-drivers.md)  
* [故障转储筛选器驱动程序](crash-dump-filter-drivers.md)  
* [存储接收器驱动程序](storage-silo-drivers.md)  
* [CD-ROM 驱动程序](cd-rom-drivers.md)  
* [磁带驱动程序](tape-drivers.md)  
* [更换器驱动程序](changer-drivers.md)  
* [存储方案](storage-scenarios.md)  

## <a name="samples"></a>示例
若要了解如何开发可以运行的存储驱动程序，比较实际的方法是研究示例。 GitHub 上提供[示例存储驱动程序](https://github.com/Microsoft/Windows-driver-samples)。

## <a name="span-iddriververificationforstorportspanspan-iddriververificationforstorportspanspan-iddriververificationforstorportspandriver-verification-for-storport"></a><span id="Driver_Verification_for_StorPort"></span><span id="driver_verification_for_storport"></span><span id="DRIVER_VERIFICATION_FOR_STORPORT"></span>StorPort 的驱动程序验证


在驱动程序开发过程中使用代码分析工具并进行测试有助于捕获存储驱动程序中的性能问题和缺陷。 [静态驱动程序验证程序 (SDV)](https://msdn.microsoft.com/library/windows/hardware/ff552808) 工具可用于发现存储驱动程序代码中的缺陷。 SDV 中包含的符合性[规则](https://msdn.microsoft.com/library/windows/hardware/hh454238)用于验证微型端口驱动程序是否正确使用了 StorPort 例程。

有关存储硬件认证的测试，请参阅 [Windows 硬件认证工具包 (HCK)](https://go.microsoft.com/fwlink/p/?LinkId=733613)。 有关存储设备的测试，请参阅 HCK 的 [Devices.Storage](https://msdn.microsoft.com/library/windows/hardware/jj125097) 类别。

 

 




