---
title: NDIS 驱动程序堆栈
description: NDIS 驱动程序堆栈
ms.assetid: 38302f1e-9b5a-4fc5-8e69-888929e5a892
keywords:
- 驱动程序堆栈 WDK 网络 NDIS 基本配置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 359ad690544d057eebc7874646ca932ca50ed8ae
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525825"
---
# <a name="ndis-driver-stack"></a>NDIS 驱动程序堆栈





### <a name="basic-stack-configuration"></a>基本堆栈配置

下图显示在 NDIS 6.0 驱动程序堆栈中的逻辑元素的基本配置。 说明了使用未指定数量的筛选器模块的驱动程序堆栈。 箭头表示堆栈的元素之间的信息流。

![说明与筛选器模块的 ndis 驱动程序堆栈的关系图](images/filterstack.png)

如前图所示，您可以通过微型端口适配器堆栈任意数量的筛选器模块。 这些模块可以是不同的筛选器驱动程序的实例和/或相同的筛选器驱动程序的多个实例。 如果微型端口驱动程序管理多个微型端口适配器，可以通过每个微型端口适配器存在单独的驱动程序堆栈。

协议驱动程序将绑定到微型端口适配器。 因此，驱动程序堆栈中的基础筛选器模块是透明的协议驱动程序。 若要获取有关基础筛选器模块的信息，协议驱动程序可以枚举驱动程序堆栈中的筛选器模块。

如果多个协议驱动程序绑定到的微型端口适配器，筛选器模块均适用于这两个协议驱动程序。 根据绑定，NDIS 将请求路由到正确的协议驱动程序。

### <a href="" id="ndis-6-0-stack-with-intermediate-driver"></a>NDIS 6.0 通过中间驱动程序堆栈

下图显示了中间驱动程序与的 NDIS 6.0 驱动程序堆栈。

![说明中间驱动程序与的 ndis 驱动程序堆栈的关系图](images/imstack.png)

如果在驱动程序堆栈中包含的 NDIS 中间驱动程序，堆栈是实质上是两个堆栈： 逐一。

中间驱动程序的虚拟微型端口用于微型端口适配器上部的堆栈，而中间驱动程序的协议 edge 提供较低的堆栈的协议绑定。

虚拟微型端口具有相同的状态与其他任何微型端口适配器。 微型端口适配器状态详细信息，请参阅[微型端口驱动程序的适配器状态](adapter-states-of-a-miniport-driver.md)。

协议缘中间驱动程序应实现作为协议驱动程序相同的绑定状态。 有关绑定状态的详细信息，请参阅[协议驱动程序的绑定状态](binding-states-of-a-protocol-driver.md)。

## <a name="related-topics"></a>相关主题


[适配器状态的微型端口驱动程序](adapter-states-of-a-miniport-driver.md)

[绑定协议驱动程序的状态](binding-states-of-a-protocol-driver.md)

[驱动程序堆栈管理](driver-stack-management.md)

[NDIS 筛选器驱动程序](ndis-filter-drivers.md)

[中间的 NDIS 驱动程序](ndis-intermediate-drivers.md)

[NDIS 微型端口驱动程序](ndis-miniport-drivers2.md)

[协议的 NDIS 驱动程序](ndis-protocol-drivers2.md)

 

 






