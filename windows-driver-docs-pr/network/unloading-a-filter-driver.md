---
title: 卸载筛选器驱动程序
description: 卸载筛选器驱动程序
keywords:
- 筛选器驱动程序 WDK 网络，卸载
- NDIS 筛选器驱动程序 WDK，卸载
- 卸载筛选器驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f558cc9ba7efd61cc99c0bb368a15a31d1de224c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822775"
---
# <a name="unloading-a-filter-driver"></a>卸载筛选器驱动程序





与 NDIS 筛选器驱动程序关联的驱动程序对象指定一个名为 *FilterDriverUnload* 的 [*卸载*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)例程。 当筛选器驱动程序服务已删除时，系统可以调用 *FilterDriverUnload* 例程。

[*Unload*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload) 应释放任何特定于驱动程序的资源。 必须销毁筛选器驱动程序创建的任何设备对象。 在 *FilterDriverUnload* 返回后，系统可以完成驱动程序卸载操作。

Unload 函数的功能特定于驱动程序。 作为一般规则， [*Unload*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload) 应撤消驱动程序初始化过程中执行的操作。 有关驱动程序初始化的详细信息，请参阅 [初始化筛选器驱动程序](initializing-a-filter-driver.md)。

筛选器驱动程序必须从 [*Unload*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)调用 [**NdisFDeregisterFilterDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfderegisterfilterdriver)函数。 **NdisFDeregisterFilterDriver** 调用 [*FilterDetach*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_detach) 以分离所有与此筛选器驱动程序关联的当前附加的筛选器模块。

有关卸载筛选器驱动程序的详细信息，请参阅 [停止驱动程序堆栈](stopping-a-driver-stack.md)。
