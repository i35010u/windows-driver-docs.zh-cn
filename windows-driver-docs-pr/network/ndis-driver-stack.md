---
title: NDIS 驱动程序堆栈
description: NDIS 驱动程序堆栈
keywords:
- 驱动程序堆栈 WDK 网络，NDIS 基本配置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0d63d4941d2543bc62bd14f34e3132f33a5289a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798039"
---
# <a name="ndis-driver-stack"></a>NDIS 驱动程序堆栈





### <a name="basic-stack-configuration"></a>基本堆栈配置

下图显示了 NDIS 6.0 驱动程序堆栈中逻辑元素的基本配置。 此图说明了具有未指定的筛选器模块数的驱动程序堆栈。 箭头表示堆栈中的元素之间的信息流。

![阐释带有筛选器模块的 ndis 驱动程序堆栈的关系图](images/filterstack.png)

如上图所示，可以通过微型端口适配器堆栈任意数量的筛选器模块。 这些模块可以是不同筛选器驱动程序的实例，也可以是同一筛选器驱动程序的多个实例。 如果微型端口驱动程序管理多个微型端口适配器，则可以在每个微型端口适配器上存在单独的驱动程序堆栈。

协议驱动程序绑定到微型端口适配器。 因此，驱动程序堆栈中的底层筛选器模块对协议驱动程序是透明的。 若要获取有关基础筛选器模块的信息，协议驱动程序可以枚举驱动程序堆栈中的筛选器模块。

如果有多个协议驱动程序绑定到微型端口适配器，这两个协议驱动程序的筛选器模块都是相同的。 根据绑定，NDIS 将请求路由到正确的协议驱动程序。

### <a name="ndis-60-stack-with-intermediate-driver"></a><a href="" id="ndis-6-0-stack-with-intermediate-driver"></a>带有中间驱动程序的 NDIS 6.0 堆栈

下图显示了带有中间驱动程序的 NDIS 6.0 驱动程序堆栈。

![阐释带有中间驱动程序的 ndis 驱动程序堆栈的关系图](images/imstack.png)

如果将 NDIS 中间驱动程序包含在驱动程序堆栈中，则堆栈实质上是两个堆栈：一个位于另一个堆栈上。

中间驱动程序的虚拟小型端口为上层堆栈提供微型端口适配器，而中间驱动程序的协议边缘为较低堆栈提供协议绑定。

虚拟微型端口具有与任何其他微型端口适配器相同的状态。 有关微型端口适配器状态的详细信息，请参阅多 [端口驱动程序的适配器状态](adapter-states-of-a-miniport-driver.md)。

中间驱动程序的协议边缘应该实现与协议驱动程序相同的绑定状态。 有关绑定状态的详细信息，请参阅 [绑定状态的协议驱动程序](binding-states-of-a-protocol-driver.md)。

## <a name="related-topics"></a>相关主题


[微型端口驱动程序的适配器状态](adapter-states-of-a-miniport-driver.md)

[协议驱动程序的绑定状态](binding-states-of-a-protocol-driver.md)

[驱动程序堆栈管理](driver-stack-management.md)

[NDIS 筛选器驱动程序](ndis-filter-drivers.md)

[NDIS 中间驱动程序](ndis-intermediate-drivers.md)

[NDIS 微型端口驱动程序](ndis-miniport-drivers2.md)

[NDIS 协议驱动程序](ndis-protocol-drivers2.md)

 

 






