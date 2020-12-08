---
title: 设置无连接微型端口驱动程序的信息
description: 设置无连接微型端口驱动程序的信息
keywords:
- 无连接驱动程序 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9615e356235fcfc823483c64a73d7da1ea53c807
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795881"
---
# <a name="setting-information-for-a-connectionless-miniport-driver"></a>设置无连接微型端口驱动程序的信息





若要设置无连接微型端口驱动程序维护的 OID，绑定协议将调用 [**NdisOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest) ，并传递 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request) 结构，该结构指定正在查询的对象 (OID) ，并指向包含应设置对象的值的缓冲区。 对 **NdisOidRequest** 的调用会使 NDIS 调用微型端口驱动程序的 [*MiniportOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request) 函数，该函数将对象设置为提供的值。

对 *MiniportOidRequest* 的调用可同步或异步完成。 若要异步完成调用，微型端口驱动程序将调用 [**NdisMOidRequestComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)。 下图说明了在每个绑定)  (的无连接微型端口驱动程序中的设置信息。

![说明每个绑定 (的无连接微型端口驱动程序中的设置信息的关系图) ](images/fig5-4.png)

 

