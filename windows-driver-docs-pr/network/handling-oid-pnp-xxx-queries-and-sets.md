---
title: 处理 OID_PNP_Xxx 查询和设置请求
description: 处理 OID_PNP_Xxx 查询和设置请求
ms.assetid: 2d5db7fb-2a27-4359-9d75-35939e72de69
keywords:
- OID_PNP_Xxx
- 查询操作 WDK NDIS 中间
- 设置操作 WDK NDIS 中间
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ee414f25f6a7efa668f15360842eee823fd5d50
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842578"
---
# <a name="handling-oid_pnp_xxx-queries-and-sets"></a>处理 OID\_PNP\_Xxx 查询和集





中间驱动程序的虚拟微型端口必须导出[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)函数。 当绑定到中间驱动程序的虚拟小型端口的过量驱动程序调用[**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)来查询或设置信息对象（OID\_*Xxx*）时，NDIS 调用中间驱动程序的*MiniportOidRequest*函数。 NDIS 还可以代表自己调用*MiniportOidRequest* 。 有关对信息对象的集和查询的微型端口驱动程序处理的详细信息，请参阅[获取并设置微型端口驱动程序信息和对 WMI 的 NDIS 支持](obtaining-and-setting-miniport-driver-information-and-ndis-support-for.md)。

中间驱动程序应保留有关其在[*ProtocolBindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)函数中收到的基础微型端口适配器功能的信息。 如果微型端口适配器不支持电源管理，NDIS 会将 Ndis 的**PowerManagementCapabilities**成员设置[ **\_将\_参数绑定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)到**NULL**。

中间驱动程序可以查询或设置由基础微型端口驱动程序维护的 OID\_*Xxx* 。 它使用**NdisOidRequest**来执行此项（如果中间驱动程序具有无连接的下边缘）或使用[**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)（如果中间驱动程序具有面向连接的下边缘）。

中间驱动程序应处理查询和设置，如下所示：

-   [OID\_PNP\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-capabilities)

    为了响应此 OID 查询，中间驱动程序必须报告基础物理微型端口适配器的 PnP 能力。 请注意，物理设备的微型端口适配器不会收到此 OID 查询。

    中间驱动程序接收绑定参数中基础微型端口适配器的 PnP 功能。 它应将其传递到适用于中间驱动程序预期用途的过量驱动程序。 中间驱动程序和微型端口驱动程序在微型端口适配器属性中报告 PnP 功能。 中间驱动程序不会向基础微型端口驱动程序发出 OID\_PNP\_功能请求。 如果基础微型端口适配器支持电源管理，请在 NDIS\_PM\_唤醒\_"虚拟" 微型端口属性中的 "\_功能" 结构，中间驱动程序必须将设备电源状态**指定为**每个唤醒功能的 NdisDeviceStateUnspecified：

    -   MinMagicPacketWakeUp
    -   MinPatternWakeUp
    -   MinLinkChangeWakeUp

    此类设置表示中间驱动程序支持电源管理，但无法唤醒系统。

-   [Oid\_pnp\_QUERY\_电源](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-query-power)和[OID\_PNP\_\_POWER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)

    中间驱动程序必须始终\_状态返回 NDIS 状态\_成功\_PNP\_查询\_电源或一组 OID\_PNP\_\_。 中间驱动程序决不能将这些 OID 请求传播到基础微型端口驱动程序。

-   "唤醒 Oid"

    如果基础 NIC 支持电源管理，中间驱动程序必须通过调用 NdisOidRequest 或 NdisCoOidRequest 传递到基础微型端口驱动程序（通过调用或）以下 OID\_PNP\_*Xxx*关联到唤醒事件：

    [OID\_PNP\_启用\_唤醒\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-enable-wake-up)

    [OID\_PNP\_添加\_唤醒\_向上\_模式](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-add-wake-up-pattern)

    [OID\_PNP\_删除\_唤醒\_向上\_模式](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-remove-wake-up-pattern)

    [OID\_PNP\_唤醒\_\_模式\_列表](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-wake-up-pattern-list)

    [OID\_PNP\_唤醒\_\_错误](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-wake-up-error)

    [OID\_PNP\_唤醒\_\_正常](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-wake-up-ok)

中间驱动程序还必须将基础微型端口驱动程序的响应传播到过量协议驱动程序。

如果基础微型端口适配器不支持电源管理，则微型端口驱动程序会将 NDIS\_微型端口的**PowerManagementCapabilities**成员设置[ **\_适配器\_常规\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)设置为**NULL** ，NDIS 将[**ndis\_绑定\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)的**PowerManagementCapabilities**成员设置为**NULL**。

如果基础微型端口适配器不支持电源管理，中间驱动程序应将 NDIS\_状态返回\_不\_支持，以响应查询或这些 Oid 集。

 

 





