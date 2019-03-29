---
title: 监视筛选器驱动程序
description: 监视筛选器驱动程序
ms.assetid: cf2bd4c5-d586-4202-ad79-4e7ff9ad6061
keywords:
- 筛选器驱动程序 WDK 监视器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90fa623cda5ab86e461cc7b771073e1213e6c51d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577276"
---
# <a name="monitor-filter-drivers"></a>监视筛选器驱动程序


## <span id="ddk_monitor_filter_drivers_gg"></span><span id="DDK_MONITOR_FILTER_DRIVERS_GG"></span>


Microsoft 提供了常规用途监视器类功能驱动程序，Monitor.sys，用于处理大多数监视器相关的任务。 供应商想要提供所提供的监视器类功能驱动程序以外的服务才供应商提供的监视器驱动程序不需要。

如果监视器供应商选择提供筛选器驱动程序，该驱动程序由位于监视器的设备堆栈中的功能的设备对象上方的筛选器设备对象表示。 筛选器驱动程序处理来自用户模式应用程序，还提供监视供应商的请求。 筛选器驱动程序和用户模式应用程序之间的接口是私有的仅监视器供应商。

请注意使监视器供应商不应实现此目的编写筛选器驱动程序，通过显示数据通道命令接口 (DDC/CI) 的监视器的编程控件不处理由监视器设备堆栈。

有关监视设备堆栈的表示形式，请参阅[监视器类功能驱动程序](monitor-class-function-driver.md)。

 

 





