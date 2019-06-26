---
title: 卸载筛选器驱动程序
description: 卸载筛选器驱动程序
ms.assetid: e7ef209f-ab61-4644-a641-2fef09023a24
keywords:
- 筛选器驱动程序 WDK 连接网络、 卸载
- NDIS 筛选器驱动程序 WDK，卸载
- 正在卸载的筛选器驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5281f141ccdf5711b5df6a95812abb3b2e110480
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382096"
---
# <a name="unloading-a-filter-driver"></a>卸载筛选器驱动程序





与的 NDIS 筛选器驱动程序相关联的驱动程序对象指定[ *Unload* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)调用的例程*FilterDriverUnload*。 系统可以调用*FilterDriverUnload*例程时，已删除的筛选器驱动程序服务的所有微型端口适配器。

[*Unload* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)应释放任何特定于驱动程序的资源。 必须销毁任何筛选器驱动程序创建的设备对象。 系统可以完成驱动程序卸载操作后的*FilterDriverUnload*返回。

卸载函数的功能是特定于驱动程序。 作为一般规则[ *Unload* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)应撤消在驱动程序初始化期间执行的操作。 有关驱动程序初始化的详细信息，请参阅[初始化筛选器驱动程序](initializing-a-filter-driver.md)。

筛选器驱动程序必须调用[ **NdisFDeregisterFilterDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfderegisterfilterdriver)函数从[*卸载*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)。 **NdisFDeregisterFilterDriver**调用[ *FilterDetach* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_detach)分离与此筛选器驱动程序相关联的所有当前所附加的筛选器模块。

有关卸载的筛选器驱动程序的详细信息，请参阅[停止驱动程序堆栈](stopping-a-driver-stack.md)。
