---
title: 全局热量管理
description: 了解 GUID_THERMAL_COOLING_INTERFACE 驱动程序接口及其在全局热量管理中的使用方式。
keywords:
- 全局热量管理
- 散热
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27bace1c14adb6c67f4728a0f361ffb2cb16f29f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824011"
---
# <a name="global-thermal-management"></a>全局热量管理 

GUID_THERMAL_COOLING_INTERFACE 驱动程序接口允许设备驱动程序在硬件平台中的各种设备上参与全局热量管理。 具有热量管理功能的设备的驱动程序实现此接口中的回调例程。 操作系统调用这些例程来动态管理平台中的热量级别，以响应用户活动和环境条件的变化。

通过防止过热，Windows 热量管理可使设备可靠运行，并防止用户可访问的表面变为 uncomfortably 热。 Windows 智能地平衡了平台中设备的热量级别要求，延长了平台处理电池电量的时间，并保持了始终开机和始终连接的计算机的外观。

有关详细信息，请参阅 [设备级热量管理](device-level-thermal-management.md)。

