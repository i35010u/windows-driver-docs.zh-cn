---
title: MSI-X 预先注册
description: MSI-X 预先注册
ms.assetid: 93a09ebd-8a50-4c96-a926-54bb4686a618
keywords:
- MSI X WDK 网络、 资源要求 filter 函数
- 消息信号中断 WDK 网络资源要求筛选器函数
- Msi WDK 网络资源要求筛选器函数
- 资源要求 filter 函数 WDK net
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f5451d7353d49b014868525c197ab30d623af71
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364052"
---
# <a name="msi-x-pre-registration"></a>MSI-X 预先注册





若要支持不断变化的 MSI X 的中断关联或删除消息中断资源，微型端口驱动程序必须建立资源要求筛选器函数。 在 NDIS 调用之前发生的此预注册步骤[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数。

若要建立资源要求筛选器函数，微型端口驱动程序必须提供[ *MiniportSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)函数。 当微型端口驱动程序调用[ **NdisMRegisterMiniportDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver)函数从[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)例程，则驱动程序为传递的入口点*MiniportSetOptions*中[ **NDIS\_微型端口\_驱动程序\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_driver_characteristics)结构。 NDIS 调用*MiniportSetOptions*的上下文中的函数**NdisMRegisterMiniportDriver**。

从*MiniportSetOptions*，微型端口驱动程序调用[ **NdisSetOptionalHandlers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissetoptionalhandlers)函数，并指定[ **NDIS\_微型端口\_PNP\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_pnp_characteristics)结构。 此结构定义的入口点[ *MiniportAddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_add_device)， [ *MiniportRemoveDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_remove_device)， [ *MiniportStartDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_pnp_irp)，并[ *MiniportFilterResourceRequirements* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_pnp_irp)函数。

NDIS 时 NDIS 接收来自插即用 (PnP) 管理器的添加设备请求，调用微型端口驱动程序*MiniportAddDevice*函数。 NDIS 将传递给的句柄*MiniportAddDevice*中*MiniportAdapterHandle*参数是 NDIS 更高版本将传递给句柄[ *MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数。

在中[ *MiniportAddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_add_device)，该驱动程序初始化[ **NDIS\_微型端口\_添加\_设备\_注册\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_add_device_registration_attributes)结构，并将传递到此结构[ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)函数。 NDIS\_微型端口\_添加\_设备\_注册\_特性结构包含**MiniportAddDeviceContext**是微型端口的句柄的成员设备的驱动程序分配的上下文区域。 NDIS 更高版本提供了此上下文句柄[ *MiniportRemoveDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_remove_device)， [ *MiniportFilterResourceRequirements*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_pnp_irp)， [*MiniportStartDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_pnp_irp)，和[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数。 有关*MiniportInitializeEx*，在传递上下文句柄**MiniportAddDeviceContext**的成员[ **NDIS\_微型端口\_INIT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_init_parameters)结构的*MiniportInitParameters*参数指向。

在 NDIS 后调用[ *MiniportAddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_add_device)并*MiniportAddDevice*返回 NDIS\_状态\_成功后，NDIS 调用*MiniportFilterResourceRequirements*函数，每当它收到[ **IRP\_MN\_筛选器\_资源\_要求** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-filter-resource-requirements) I/O 请求数据包 (IRP)。 *MiniportFilterResourceRequirements*可以更改每个 MSI X 消息中断关联、 添加消息中断资源，或删除消息中断资源，如果驱动程序将注册，以便在基于行的中断[*MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数。 有关建立中断关联策略的详细信息，请参阅[MSI X 资源筛选](msi-x-resource-filtering.md)。

NDIS NDIS 收到删除设备请求时从 PnP 管理器，当调用微型端口驱动程序的[ *MiniportRemoveDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_remove_device)函数。 *MiniportRemoveDevice*函数应撤消操作的[ *MiniportAddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_add_device)函数执行。

 

 





