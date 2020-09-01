---
title: 设置微型端口驱动程序信息的场合
description: 设置微型端口驱动程序信息的场合
ms.assetid: 46834d76-e1b9-440c-af18-a4b564d1a76e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05e9f8e34fc804649b062f464beda33bd402aee2
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214654"
---
# <a name="occasions-for-setting-miniport-driver-information"></a>设置微型端口驱动程序信息的场合





无连接微型端口驱动程序中的 [*MiniportOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request) 函数和面向连接的微型端口驱动程序中的 [**MiniportCoOidRequest**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request) 函数是在初始化过程中调用的。 还可以调用这些函数：

-   在硬件重置过程中，

-   如果协议调用 [**NdisCloseAdapterEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscloseadapterex)。

在[硬件重置操作](hardware-reset.md)期间调用*MiniportOidRequest*或*MiniportCoOidRequest* 。 在这种情况下，将调用 *MiniportOidRequest* 或 *MiniportCoOidRequest* ，以将微型端口驱动程序的初始状态重置为其地址。

当某个微型端口驱动程序的 NIC 被协议的[**NdisCloseAdapterEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscloseadapterex)调用关闭时，NDIS 将调用*MiniportOidRequest*或*MiniportCoOidRequest* 。 这种微型端口驱动程序将被请求更新其寻址信息。

 

