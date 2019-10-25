---
title: 在中间驱动程序中响应设置和查询请求
description: 在中间驱动程序中响应设置和查询请求
ms.assetid: ccc99542-4a36-4bf9-8a19-4e7d385399da
keywords:
- 查询操作 WDK NDIS 中间
- 设置操作 WDK NDIS 中间
- 取消 OID 请求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e261dc3851521c62873fb4c38e51ab63fe5974b4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842018"
---
# <a name="responding-to-sets-and-queries-in-an-intermediate-driver"></a>在中间驱动程序中响应设置和查询请求





因为 NDIS 中间驱动程序绑定到过量的 NDIS 驱动程序，所以它还可以从其[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)函数接收查询和集。 在某些情况下，中间驱动程序只会将此类请求传递到基础微型端口驱动程序。 否则，可以对这些查询进行响应，并将其设置为适用于在其上边缘导出的介质。 请注意，中间驱动程序必须始终通过从从属 NDIS 驱动程序收到的任何 OID\_PNP\_*Xxx*请求传递到基础微型端口驱动程序。 NDIS 6.0 中间驱动程序还可以取消 OID 请求。

若要将请求转发到底层驱动程序，NDIS 中间驱动程序会调用[**NdisAllocateCloneOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatecloneoidrequest)来分配克隆的[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构。 驱动程序调用[**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)函数以发送请求。 请求完成后，驱动程序必须调用[**NdisFreeCloneOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreecloneoidrequest)函数，以\_请求结构释放\_OID 的 NDIS。

若要取消 OID 请求，请调用[**NdisCancelOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscanceloidrequest)函数。

通常，中间驱动程序接收到的常规 Oid 与中间驱动程序发送到基础微型端口驱动程序的常规 Oid 相同或相似。 中间驱动程序接收的特定于介质的 Oid 是过量驱动程序所需的介质类型。

如果中间驱动程序自行处理 OID 的设置，而不是将设置请求传递到基础微型端口，则应验证要设置的值。 如果中间驱动程序确定要设置的值超出界限，则它应使集请求失败。

**请注意**  如果中间驱动程序修改了向下移动到基础微型端口驱动程序的 tcp 网络数据的内容，以便无法对网络数据执行 tcp 卸载功能，则中间驱动程序应响应[OID\_TCP\_卸载\_当前\_配置](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)查询，状态为 NDIS\_状态\_不支持\_，而不是向下传递请求到底层微型端口。

 

有关在中间驱动程序中响应集和查询的其他信息，请参阅[获取并设置微型端口驱动程序信息和 WMI 对 WMI 的支持](obtaining-and-setting-miniport-driver-information-and-ndis-support-for.md)。

 

 





