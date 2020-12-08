---
title: 设置微型端口驱动程序信息的场合
description: 设置微型端口驱动程序信息的场合
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95589ae1a67c9a90c554d8ebf219e1f3fb74d469
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813647"
---
# <a name="occasions-for-setting-miniport-driver-information"></a>设置微型端口驱动程序信息的场合





无连接微型端口驱动程序中的 [*MiniportOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request) 函数和面向连接的微型端口驱动程序中的 [**MiniportCoOidRequest**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request) 函数是在初始化过程中调用的。 还可以调用这些函数：

-   在硬件重置过程中，

-   如果协议调用 [**NdisCloseAdapterEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscloseadapterex)。

在 [硬件重置操作](hardware-reset.md)期间调用 *MiniportOidRequest* 或 *MiniportCoOidRequest* 。 在这种情况下，将调用 *MiniportOidRequest* 或 *MiniportCoOidRequest* ，以将微型端口驱动程序的初始状态重置为其地址。

当某个微型端口驱动程序的 NIC 被协议的 [**NdisCloseAdapterEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscloseadapterex)调用关闭时，NDIS 将调用 *MiniportOidRequest* 或 *MiniportCoOidRequest* 。 这种微型端口驱动程序将被请求更新其寻址信息。

 

