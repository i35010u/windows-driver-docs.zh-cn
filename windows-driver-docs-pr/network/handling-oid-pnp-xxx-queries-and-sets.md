---
title: 处理 OID_PNP_Xxx 查询和设置请求
description: 处理 OID_PNP_Xxx 查询和设置请求
keywords:
- OID_PNP_Xxx
- 查询操作 WDK NDIS 中间
- 设置操作 WDK NDIS 中间
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5512c1a11b7b36036bd8485aa57ba3964c4bf6f7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790489"
---
# <a name="handling-oid_pnp_xxx-queries-and-sets"></a>处理 OID \_ PNP \_ Xxx 查询和集





中间驱动程序的虚拟微型端口必须导出 [*MiniportOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request) 函数。 当绑定到中间驱动程序的虚拟小型端口的过量驱动程序调用 [**NdisOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)来查询或设置 (OID Xxx) 的信息对象时，NDIS 调用中间驱动程序的 *MiniportOidRequest* 函数 \_ *Xxx* 。 NDIS 还可以代表自己调用 *MiniportOidRequest* 。 有关对信息对象的集和查询的微型端口驱动程序处理的详细信息，请参阅 [获取并设置微型端口驱动程序信息和对 WMI 的 NDIS 支持](ndis-management-information-and-oids.md)。

中间驱动程序应保留有关其在 [*ProtocolBindAdapterEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex) 函数中收到的基础微型端口适配器功能的信息。 如果微型端口适配器不支持电源管理，NDIS 会将 [**ndis \_ 绑定 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)的 **PowerManagementCapabilities** 成员设置为 **NULL**。

中间驱动程序可以查询或设置 \_ 由基础微型端口驱动程序维护的 OID *Xxx* 。 如果中间驱动程序具有不连接的下边缘) ，则此方法将使用 **NdisOidRequest** (，如果中间驱动程序具有面向连接的下边缘) ，则使用 [**NdisCoOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest) (。

中间驱动程序应处理查询和设置，如下所示：

-   [OID \_ PNP \_ 功能](./oid-pnp-capabilities.md)

    为了响应此 OID 查询，中间驱动程序必须报告基础物理微型端口适配器的 PnP 能力。 请注意，物理设备的微型端口适配器不会收到此 OID 查询。

    中间驱动程序接收绑定参数中基础微型端口适配器的 PnP 功能。 它应将其传递到适用于中间驱动程序预期用途的过量驱动程序。 中间驱动程序和微型端口驱动程序在微型端口适配器属性中报告 PnP 功能。 中间驱动程序不会 \_ \_ 向基础微型端口驱动程序发出 OID PNP 功能请求。 如果基础微型端口适配器支持电源管理，则在 \_ \_ \_ 虚拟微型端口属性的 NDIS PM 唤醒 \_ 功能结构中，中间驱动程序必须为每个唤醒功能指定设备电源状态 **NdisDeviceStateUnspecified** ：

    -   MinMagicPacketWakeUp
    -   MinPatternWakeUp
    -   MinLinkChangeWakeUp

    此类设置表示中间驱动程序支持电源管理，但无法唤醒系统。

-   [OID \_PNP \_ 查询 \_ 电源](./oid-pnp-query-power.md) 和 [OID \_ PNP \_ 设置 \_ 电源](./oid-pnp-set-power.md)

    中间驱动程序必须始终将 NDIS \_ 状态 \_ 成功返回到 oid \_ pnp \_ 查询 \_ 功能或一组 oid \_ pnp \_ 集 \_ 功能的查询。 中间驱动程序决不能将这些 OID 请求传播到基础微型端口驱动程序。

-   "唤醒 Oid"

    如果基础 NIC 支持电源管理，则中间驱动程序必须通过调用 **NdisOidRequest** 或 **NdisCoOidRequest**) 与 \_ 唤醒事件相关的以下 OID PNP \_ *Xxx* ，将中间驱动程序传递到基础微型端口驱动程序 (：

    [OID \_ PNP \_ 启用 \_ 唤醒 \_](./oid-pnp-enable-wake-up.md)

    [OID \_ PNP \_ 添加 \_ 唤醒 \_ \_ 模式](./oid-pnp-add-wake-up-pattern.md)

    [OID \_ PNP \_ 删除 \_ 唤醒 \_ \_ 模式](./oid-pnp-remove-wake-up-pattern.md)

    [OID \_ PNP \_ 唤醒 \_ \_ 模式 \_ 列表](./oid-pnp-wake-up-pattern-list.md)

    [OID \_ PNP \_ 唤醒 \_ \_ 错误](./oid-pnp-wake-up-error.md)

    [OID \_ PNP \_ 唤醒 \_ 正常 \_](./oid-pnp-wake-up-ok.md)

中间驱动程序还必须将基础微型端口驱动程序的响应传播到过量协议驱动程序。

如果基础微型端口适配器不能识别电源，则微型端口驱动程序会将 [**ndis \_ 微型端口 \_ 适配器 \_ 常规 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)的 **PowerManagementCapabilities** 成员设置为 **Null** ，ndis 会将 [**ndis \_ 绑定 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)的 **PowerManagementCapabilities** 成员设置为 **null**。

如果基础微型端口适配器不支持电源管理，中间驱动程序应返回 NDIS 状态， \_ \_ \_ 以响应查询或这些 oid 集。

 

