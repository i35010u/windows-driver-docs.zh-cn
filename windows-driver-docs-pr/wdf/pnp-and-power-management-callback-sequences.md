---
title: PnP 和电源管理回调序列
description: 下面的主题介绍的顺序在该框架将调用 WDF 驱动程序 PnP 和电源管理事件的回调函数
ms.assetid: 74663110-8E3C-4AC4-8BCD-63C788047F38
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3fa9d5546027d1509266eee098024c1af27c52ce
ms.sourcegitcommit: 1a5d7884cec9dd8d2b85242bee78b56a1cf8e4c9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/01/2019
ms.locfileid: "58761838"
---
# <a name="pnp-and-power-management-callback-sequences"></a>PnP 和电源管理回调序列


以下主题介绍的序列中的框架将调用 WDF (KMDF 和 UMDF v2) 驱动程序 PnP 和电源管理事件回调函数：

-   [函数或筛选器驱动程序的启动顺序](power-up-sequence-for-a-function-or-filter-driver.md)
-   [总线驱动程序的启动顺序](power-up-sequence-for-a-bus-driver.md)
-   [电源关闭和删除序列的函数或筛选器驱动程序](power-down-and-removal-sequence-for-a-function-or-filter-driver.md)
-   [电源关闭和总线驱动程序的删除顺序](power-down-and-removal-sequence-for-a-bus-driver.md)
-   [意外删除序列](surprise-removal-sequence.md)
-   [WDM Irp 和相应 WDF 事件回调](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdm-irps-and-kmdf-event-callback-functions)

下列主题确定典型的即插即用和电源管理方案，并显示在该框架将调用驱动程序的事件回调函数在这些方案期间的序列：

- [用户插入设备](a-user-plugs-in-a-device.md)
- [用户断开设备](a-user-unplugs-a-device.md)
- [在设备进入低功耗状态](a-device-enters-a-low-power-state.md)
- [设备将恢复工作状态](a-device-returns-to-its-working-state.md)
- [PnP 管理器将重新分发的系统资源](the-pnp-manager-redistributes-system-resources.md)
 

 





