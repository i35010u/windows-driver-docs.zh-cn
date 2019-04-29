---
title: 被动和主动散热模式
description: 从 Windows 8 开始，具有热量管理功能的设备可以公开到操作系统 GUID_THERMAL_COOLING_INTERFACE 驱动程序接口通过这些功能。
ms.assetid: 4AB70ED3-E71A-45EE-818D-7DCDE0FFBCB3
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 16a346a52e347e5859030e57dc8057abcfc7269a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369275"
---
# <a name="passive-and-active-cooling-modes"></a>被动和主动散热模式


从 Windows 8 开始，具有热量管理功能的设备可以公开到操作系统通过这些功能[GUID\_热量\_冷却\_接口](https://msdn.microsoft.com/library/windows/hardware/hh698265)驱动程序接口。 此接口中的两个主体驱动程序实现的回调例程都[ *PassiveCooling* ](https://msdn.microsoft.com/library/windows/hardware/hh698270)并[ *ActiveCooling*](https://msdn.microsoft.com/library/windows/hardware/hh698235)。 被动冷却功能实现的驱动程序*PassiveCooling*例程。 具有活动冷却功能实现的驱动程序*ActiveCooling*例程。 在响应计算机使用情况或环境条件中的更改，操作系统将调用一个 （或可能是两者） 的这些例程来管理动态中的硬件平台的热量级别。

高级配置和电源接口 (ACPI) 启用硬件平台供应商的联系，以在平台分区成称为热区域的区域。 传感器设备跟踪每个热量区域中的温度。 在热区域开始过热，操作系统可以采取措施以冷却区域中的设备。 这些操作可以划分为被动冷却或活动冷却。

若要执行被动冷却，操作系统会限制以减少这些设备发热量热量区域中的一个或多个设备。 限制可能涉及降低驱动器在设备的时钟频率、 降低电压提供给设备，或关闭设备的一部分。 一般来说，限制将限制设备性能。

若要执行 active 冷却，操作系统会启用的冷却设备，如风扇。 被动冷却减少热量区域; 中的设备使用电源active 冷却会增加功率消耗。

在硬件平台的设计中，决定使用被动冷却还是 active 冷却取决于硬件平台、 平台的电源和平台的使用方式的物理特征。

Active 冷却可能更容易实现，但有几个潜在的缺点。 添加 active 冷却设备 （例如，风扇） 可能会增加成本和大小的硬件平台。 运行活动的冷却设备所需的功能可能会降低电池供电的平台可以靠电池电量的时间。 风扇噪音，可能不需要在某些应用程序，并且赛事的球迷们需要通风。

被动冷却是提供给许多移动设备的唯一冷却模式。 具体而言，手持计算平台很可能已经关闭情况下，并使用电池运行。 这些平台通常包含可能会限制性能来减少热量生成的设备。 这些设备包括处理器、 图形处理单元 (Gpu)、 电池充电器，并且显示背光功能。

手持计算平台通常使用包含处理器和 Gpu 芯片 (SoC) 芯片中的系统和 SoC 硬件供应商提供这些设备的热量管理软件。 但是，外围设备，如电池充电器和显示背光功能是外部的 SoC 芯片。 这些设备的供应商必须提供设备驱动程序，并且这些驱动程序必须提供任何热量管理支持，可能需要的设备。 设备驱动程序以支持热量管理相对简单的方式是实现 GUID\_热量\_冷却\_接口驱动程序接口。

 

 




