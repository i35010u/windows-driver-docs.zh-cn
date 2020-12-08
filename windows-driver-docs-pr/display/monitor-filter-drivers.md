---
title: 监视筛选器驱动程序
description: 监视筛选器驱动程序
keywords:
- 筛选器驱动程序 WDK 监视器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1584298988e114fe7bc4921c732438db95aecf97
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806369"
---
# <a name="monitor-filter-drivers"></a>监视筛选器驱动程序


## <span id="ddk_monitor_filter_drivers_gg"></span><span id="DDK_MONITOR_FILTER_DRIVERS_GG"></span>


Microsoft 提供了一个常规用途的监视器类函数驱动程序，Monitor.sys，用于处理与监视器相关的大部分任务。 不需要供应商提供的监视驱动程序，除非供应商希望提供的服务超出了 monitor 类函数驱动程序提供的服务。

如果监视器供应商选择提供筛选器驱动程序，则该驱动程序由一个筛选器设备对象表示，该对象位于监视器的设备堆栈中的功能设备对象之上。 筛选器驱动程序处理来自用户模式应用程序的请求，这些请求也由监视器供应商提供。 筛选器驱动程序和用户模式应用程序之间的接口是专用的，仅适用于监视供应商。

请注意，通过显示数据通道命令界面 (DDC/CI) 的编程控制监视器不会由监视设备堆栈处理，因此，监视器供应商不应为此目的编写筛选器驱动程序。

有关监视设备堆栈的表示形式，请参阅 [监视类函数驱动程序](monitor-class-function-driver.md)。

 

 





