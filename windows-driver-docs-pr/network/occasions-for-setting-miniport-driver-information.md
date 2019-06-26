---
title: 设置微型端口驱动程序信息的场合
description: 设置微型端口驱动程序信息的场合
ms.assetid: 46834d76-e1b9-440c-af18-a4b564d1a76e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab733cf4cb30b9e25ecb8a13e77f6a4c7adad042
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368507"
---
# <a name="occasions-for-setting-miniport-driver-information"></a>设置微型端口驱动程序信息的场合





[ *MiniportOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)无连接的微型端口驱动程序中的函数和[ **MiniportCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_oid_request)中的函数在初始化期间调用的面向连接的微型端口驱动程序。 也可以调用这些函数：

-   在硬件重置，过程

-   如果协议调用[ **NdisCloseAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscloseadapterex)。

*MiniportOidRequest*或*MiniportCoOidRequest*期间调用[硬件重置操作](hardware-reset.md)。 在这种情况下， *MiniportOidRequest*或*MiniportCoOidRequest*调用重置为其初始状态相对于其地址的微型端口驱动程序。

NDIS 调用*MiniportOidRequest*或*MiniportCoOidRequest*的协议时关闭微型端口驱动程序的 NIC [ **NdisCloseAdapterEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscloseadapterex)调用。 这样的微型端口驱动程序将请求来更新其寻址信息。

 

 





