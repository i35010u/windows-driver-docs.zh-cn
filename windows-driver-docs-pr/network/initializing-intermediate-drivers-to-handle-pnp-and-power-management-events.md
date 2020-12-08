---
title: 处理中间驱动程序中的 PnP 和电源管理事件
description: 初始化中间驱动程序以处理 PnP 和电源管理事件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09aab8bee7200f52af8ebe6d0668b6f85b5b50fd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816007"
---
# <a name="initializing-intermediate-drivers-to-handle-pnp-and-power-management-events"></a>初始化中间驱动程序以处理 PnP 和电源管理事件


若要处理即插即用 (PnP) 和电源管理事件，NDIS 中间驱动程序必须执行以下操作：

-   当 NDIS 调用中间驱动程序的 [*ProtocolBindAdapterEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex) 函数时， *BindParameters* 参数指向包含基础微型端口适配器功能的 [**NDIS \_ PM \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities) 结构。 可在以下任一成员中报告电源管理功能：

    -   **PowerManagementCapabilities**

        对于 NDIS 6.0 和 NDIS 6.1 中间驱动程序，此成员包含 NDIS \_ PNP 功能结构中的电源管理功能 \_ 。 有关此结构的详细信息，请参阅 [OID \_ PNP \_ 功能](./oid-pnp-capabilities.md)。

        **注意**  对于 NDIS 6.20 和更高版本中间驱动程序，将 **PowerManagementCapabilities** 成员设置为 **NULL** ，并在 **PowerManagementCapabilitiesEx** 成员中报告电源管理功能。



    -   **PowerManagementCapabilitiesEx**

        对于 NDIS 6.20 和更高版本中间驱动程序，此成员包含 [**NDIS \_ PM \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities) 结构中的电源管理功能。

        **注意**  对于 NDIS 6.0 和 NDIS 6.1 中间驱动程序， **PowerManagementCapabilitiesEx** 成员设置为 **NULL** ，并且在 **PowerManagementCapabilities** 成员中报告电源管理功能。




**注意**  如果基础微型端口适配器不支持电源管理事件，则 **PowerManagementCapabilities** 和 **PowerManagementCapabilitiesEx** 成员将设置为 **NULL**。




-   当 NDIS 为 NDIS 中间驱动程序支持的每个虚拟小型端口调用 [MiniportInitializeEx](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 时，驱动程序将通过以下方式调用 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes) 来报告其电源管理功能：

    1.  根据 NDIS 中间驱动程序的版本，可以在 NDIS 6.0 和 NDIS 6.1 中间驱动程序的 **PowerManagementCapabilities** 成员 (中报告电源管理功能，) 或 **PowerManagementCapabilitiesEx** 成员 () 6.20 [**用于 ndis \_ \_ \_ \_**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)的 如果 [**NDIS \_ 绑定 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)结构的 **PowerManagementCapabilities** 或 **PowerManagementCapabilitiesEx** 成员不为 **NULL**，则中间驱动程序必须执行以下操作：

        -   将 **PowerManagementCapabilities** 的 **MinMagicPacketWakeUp**、 **MinPatternWakeUp** 和 **MINLINKCHANGEWAKEUP** 成员的原始值保存 (ndis 6.0 和 ndis 6.1) 或 **PowerManagementCapabilitiesEx** (ndis 6.20 及更高版本) 成员。

        -   通过将 **MinMagicPacketWakeUp**、 **MinPatternWakeUp** 和 **MinLinkChangeWakeUp** 成员设置为 **NdisDeviceStateUnspecified**，禁用电源管理功能。

        -   在对 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)的调用中，将已修改的 [**NDIS \_ 微型端口 \_ 适配器的 \_ 常规 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)结构的地址传递为 *MiniportAttributes* 参数。

    2.  中间驱动程序必须 \_ \_ \_ \_ \_ \_ 在 [**ndis \_ 微型端口 \_ 适配器 \_ 注册 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)结构的 **AttributeFlags** 成员中设置 ndis 微型端口属性 NO 暂停标志。 在对 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)的调用中，驱动程序必须将此结构的地址作为 *MiniportAttributes* 参数进行传递。

    有关 NDIS 中间驱动程序的初始化要求的详细信息，请参阅 [初始化 Virtual 微型端口](initializing-virtual-miniports.md)。
