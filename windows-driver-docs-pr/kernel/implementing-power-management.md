---
title: Windows 驱动程序的电源管理
description: 内核模式驱动程序应管理其硬件设备，以便他们会打开并可供使用时需要但在低功耗模式下运行和未使用时生成任何不必要的系统活动。
ms.assetid: ed422428-8a87-4a2d-830d-e156ef949b13
keywords:
- 电源管理 WDK 内核
- 内核模式驱动程序 WDK、 电源管理
- 能源 WDK 电源管理
- 启动 power management WDK 内核
- 关闭电源管理 WDK 内核
- 设备电源管理 WDK 内核
- 还原 power WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec7e98caba00db18d17045e9f7c6bed8ece5065a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366171"
---
# <a name="power-management-for-windows-drivers"></a>Windows 驱动程序的电源管理


内核模式驱动程序应管理其硬件设备，以便他们会打开并可供使用时需要但在低功耗模式下运行和未使用时生成任何不必要的系统活动。 [*电源管理器*](power-manager.md)是负责协调中的硬件平台的设备的电源状态的 Windows 内核组件。




在准备其设备进入低能耗模式和驱动程序收到通知后从电源管理器在其设备重新打开时，电源管理器指示驱动程序。 驱动程序是负责向电源管理器报告其电源功能。 驱动程序必须检测时他们的设备处于空闲状态 （和可以切换到低功耗模式下） 或依赖于此类检测的电源管理器的选项。

## <a name="in-this-section"></a>本节内容


-   [电源管理简介](introduction-to-power-management.md)
-   [内核模式电源管理组件](kernel-mode-power-management-components.md)
-   [电源管理职责的驱动程序](power-management-responsibilities-for-drivers.md)
-   [处理 Power Irp 规则](rules-for-handling-power-irps.md)
-   [各个设备管理的电源](managing-power-for-individual-devices.md)
-   [处理系统电源状态的请求](handling-system-power-state-requests.md)
-   [电源管理框架的概述](overview-of-the-power-management-framework.md)
-   [平台扩展插件 (Pep)](platform-extension-plug-ins--peps-.md)
-   [支持具有唤醒功能的设备](supporting-devices-that-have-wake-up-capabilities.md)
-   [系统以提高启动性能](improving-system-startup-performance.md)
-   [设备级别的热量管理](device-level-thermal-management.md)

 

 




