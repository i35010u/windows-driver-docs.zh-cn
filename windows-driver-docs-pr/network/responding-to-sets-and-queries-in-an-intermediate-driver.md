---
title: 在中间驱动程序中响应设置和查询请求
description: 在中间驱动程序中响应设置和查询请求
keywords:
- 查询操作 WDK NDIS 中间
- 设置操作 WDK NDIS 中间
- 取消 OID 请求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe092dc52743d6ba38ea050e24d200a60eb5fbdc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836703"
---
# <a name="responding-to-sets-and-queries-in-an-intermediate-driver"></a>在中间驱动程序中响应设置和查询请求





因为 NDIS 中间驱动程序绑定到过量的 NDIS 驱动程序，所以它还可以从其 [*MiniportOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request) 函数接收查询和集。 在某些情况下，中间驱动程序只会将此类请求传递到基础微型端口驱动程序。 否则，可以对这些查询进行响应，并将其设置为适用于在其上边缘导出的介质。 请注意，中间驱动程序必须始终将它从占用的 NDIS 驱动程序收到的任何 OID \_ PNP \_ *Xxx* 请求传递到基础微型端口驱动程序。 NDIS 6.0 中间驱动程序还可以取消 OID 请求。

若要将请求转发到底层驱动程序，NDIS 中间驱动程序会调用 [**NdisAllocateCloneOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatecloneoidrequest) 来分配克隆的 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request) 结构。 驱动程序调用 [**NdisOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest) 函数以发送请求。 请求完成后，驱动程序必须调用 [**NdisFreeCloneOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreecloneoidrequest) 函数以释放 NDIS \_ OID \_ 请求结构。

若要取消 OID 请求，请调用 [**NdisCancelOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscanceloidrequest) 函数。

通常，中间驱动程序接收到的常规 Oid 与中间驱动程序发送到基础微型端口驱动程序的常规 Oid 相同或相似。 中间驱动程序接收的特定于介质的 Oid 是过量驱动程序所需的介质类型。

如果中间驱动程序自行处理 OID 的设置，而不是将设置请求传递到基础微型端口，则应验证要设置的值。 如果中间驱动程序确定要设置的值超出界限，则它应使集请求失败。

**注意**  如果中间驱动程序修改了 TCP 网络数据的内容，这些数据会向下传递到基础微型端口驱动程序，以便无法对网络数据执行 TCP 卸载功能，则中间驱动程序应使用不受支持的 "NDIS 状态" 状态的 "不支持" 状态，而不是向下传递请求来响应 [OID \_ TCP \_ 卸载 \_ 当前 \_ 配置](./oid-tcp-offload-current-config.md) 查询 \_ \_ \_ 。

 

有关在中间驱动程序中响应集和查询的其他信息，请参阅 [获取并设置微型端口驱动程序信息和 WMI 对 WMI 的支持](ndis-management-information-and-oids.md)。

 

