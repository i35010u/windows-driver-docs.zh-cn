---
title: 处理 OID_PNP_Xxx 查询和设置请求
description: 处理 OID_PNP_Xxx 查询和设置请求
ms.assetid: 2d5db7fb-2a27-4359-9d75-35939e72de69
keywords:
- OID_PNP_Xxx
- 查询操作 WDK NDIS 中间
- 集运算 WDK NDIS 中间
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e031ed48a5b2d36cd1d2951cb65d6d699864031e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563987"
---
# <a name="handling-oidpnpxxx-queries-and-sets"></a>处理 OID\_PNP\_Xxx 查询和集





中间的驱动程序的虚拟微型端口必须导出[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)函数。 NDIS 调用中间驱动程序*MiniportOidRequest*函数时绑定到中间驱动程序的虚拟微型端口调用的基础驱动程序[ **NdisOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff563710)来查询或设置信息的对象 (OID\_*Xxx*)。 此外可以调用 NDIS *MiniportOidRequest*代表其自身。 有关设置和查询信息的对象的微型端口驱动程序处理的详细信息，请参阅[获取和设置微型端口驱动程序的信息和 NDIS 支持 WMI](obtaining-and-setting-miniport-driver-information-and-ndis-support-for.md)。

中间驱动程序应保留的基础的微型端口适配器的接收中的功能信息[ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220)函数。 如果微型端口适配器不是电源管理感知，请设置 NDIS**布尔**的成员[ **NDIS\_绑定\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff564832)到**NULL**。

中间驱动程序可使用查询或设置一个 OID\_*Xxx* ，由基础的微型端口驱动程序进行维护。 做到这一点与**NdisOidRequest**（如果中间驱动程序有无连接的下边缘），或使用[ **NdisCoOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff561711)(如果有中间驱动程序面向连接的下边缘）。

中间的驱动程序应处理查询和集，如下所示：

-   [OID\_PNP\_CAPABILITIES](https://msdn.microsoft.com/library/windows/hardware/ff569774)

    在此 OID 查询响应，中间驱动程序必须报告基础物理微型端口适配器所具有的即插即用的能力。 请注意，物理设备的微型端口适配器不会收到此 OID 查询。

    中间驱动程序绑定参数中接收的基础的微型端口适配器的即插即用功能。 它应将其传递给过量根据中间驱动程序的预期用途的驱动程序。 中间驱动程序和微型端口驱动程序报告微型端口适配器属性中的即插即用功能。 中间驱动程序不会发出 OID\_PNP\_为基础的微型端口驱动程序的功能请求。 如果基础的微型端口适配器是电源管理感知，在 NDIS\_PM\_唤醒\_向上\_功能构建虚拟微型端口属性中，中间驱动程序必须指定设备电源状态**NdisDeviceStateUnspecified**为每个唤醒功能：

    -   MinMagicPacketWakeUp
    -   MinPatternWakeUp
    -   MinLinkChangeWakeUp

    这种设置中指示中间驱动程序是管理感知电源，但无法唤醒系统。

-   [OID\_PNP\_查询\_POWER](https://msdn.microsoft.com/library/windows/hardware/ff569778)并[OID\_PNP\_设置\_电源](https://msdn.microsoft.com/library/windows/hardware/ff569780)

    中间驱动程序必须始终返回 NDIS\_状态\_OID 的查询的成功\_PNP\_查询\_电源或一系列 OID\_PNP\_设置\_电源。 中间驱动程序必须永远不会传播到基础微型端口驱动程序，这些 OID 请求之一。

-   "唤醒 Oid"

    如果基础 NIC，电源管理感知中间驱动程序必须传递给基础的微型端口驱动程序 (通过调用**NdisOidRequest**或**NdisCoOidRequest**) 以下 OID\_PNP\_*Xxx*唤醒使相关事件：

    [OID\_PNP\_ENABLE\_WAKE\_UP](https://msdn.microsoft.com/library/windows/hardware/ff569775)

    [OID\_PNP\_ADD\_WAKE\_UP\_PATTERN](https://msdn.microsoft.com/library/windows/hardware/ff569773)

    [OID\_PNP\_REMOVE\_WAKE\_UP\_PATTERN](https://msdn.microsoft.com/library/windows/hardware/ff569779)

    [OID\_PNP\_WAKE\_UP\_PATTERN\_LIST](https://msdn.microsoft.com/library/windows/hardware/ff569783)

    [OID\_PNP\_WAKE\_UP\_ERROR](https://msdn.microsoft.com/library/windows/hardware/ff569781)

    [OID\_PNP\_WAKE\_UP\_OK](https://msdn.microsoft.com/library/windows/hardware/ff569782)

中间驱动程序还将传播到基础协议驱动程序这些 Oid 基础微型端口驱动程序的响应。

如果基础的微型端口适配器是电源管理感知，微型端口驱动程序设置**布尔**的成员[ **NDIS\_微型端口\_适配器\_常规\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)到**NULL**和 NDIS 集**布尔**隶属[**NDIS\_绑定\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff564832)到**NULL**。

如果基础的微型端口适配器不是电源管理感知，中间驱动程序应返回 NDIS\_状态\_不\_以响应一个查询或一组这些 Oid 的支持。

 

 





