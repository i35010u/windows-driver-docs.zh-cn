---
title: 释放 NDIS 端口
description: 释放 NDIS 端口
ms.assetid: ae7b608d-6105-4fdc-b805-0f0101d7c218
keywords:
- 端口 WDK NDIS，释放
- NDIS 端口 WDK，释放
- 释放 NDIS 端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9ca18ad48915b38d796fd6d210243630592ef6b
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212467"
---
# <a name="freeing-an-ndis-port"></a>释放 NDIS 端口





微型端口驱动程序必须释放它在其[*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数中为微型端口适配器[分配](allocating-an-ndis-port.md)的所有 NDIS 端口。 除了下面所述的两个情况外，它还可以通过调用 [**NdisMFreePort**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreeport)来释放端口。

在这些情况下，微型端口驱动程序必须释放所有已分配的端口：

-   如果驱动程序的 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数失败，则必须释放所有已分配的端口。
-   如果某个微型端口适配器已停止，则驱动程序的 [*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt) 函数必须释放所有已分配的端口。

在这些情况下，微型端口驱动程序不能简单地调用 [**NdisMFreePort**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreeport) ：

-   如果端口是默认端口，NDIS 会自动将其释放，因此微型端口驱动程序不得释放它。 如果尝试释放 [默认端口](default-ndis-port.md)， [**NdisMFreePort**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreeport) 将返回 "NDIS \_ 状态 \_ 无效 \_ 端口错误" 错误。
-   如果端口处于活动状态，则微型端口驱动程序需要在调用 [**NdisMFreePort**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreeport)之前停用它。

## <a name="related-topics"></a>相关主题


[分配 NDIS 端口](allocating-an-ndis-port.md)

[停用 NDIS 端口](deactivating-an-ndis-port.md)

[默认 NDIS 端口](default-ndis-port.md)

 

