---
title: 待机休眠优化
description: Windows 8 为图形堆栈提供优化，你的驱动程序可以选择利用它来提高睡眠和恢复系统性能。
ms.assetid: 1E71BFDF-3C67-41F6-968A-8AE54B54CCCB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6bda009ca528a5e774775ce6af5c1883521b8bfd
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968588"
---
# <a name="standby-hibernate-optimizations"></a>待机休眠优化


Windows 8 为图形堆栈提供优化，你的驱动程序可以选择利用它来提高睡眠和恢复系统性能。

**最小 Windows 显示驱动程序模型（WDDM）版本**：1。2

**最低 Windows 版本**：8

**驱动程序实现-完整图形和仅呈现**：可选

** [WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)要求和测试**： **Device. Graphics ¦ StandbyHibernateFlags**


 

## <a name="span-idstandby_hibernate_device_driver_interface__ddi_spanspan-idstandby_hibernate_device_driver_interface__ddi_spanspan-idstandby_hibernate_device_driver_interface__ddi_spanstandby-hibernate-device-driver-interface-ddi"></a><span id="Standby_hibernate_device_driver_interface__DDI_"></span><span id="standby_hibernate_device_driver_interface__ddi_"></span><span id="STANDBY_HIBERNATE_DEVICE_DRIVER_INTERFACE__DDI_"></span>备用休眠设备驱动程序接口（DDI）


从 Windows 8 开始，这些结构是新的或更新的，以支持备用休眠。

-   [**DXGK \_ QUERYADAPTERINFOTYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ne-d3dkmddi-_dxgk_queryadapterinfotype)
-   [**DXGK \_ SEGMENTDESCRIPTOR3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor3)
-   [**DXGK \_ SEGMENTFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentflags)

可以支持此功能的每个设备都应利用这些休眠优化。 当 WDDM 1.2 或更高版本的驱动程序枚举段功能时，它还必须设置一个或多个备用休眠标志**PreservedDuringStandby**、 **PreservedDuringHibernate**和**PartiallyPreservedDuringHibernate**。 有关更多详细信息，请参阅[**DXGK \_ SEGMENTFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentflags)主题的备注。

## <a name="span-idstandbyoptspanspan-idstandbyoptspanusing-standby-hibernate-optimizations"></a><span id="standbyopt"></span><span id="STANDBYOPT"></span>使用备用休眠优化


当电脑转换为睡眠状态或从睡眠状态恢复时，将发生若干操作以确保正确保留和还原视频内存内容。 其中一些操作是不必要的，可以避免：

-   集成图形适配器使用系统内存作为视频内存。 由于在计算机进入睡眠状态时始终刷新系统内存，因此不需要任何逐出。 因此，图形堆栈引入的延迟可能会降低到零延迟或几毫秒的顺序。
-   清除离散适配器上的内存的总时间等于清除的内存量除以清除率。 这样可以减少要清除的内存量，从而减少时间。

这些操作的目标是确保丢弃的唯一数据是可以重新创建的数据。

WDDM 1.2 驱动程序可以通过指定在电源状态转换期间应保留哪些分配来利用这些优化。

较新版本的离散图形适配器可设计为在处于待机状态时刷新其内存（自行刷新 VRAM）。 这些适配器将从这些优化中受益。

对于没有自我刷新 VRAM 功能的离散图形适配器，逐出仍适用。 在这些情况下，性能优化旨在最大程度地减少所保留的数据量。 例如，可以放弃视频内存中未使用的数据，例如提供的分配、丢弃的分配和未使用的直接内存访问（DMA）缓冲区。

此功能可带来以下好处：

-   不执行任何操作：对于集成和离散图形适配器（使用自我刷新 VRAM 功能），图形堆栈引入的延迟可能会降低到零延迟或几毫秒的顺序。
-   执行更少的工作：在离散图形适配器上，性能改进主要取决于丢失视频内存中未使用的数据的数量。
-   减少内存 trashing：逐出的内存量越大，内存 trashing 的影响越大。 这会对离散图形适配器造成较大的影响，因为它们需要大量的系统内存才能收回。

## <a name="span-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>硬件认证要求


有关硬件设备实现此功能时必须满足的要求的信息，请参阅相关[WHCK 文档](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)，了解**¦ StandbyHibernateFlags**。

请参阅[WDDM 1.2 功能](wddm-v1-2-features.md)，了解 Windows 8 中添加的功能。

 

 





