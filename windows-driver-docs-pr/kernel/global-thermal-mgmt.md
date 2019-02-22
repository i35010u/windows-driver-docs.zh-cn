---
title: 全局热量管理
description: 处理一个 IRP_MN_SURPRISE_REMOVAL 请求
ms.assetid: 3CBF44B2-891A-4B68-97F6-3563EC0D5122
keywords:
- 全局热量管理
- 温度
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3177ded380484b2f4661582cc643680672eaa4bd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533906"
---
# <a name="global-thermal-management"></a>全局热量管理 

可通过 GUID_THERMAL_COOLING_INTERFACE 驱动程序接口的设备驱动程序参与全局热量管理跨多个中的硬件平台的设备。 在此界面，具有热量管理功能的设备的驱动程序执行的回调例程。 操作系统将调用这些例程可以动态地管理用户活动和环境条件中的响应的更改在平台中的散热级别。

通过防止过热，Windows 热量管理保留设备可靠地运行，并阻止用户可访问的图面变得 uncomfortably 热门。 Windows 智能地平衡的温度级别要求在平台中的设备的可扩展平台可以靠电池电量的时间和维护始终处于打开和始终连接的计算机的外观。

有关详细信息，请参阅[设备级别的热量管理](device-level-thermal-management.md)。

