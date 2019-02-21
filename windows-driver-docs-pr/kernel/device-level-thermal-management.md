---
title: 设备级别的热量管理
description: 从 Windows 8 开始，Windows 支持设备级热量管理内核模式设备驱动程序。
ms.assetid: C66E0050-04E8-4DCD-B989-94A97558C4CE
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9fae6e9bcb09ee5192eb537f22682ea3aa0acea1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541893"
---
# <a name="device-level-thermal-management"></a>设备级别的热量管理


从 Windows 8 开始，Windows 支持设备级热量管理内核模式设备驱动程序。 Windows 热量管理具有这些目标：

-   阻止从过热，一种硬件平台这可能导致它们不正确或 unreliably 而运行的设备。
-   避免对用户可访问的图面上计算机机箱进行轻松触摸或保存温度过高。

通过协调设备本地全局热量条件的上下文中的散热约束，必须在平台范围内实现类似于电源管理，热量管理。 通过提供全局协调，操作系统可以跨多个设备最大程度减少干扰用户正在执行任务的方式分发冷却需求。 热要求与其他系统要求，如电源管理和对用户操作的响应能力可以智能地进行平衡。

与此相反，尝试管理其设备本地，散热级别在隔离在平台中，与其他设备的设备驱动程序是更有可能做出不佳导致效率低下的电源使用情况和响应用户界面 (UI) 的决策。

若要参与全局热量管理，设备驱动程序实现[GUID\_热量\_冷却\_接口](https://msdn.microsoft.com/library/windows/hardware/hh698265)驱动程序接口。 系统启动期间，系统提供驱动程序，Acpi.sys，系统以确定其中哪些支持此接口中的查询的设备驱动程序。 驱动程序可以接收[ **IRP\_MN\_查询\_接口**](https://msdn.microsoft.com/library/windows/hardware/ff551687)请求为此接口后随时[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)调用驱动程序的设备的例程。 以响应此请求，具有热量管理功能的设备的驱动程序可以提供一个指向[**热量\_冷却\_接口**](https://msdn.microsoft.com/library/windows/hardware/hh698275)结构。 此结构包含的一组由驱动程序实现的回调例程的指针。 若要管理的设备中的散热级别，操作系统将调用这些例程直接。

此接口中的两个主体例程都[ *ActiveCooling* ](https://msdn.microsoft.com/library/windows/hardware/hh698235)并[ *PassiveCooling*](https://msdn.microsoft.com/library/windows/hardware/hh698270)。 在驱动程序*ActiveCooling*例程公民或脱开 active 冷却设备中。 例如，此例程可能打开和关闭打开风扇。 在驱动程序*PassiveCooling*例程控制到必须限制的设备的性能来维护可接受的热量级别的程度。 例如，可能会调用此例程以半速以防止它过热运行设备。

默认情况下，首次调用前*ActiveCooling*例程，active 冷却未占用 （例如，风扇处于关闭状态）。 首次调用前*PassiveCooling*例程，该驱动程序将设备配置为在完整的性能，不带任何冷却限制运行。

驱动程序可以实现一个或两个例程，具体取决于设备硬件的功能。 有关详细信息，请参阅[被动和 Active 冷却模式](passive-and-active-cooling-modes.md)。

 

 




