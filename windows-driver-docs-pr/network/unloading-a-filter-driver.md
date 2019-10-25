---
title: 卸载筛选器驱动程序
description: 卸载筛选器驱动程序
ms.assetid: e7ef209f-ab61-4644-a641-2fef09023a24
keywords:
- 筛选器驱动程序 WDK 网络，卸载
- NDIS 筛选器驱动程序 WDK，卸载
- 卸载筛选器驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a49602bb20d6c33e8104b84f2ef5be926f3ebc22
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843011"
---
# <a name="unloading-a-filter-driver"></a>卸载筛选器驱动程序





与 NDIS 筛选器驱动程序关联的驱动程序对象指定一个名为*FilterDriverUnload*的[*卸载*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)例程。 当筛选器驱动程序服务已删除时，系统可以调用*FilterDriverUnload*例程。

[*Unload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)应释放任何特定于驱动程序的资源。 必须销毁筛选器驱动程序创建的任何设备对象。 在*FilterDriverUnload*返回后，系统可以完成驱动程序卸载操作。

Unload 函数的功能特定于驱动程序。 作为一般规则， [*Unload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)应撤消驱动程序初始化过程中执行的操作。 有关驱动程序初始化的详细信息，请参阅[初始化筛选器驱动程序](initializing-a-filter-driver.md)。

筛选器驱动程序必须从[*Unload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)调用[**NdisFDeregisterFilterDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfderegisterfilterdriver)函数。 **NdisFDeregisterFilterDriver**调用[*FilterDetach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_detach)以分离所有与此筛选器驱动程序关联的当前附加的筛选器模块。

有关卸载筛选器驱动程序的详细信息，请参阅[停止驱动程序堆栈](stopping-a-driver-stack.md)。
