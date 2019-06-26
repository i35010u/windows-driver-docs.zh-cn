---
title: 在中间驱动程序中响应设置和查询请求
description: 在中间驱动程序中响应设置和查询请求
ms.assetid: ccc99542-4a36-4bf9-8a19-4e7d385399da
keywords:
- 查询操作 WDK NDIS 中间
- 集运算 WDK NDIS 中间
- 正在取消 OID 请求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a3a355277ba6af9617580361b794f51e9065f7c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378641"
---
# <a name="responding-to-sets-and-queries-in-an-intermediate-driver"></a>在中间驱动程序中响应设置和查询请求





因为 NDIS 中间驱动程序绑定到基础的 NDIS 驱动程序，它还可以接收查询和集从其[ *MiniportOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)函数。 在某些情况下，中间驱动程序只需将通过此类请求传递给基础的微型端口驱动程序。 否则为它可以响应这些查询，并设置到它在其上边缘将导出的介质根据需要。 请注意，中间驱动程序必须始终通过任何 OID\_PNP\_*Xxx*从过量的 NDIS 驱动程序为基础的微型端口驱动程序收到的请求。 NDIS 6.0 中间驱动程序还可以取消 OID 请求。

要将转发到基础驱动程序的请求，NDIS 中间层驱动程序调用[ **NdisAllocateCloneOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatecloneoidrequest)来分配对克隆[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构。 驱动程序调用[ **NdisOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisoidrequest)函数来发送请求。 请求完成后，该驱动程序必须调用[ **NdisFreeCloneOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreecloneoidrequest)函数来释放 NDIS\_OID\_请求结构。

若要取消的 OID 请求，请调用[ **NdisCancelOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscanceloidrequest)函数。

通常情况下，中间驱动程序将收到的常规 Oid 是相同或类似于中间驱动程序将发送到基础微型端口驱动程序。 中间的驱动程序将收到的特定于中等的 Oid 是基础驱动程序需要对介质的类型。

如果中间驱动程序本身进程 OID 的设置，而不是将 set 请求传递给基础的微型端口，应验证要设置的值。 如果中间驱动程序确定要设置的值超出界限，则应失败集请求。

**请注意**  如果中间驱动程序修改用于将其转发到基础的微型端口驱动程序，以便 TCP 卸载 TCP 网络数据的内容不能在函数执行上的网络数据，中间驱动程序应响应[OID\_TCP\_卸载\_当前\_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)查询状态为 NDIS\_状态\_不\_支持而不是将请求传递到基础微型端口。

 

有关对组和中间驱动程序中的查询响应的其他信息，请参阅[获取和设置微型端口驱动程序的信息和 NDIS 支持 WMI](obtaining-and-setting-miniport-driver-information-and-ndis-support-for.md)。

 

 





