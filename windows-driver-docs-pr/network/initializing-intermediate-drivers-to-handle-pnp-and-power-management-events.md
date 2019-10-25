---
title: 处理中间驱动程序中的 PnP 和电源管理事件
description: 初始化中间驱动程序以处理 PnP 和电源管理事件
ms.assetid: 7c9f10f1-1094-4b43-990b-fc3b3fee5ed1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d60ef6b907985ddd73028cebd26973e33b51bb7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824443"
---
# <a name="initializing-intermediate-drivers-to-handle-pnp-and-power-management-events"></a>初始化中间驱动程序以处理 PnP 和电源管理事件


若要处理即插即用（PnP）和电源管理事件，NDIS 中间驱动程序必须执行以下操作：

-   当 NDIS 调用中间驱动程序的[*ProtocolBindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)函数时， *BindParameters*参数指向[**NDIS\_PM\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)结构，该结构包含基础微型端口的功能适配器. 可在以下任一成员中报告电源管理功能：

    -   **PowerManagementCapabilities**

        对于 NDIS 6.0 和 NDIS 6.1 中间驱动程序，此成员包含 NDIS\_PNP\_功能结构中的电源管理功能。 有关此结构的详细信息，请参阅[OID\_PNP\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-capabilities)。

        **注意** 对于 NDIS 6.20 和更高版本中间驱动程序，将**PowerManagementCapabilities**成员设置为**NULL** ，并在**PowerManagementCapabilitiesEx**成员中报告电源管理功能。



    -   **PowerManagementCapabilitiesEx**

        对于 NDIS 6.20 和更高版本中间驱动程序，此成员包含[**NDIS\_PM\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)结构中的电源管理功能。

        **注意** 对于 NDIS 6.0 和 NDIS 6.1 中间驱动程序， **PowerManagementCapabilitiesEx**成员设置为**NULL** ，并且在**PowerManagementCapabilities**成员中报告电源管理功能。




**注意** 如果基础微型端口适配器不支持电源管理事件，则**PowerManagementCapabilities**和**PowerManagementCapabilitiesEx**成员将设置为**NULL**。




-   当 NDIS 为 NDIS 中间驱动程序支持的每个虚拟小型端口调用[MiniportInitializeEx](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)时，驱动程序将通过以下方式调用[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)来报告其电源管理功能：

    1.  根据 NDIS 中间驱动程序的版本，可以在**PowerManagementCapabilities**成员（对于 ndis 6.0 和 ndis 6.1 中间驱动程序）或**PowerManagementCapabilitiesEx**中报告电源管理功能。Ndis 的成员（适用于 NDIS 6.20 和更高版本中间驱动程序） [ **\_微型端口\_适配器\_常规\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)。 如果[**NDIS\_绑定\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)结构不为**NULL** **，则中间**驱动程序必须执行以下操作：

        -   保存**PowerManagementCapabilities**的**MinMagicPacketWakeUp**、 **MinPatternWakeUp**和**MinLinkChangeWakeUp**成员的原始值（ndis 6.0 和 ndis 6.1）或**PowerManagementCapabilitiesEx**（ndis6.20 及更高版本）的成员。

        -   通过将**MinMagicPacketWakeUp**、 **MinPatternWakeUp**和**MinLinkChangeWakeUp**成员设置为**NdisDeviceStateUnspecified**，禁用电源管理功能。

        -   在对[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)的调用中，将已修改的[**NDIS\_微型端口\_适配器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)的地址作为*MiniportAttributes*参数传递\_常规\_特性结构。

    2.  中间驱动程序必须将 NDIS\_微型端口\_属性\_不\_暂停\_在 [**NDIS\_微型端口\_适配器的 AttributeFlags 成员\_注册\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)结构。 在对[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)的调用中，驱动程序必须将此结构的地址作为*MiniportAttributes*参数进行传递。

    有关 NDIS 中间驱动程序的初始化要求的详细信息，请参阅[初始化 Virtual 微型端口](initializing-virtual-miniports.md)。









