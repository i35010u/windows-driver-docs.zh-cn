---
title: 确定网络适配器的 NVGRE 任务卸载功能
description: 本部分介绍如何确定网络适配器的 NVGRE 任务卸载功能
ms.assetid: 1F9C5E7D-5488-47C1-BEDC-D7C640F57511
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b3d5c65096ff8d3915181024f845591022ee038
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565214"
---
# <a name="determining-the-nvgre-task-offload-capabilities-of-a-network-adapter"></a>确定网络适配器的 NVGRE 任务卸载功能


支持的微型端口驱动程序[网络虚拟化使用通用路由封装 (NVGRE) 任务卸载](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)报告通过此功能[ **NDIS\_卸载**](https://msdn.microsoft.com/library/windows/hardware/ff566599)结构，其[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数将传递给[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672).

## <a name="reporting-nvgre-task-offload-capability"></a>报告 NVGRE 任务卸载功能


在中[ **NDIS\_卸载**](https://msdn.microsoft.com/library/windows/hardware/ff566599)结构**标头**成员必须按如下所示设置：

-   **修订**成员必须设置为**NDIS\_卸载\_修订\_3**。
-   **大小**成员必须设置为**NDIS\_SIZEOF\_NDIS\_卸载\_修订\_3**。

若要报告其支持 NVGRE 任务卸载，微型端口驱动程序设置以下中的成员[ **NDIS\_封装\_数据包\_任务\_卸载**](https://msdn.microsoft.com/library/windows/hardware/jj991956)结构，它存储在**EncapsulatedPacketTaskOffloadGre**的成员[ **NDIS\_卸载**](https://msdn.microsoft.com/library/windows/hardware/ff566599)结构微型端口驱动程序[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数将传递给[ **NdisMSetMiniportAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff563672):

-   设置**MaxHeaderSizeSupported**成员添加到的最大标头大小从开头到开头的内部 TCP 或 UDP 负载 （TCP 或 UDP 内部标头的最后一个字节） 的 NIC 必须支持所有这些任务数据包将卸载。 协议驱动程序应不卸载其组合的封装标头超过此大小的数据包的处理。

    **请注意**  256 个字节是一个很好的默认值，应涵盖所有可能情况。

     

-   设置的其他成员来指示哪些类型的任务卸载封装的数据包微型端口驱动程序支持。 可以为这些成员中设置的标志的列表，请参阅备注部分[ **NDIS\_封装\_数据包\_任务\_卸载**](https://msdn.microsoft.com/library/windows/hardware/jj991956)。

## <a name="querying-nvgre-task-offload-capability"></a>查询 NVGRE 任务卸载功能


若要确定微型端口驱动程序是否支持 NVGRE 任务卸载，协议和筛选器驱动程序可以发出[OID\_TCP\_卸载\_硬件\_功能](https://msdn.microsoft.com/library/windows/hardware/ff569806)OID 请求它将返回[ **NDIS\_卸载**](https://msdn.microsoft.com/library/windows/hardware/ff566599)结构。

**请注意**  若要确定微型端口驱动程序的 NVGRE 功能当前是否已启用，请使用[OID\_TCP\_卸载\_当前\_配置](https://msdn.microsoft.com/library/windows/hardware/ff569805)OID 请求中所述[查询和更改 NVGRE 任务卸载状态](querying-and-changing-nvgre-task-offload-state.md)。

 

**请注意**  若要启用或禁用微型端口驱动程序的 NVGRE 功能，使用[OID\_TCP\_卸载\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569807)OID 请求中所述[查询和更改 NVGRE 任务卸载状态](querying-and-changing-nvgre-task-offload-state.md)。

 

 

 





