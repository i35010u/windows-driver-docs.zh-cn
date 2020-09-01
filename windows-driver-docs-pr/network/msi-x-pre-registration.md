---
title: MSI-X 预先注册
description: MSI-X 预先注册
ms.assetid: 93a09ebd-8a50-4c96-a926-54bb4686a618
keywords:
- MSI-X WDK 网络，资源需求筛选器函数
- 消息-已发出信号中断 WDK 网络，资源需求筛选器函数
- Msi WDK 网络，资源需求筛选器函数
- 资源需求筛选器函数 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 484b779be2c82f9d1b19226886068ff3a7b2cbdd
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218406"
---
# <a name="msi-x-pre-registration"></a>MSI-X 预先注册





若要支持更改 MSI X 的中断相关性或删除消息中断资源，微型端口驱动程序必须建立资源需求筛选器函数。 此预注册步骤发生在 NDIS 调用 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数之前。

若要建立资源需求筛选器函数，微型端口驱动程序必须提供 [*MiniportSetOptions*](/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options) 函数。 当微型端口驱动程序从[**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程调用[**NdisMRegisterMiniportDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)函数时，驱动程序会在[**NDIS \_ 微型端口 \_ 驱动程序 \_ 特征**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics)结构中传递*MiniportSetOptions*的入口点。 NDIS 在**NdisMRegisterMiniportDriver**的上下文中调用*MiniportSetOptions*函数。

在 *MiniportSetOptions*中，微型端口驱动程序调用 [**NdisSetOptionalHandlers**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers) 函数并指定一个 [**NDIS \_ 微型端口 \_ PNP \_ 特征**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_pnp_characteristics) 结构。 此结构定义了 [*MiniportAddDevice*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_add_device)、 [*MiniportRemoveDevice*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_remove_device)、 [*MiniportStartDevice*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pnp_irp)和 [*MiniportFilterResourceRequirements*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pnp_irp) 函数的入口点。

当 NDIS 从即插即用 (PnP) 管理器接收添加设备请求时，NDIS 将调用微型端口驱动程序的 *MiniportAddDevice* 函数。 NDIS 传递到*MiniportAdapterHandle*参数中的*MiniportAddDevice*的句柄是 Ndis 稍后传递到[*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数的句柄。

在 [*MiniportAddDevice*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_add_device)中，驱动程序初始化 [**NDIS \_ 微型端口 \_ 添加 \_ 设备 \_ 注册 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_add_device_registration_attributes) 结构，并将此结构传递给 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes) 函数。 NDIS \_ 微型端口 \_ 添加 \_ 设备 \_ 注册 \_ 属性结构包含 **MiniportAddDeviceContext** 成员，该成员是设备的微型端口驱动程序分配上下文区域的句柄。 稍后，NDIS 为 [*MiniportRemoveDevice*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_remove_device)、 [*MiniportFilterResourceRequirements*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pnp_irp)、 [*MiniportStartDevice*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pnp_irp)和 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数提供了此上下文句柄。 对于*MiniportInitializeEx*，上下文句柄传递到*MiniportInitParameters*参数指向的[**NDIS \_ 微型端口 \_ INIT \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_init_parameters)结构的**MiniportAddDeviceContext**成员中。

在 NDIS 调用[*MiniportAddDevice*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_add_device)和*MiniportAddDevice*返回 ndis \_ 状态 \_ SUCCESS 后，每次收到[**irp \_ MN \_ 筛选器 \_ 资源 \_ 需求**](../kernel/irp-mn-filter-resource-requirements.md))  (irp 时，ndis 都会调用*MiniportFilterResourceRequirements*函数。 如果驱动程序将在[*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数中注册基于行的中断，则*MiniportFilterResourceRequirements*可以更改每个 MSI X 消息的中断相关性，添加消息中断资源，或删除消息中断资源。 有关建立中断关联策略的详细信息，请参阅 " [MSI-X 资源筛选](msi-x-resource-filtering.md)"。

当 NDIS 接收来自 PnP 管理器的删除设备请求时，NDIS 会调用微型端口驱动程序的 [*MiniportRemoveDevice*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_remove_device) 函数。 *MiniportRemoveDevice*函数应撤消[*MiniportAddDevice*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_add_device)函数执行的操作。

 

