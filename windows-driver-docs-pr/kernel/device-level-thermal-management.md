---
title: 设备级热量管理
description: 从 Windows 8 开始，Windows 支持对内核模式设备驱动程序进行设备级热量管理。
ms.assetid: C66E0050-04E8-4DCD-B989-94A97558C4CE
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3bcff98aa98a07689a67688573f90b958bc1501c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838748"
---
# <a name="device-level-thermal-management"></a>设备级热量管理


从 Windows 8 开始，Windows 支持对内核模式设备驱动程序进行设备级热量管理。 Windows 热量管理有以下目标：

-   防止硬件平台中的设备过热，这可能导致它们无法正确运行或 unreliably。
-   避免在计算机上进行用户辅助性的表面热的触摸屏输入。

与电源管理类似，热量管理必须在整个平台范围内实现，因为在全球热条件环境中协调设备本地热量约束。 通过提供全局协调，操作系统可以在多个设备之间分配冷却要求，从而最大限度地减少用户正在执行的任务的干扰。 热量要求可以与其他系统要求智能地平衡，如电源管理和对用户操作的响应。

与此相反，尝试在本地管理设备的温度级别的设备驱动程序与平台中的其他设备相隔离，更有可能做出不良的决策，导致电源使用效率低下和用户界面（UI）无响应。

若要参与全局热量管理，设备驱动程序可实现[GUID\_热量\_冷却\_接口](https://msdn.microsoft.com/library/windows/hardware/hh698265)驱动程序接口。 在系统启动过程中，系统提供的驱动程序（Acpi）会查询系统中的设备驱动程序，以确定哪些设备驱动程序支持此接口。 在调用驱动程序的设备的[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程后，无论何时，驱动程序都可以接收此接口的[**IRP\_MN\_QUERY\_接口**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface)请求。 为响应此请求，具有热量管理功能的设备的驱动程序可以提供指向[**热量\_冷却\_接口**](https://msdn.microsoft.com/library/windows/hardware/hh698275)结构的指针。 此结构包含指向由驱动程序实现的一组回调例程的指针。 若要在设备中管理热量级别，操作系统会直接调用这些例程。

此接口中的两个主体例程是[*ActiveCooling*](https://msdn.microsoft.com/library/windows/hardware/hh698235)和[*PassiveCooling*](https://msdn.microsoft.com/library/windows/hardware/hh698270)。 驱动程序的*ActiveCooling*例程在设备上啮合或 disengages 活动冷却。 例如，此例程可能会打开和关闭风扇。 驱动程序的*PassiveCooling*例程控制设备性能必须限制到的程度，以维持可接受的温度水平。 例如，可以调用此例程来以半速速度运行设备，以防止其过热。

默认情况下，在首次调用*ActiveCooling*例程之前，会断开活动冷却（例如，风扇处于关闭状态）。 第一次调用*PassiveCooling*例程之前，驱动程序将设备配置为在完全性能下运行，而不会有任何冷却限制。

根据设备硬件的功能，驱动程序可以实现其中一个或两个例程。 有关详细信息，请参阅[被动和主动冷却模式](passive-and-active-cooling-modes.md)。

 

 




