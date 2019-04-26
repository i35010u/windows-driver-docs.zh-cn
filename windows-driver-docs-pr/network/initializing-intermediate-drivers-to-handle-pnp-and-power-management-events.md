---
title: 在中间的驱动程序中处理 PnP 和电源管理事件
description: 初始化中间驱动程序以处理 PnP 和电源管理事件
ms.assetid: 7c9f10f1-1094-4b43-990b-fc3b3fee5ed1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a14f345f48748f8c61ca890eb7fd7f5aeab6246f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324943"
---
# <a name="initializing-intermediate-drivers-to-handle-pnp-and-power-management-events"></a>初始化中间驱动程序以处理 PnP 和电源管理事件


若要处理插即用 (PnP) 和电源管理事件，中间的 NDIS 驱动程序必须执行以下操作：

-   当 NDIS 调用中间驱动程序[ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220)函数， *BindParameters*参数指向[ **NDIS\_PM\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)结构，其中包含基础的微型端口适配器的功能。 以下成员之一中报告的电源管理功能：

    -   **PowerManagementCapabilities**

        NDIS 6.0 和 NDIS 6.1 中间驱动程序，此成员包含的电源管理功能内 NDIS\_PNP\_功能结构。 有关此结构的详细信息，请参阅[OID\_PNP\_功能](https://msdn.microsoft.com/library/windows/hardware/ff569774)。

        **请注意**有关 NDIS 6.20 和更高版本中间驱动程序**布尔**成员设置为**NULL** 中报告的电源管理功能和**PowerManagementCapabilitiesEx**成员。



    -   **PowerManagementCapabilitiesEx**

        有关 NDIS 6.20 和更高版本的中间驱动程序，此成员包含中的电源管理功能[ **NDIS\_PM\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)结构。

        **请注意**为 NDIS 6.0 和 NDIS 6.1 中间驱动程序， **PowerManagementCapabilitiesEx**成员设置为**NULL** 中报告的电源管理功能和**布尔**成员。




**请注意**基础的微型端口适配器不支持电源管理事件，如果**布尔**并**PowerManagementCapabilitiesEx**成员设置为**NULL**。




-   当调用 NDIS [MiniportInitializeEx](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)为 NDIS 中间驱动程序支持的每个虚拟微型端口驱动程序报告其电源管理功能通过调用[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)以下方面：

    1.  根据 NDIS 中间驱动程序的版本，报告的电源管理功能中任何一种**布尔**（适用于 NDIS 6.0 和 NDIS 6.1 中间驱动程序） 的成员或**PowerManagementCapabilitiesEx** （适用于 NDIS 6.20 和更高版本的中间驱动程序） 的成员[ **NDIS\_微型端口\_适配器\_常规\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)。 如果任一**布尔**或**PowerManagementCapabilitiesEx**的成员[ **NDIS\_绑定\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff564832)结构不是**NULL**，中间驱动程序必须执行以下操作：

        -   保存的原始值**MinMagicPacketWakeUp**， **MinPatternWakeUp**，并**MinLinkChangeWakeUp**的成员**布尔**（NDIS 6.0 和 NDIS 6.1） 或**PowerManagementCapabilitiesEx**(NDIS 6.20 及更高版本) 成员。

        -   通过设置来禁用电源管理功能**MinMagicPacketWakeUp**， **MinPatternWakeUp**，并**MinLinkChangeWakeUp**成员**NdisDeviceStateUnspecified**。

        -   将修改后的地址传递[ **NDIS\_微型端口\_适配器\_常规\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)结构作为*MiniportAttributes*对的调用中的参数[ **NdisMSetMiniportAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff563672)。

    2.  中间的驱动程序必须设置 NDIS\_微型端口\_特性\_否\_暂停\_ON\_中的挂起标志**AttributeFlags**的成员[ **NDIS\_微型端口\_适配器\_注册\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565934)结构。 该驱动程序必须通过作为此结构的地址*MiniportAttributes*调用中的参数[ **NdisMSetMiniportAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff563672)。

    中间的 NDIS 驱动程序的初始化要求的详细信息，请参阅[初始化虚拟微型端口](initializing-virtual-miniports.md)。









