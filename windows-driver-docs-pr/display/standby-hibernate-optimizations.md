---
title: 备用休眠优化
description: Windows 8 提供了您的驱动程序 （可选） 可以充分利用提高睡眠的系统性能和恢复了图形堆栈的优化。
ms.assetid: 1E71BFDF-3C67-41F6-968A-8AE54B54CCCB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0e12306d7874d99cb0900c94353baeb1c3a2877
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519363"
---
# <a name="standby-hibernate-optimizations"></a>备用休眠优化


Windows 8 提供了您的驱动程序 （可选） 可以充分利用提高睡眠的系统性能和恢复了图形堆栈的优化。

|                                                                                   |                                             |
|-----------------------------------------------------------------------------------|---------------------------------------------|
| Windows 显示器驱动程序模型 (WDDM) 的最低版本                               | 1.2                                         |
| 最低 Windows 版本                                                           | 8                                           |
| 驱动程序实现 — 仅完全图形和呈现                               | 可选                                    |
| [WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)要求和测试 | **Device.Graphics¦StandbyHibernateFlags** |

 

## <a name="span-idstandbyhibernatedevicedriverinterfaceddispanspan-idstandbyhibernatedevicedriverinterfaceddispanspan-idstandbyhibernatedevicedriverinterfaceddispanstandby-hibernate-device-driver-interface-ddi"></a><span id="Standby_hibernate_device_driver_interface__DDI_"></span><span id="standby_hibernate_device_driver_interface__ddi_"></span><span id="STANDBY_HIBERNATE_DEVICE_DRIVER_INTERFACE__DDI_"></span>备用休眠设备驱动程序接口 (DDI)


这些结构是新的或更新从 Windows 8，以支持备用休眠状态开始。

-   [**DXGK\_QUERYADAPTERINFOTYPE**](https://msdn.microsoft.com/library/windows/hardware/ff562010)
-   [**DXGK\_SEGMENTDESCRIPTOR3**](https://msdn.microsoft.com/library/windows/hardware/hh464086)
-   [**DXGK\_SEGMENTFLAGS**](https://msdn.microsoft.com/library/windows/hardware/ff562039)

可以支持此功能应可以利用我们的这些休眠优化每个设备。 当 WDDM 1.2 或更高版本的驱动程序枚举段功能时，它还必须设置一个或多个备用休眠标志**PreservedDuringStandby**， **PreservedDuringHibernate**，和**PartiallyPreservedDuringHibernate**。 请参阅备注的[ **DXGK\_SEGMENTFLAGS** ](https://msdn.microsoft.com/library/windows/hardware/ff562039)主题的更多详细信息。

## <a name="span-idstandbyoptspanspan-idstandbyoptspanusing-standby-hibernate-optimizations"></a><span id="standbyopt"></span><span id="STANDBYOPT"></span>使用 standby 休眠优化


PC 进入睡眠状态的转换或从睡眠状态恢复，多个操作发生，以确保该视频内存内容时正确保留并还原。 某些操作不是必需的可以避免：

-   集成的图形适配器作为视频内存，将使用系统内存。 当计算机进入睡眠状态时，始终刷新系统内存，因为没有将其移出是必需的。 因此，所引入的图形堆栈的延迟问题可以会遭遇停机对零延迟或几毫秒的顺序。
-   若要清除离散的适配器上的内存的总时间等于除以清除率的清除的内存量。 因此，可以通过减少要清除的内存量减少的时间。

这些操作的目标是确保将被丢弃的唯一数据是可以重新创建的数据。

WDDM 1.2 驱动程序可以充分利用这些优化，通过指定应在电源状态转换期间保留的分配。

较新的代的离散图形适配器可以用于刷新它们处于待机状态 （正在刷新 vram 能够自我） 时的内存。 这些适配器将从这些优化中受益。

逐出仍将适用于没有自刷新的 vram 能够功能的离散图形适配器。 在这些情况下，性能优化是最大程度减少保留的数据量。 例如，在视频内存中未使用的数据提供分配，丢弃分配和未使用直接内存访问 (DMA) 缓冲区可以被丢弃。

此功能可以产生以下优势：

-   不执行任何工作：（具有自刷新 vram 能够功能） 的集成和离散图形适配器，在引入的图形堆栈的延迟可以关闭对零延迟或几毫秒的顺序。
-   执行较少工作：离散图形适配器上的性能改进是主要取决于视频内存中多少未使用的数据将被丢弃。
-   移入垃圾桶降低了的内存：更大的内存量逐出的内存移入垃圾桶越大效果。 这在离散图形适配器上具有更大的影响，因为它们需要大量的系统内存中收回。

## <a name="span-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>硬件认证要求


有关实现此功能时，必须满足硬件设备要求的信息，请参阅相关[WHCK 文档](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)上**Device.Graphics...StandbyHibernateFlags**。

请参阅[WDDM 1.2 功能](wddm-v1-2-features.md)评审的 Windows 8 一起添加的功能。

 

 





