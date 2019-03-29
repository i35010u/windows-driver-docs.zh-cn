---
title: PnP 和电源管理回调序列
description: 下面的主题介绍的顺序在该框架将调用 KMDF 驱动程序 PnP 和电源管理事件的回调函数
ms.assetid: 74663110-8E3C-4AC4-8BCD-63C788047F38
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71893487e3858a678a94a93a75ca86abfb8dbe93
ms.sourcegitcommit: 68bfa1f69229b7ac29d0e98f049734f5bc566a30
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/19/2019
ms.locfileid: "58187468"
---
# <a name="pnp-and-power-management-callback-sequences"></a>PnP 和电源管理回调序列


以下主题介绍的顺序在该框架将调用 KMDF 驱动程序 PnP 和电源管理事件的回调函数：

-   [函数或筛选器驱动程序的启动顺序](power-up-sequence-for-a-function-or-filter-driver.md)
-   [总线驱动程序的启动顺序](power-up-sequence-for-a-bus-driver.md)
-   [电源关闭和删除序列的函数或筛选器驱动程序](power-down-and-removal-sequence-for-a-function-or-filter-driver.md)
-   [电源关闭和总线驱动程序的删除顺序](power-down-and-removal-sequence-for-a-bus-driver.md)
-   [意外删除序列](surprise-removal-sequence.md)
-   [WDM Irp 和相应 WDF 事件回调](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdm-irps-and-kmdf-event-callback-functions)

有关 UMDF 回调序列的信息，请参阅[PnP 和电源管理方案，在 UMDF](pnp-and-power-management-scenarios-in-umdf.md)。

 

 





