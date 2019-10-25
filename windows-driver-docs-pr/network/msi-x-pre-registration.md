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
ms.openlocfilehash: c6af56278c3d771d822db1e9f61cb3f23f77f684
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844214"
---
# <a name="msi-x-pre-registration"></a>MSI-X 预先注册





若要支持更改 MSI X 的中断相关性或删除消息中断资源，微型端口驱动程序必须建立资源需求筛选器函数。 此预注册步骤发生在 NDIS 调用[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数之前。

若要建立资源需求筛选器函数，微型端口驱动程序必须提供[*MiniportSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)函数。 当微型端口驱动程序从[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程调用[**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)函数时，驱动程序会在 [**NDIS\_微型端口\_驱动程序中传递 MiniportSetOptions 的入口点\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics)结构。 NDIS 在**NdisMRegisterMiniportDriver**的上下文中调用*MiniportSetOptions*函数。

在*MiniportSetOptions*中，微型端口驱动程序调用[**NdisSetOptionalHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)函数并指定[**NDIS\_微型端口\_PNP\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_pnp_characteristics)结构。 此结构定义了[*MiniportAddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_add_device)、 [*MiniportRemoveDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_remove_device)、 [*MiniportStartDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pnp_irp)和[*MiniportFilterResourceRequirements*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pnp_irp)函数的入口点。

当 NDIS 接收到来自即插即用（PnP）管理器的添加设备请求时，NDIS 将调用微型端口驱动程序的*MiniportAddDevice*函数。 NDIS 传递到*MiniportAdapterHandle*参数中的*MiniportAddDevice*的句柄是 Ndis 稍后传递到[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数的句柄。

在[*MiniportAddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_add_device)中，驱动程序初始化[**NDIS\_微型端口\_添加\_设备\_注册\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_add_device_registration_attributes)结构，并将此结构传递给[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)才能. NDIS\_微型端口\_添加\_设备\_注册\_属性结构包含**MiniportAddDeviceContext**成员，该成员是设备的微型端口驱动程序分配上下文区域的句柄。 稍后，NDIS 为[*MiniportRemoveDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_remove_device)、 [*MiniportFilterResourceRequirements*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pnp_irp)、 [*MiniportStartDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pnp_irp)和[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数提供了此上下文句柄。 对于*MiniportInitializeEx*，上下文句柄传递到 NDIS\_微型端口的**MiniportAddDeviceContext**成员中， [ **\_INIT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_init_parameters)结构， *MiniportInitParameters*参数指向。

在 NDIS 调用[*MiniportAddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_add_device)和*MiniportAddDevice*返回 NDIS\_状态\_SUCCESS 后，ndis 会在每次收到 IRP\_MN 时调用*MiniportFilterResourceRequirements*函数[ **\_筛选器\_资源\_需求**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-filter-resource-requirements)i/o 请求数据包（IRP）。 *MiniportFilterResourceRequirements*可以更改每个 MSI X 消息的中断相关性，添加消息中断资源，或删除消息中断资源（如果驱动程序将在[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数。 有关建立中断关联策略的详细信息，请参阅 " [MSI-X 资源筛选](msi-x-resource-filtering.md)"。

当 NDIS 接收来自 PnP 管理器的删除设备请求时，NDIS 会调用微型端口驱动程序的[*MiniportRemoveDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_remove_device)函数。 *MiniportRemoveDevice*函数应撤消[*MiniportAddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_add_device)函数执行的操作。

 

 





