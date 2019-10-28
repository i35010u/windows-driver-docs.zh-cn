---
title: 注册 NDIS QoS 功能
description: 注册 NDIS QoS 功能
ms.assetid: 03D70079-37A4-4FAA-BF18-ACED3A9E8267
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d94c9506554332df2b99cbaad2ce7e24dc5ef41f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842075"
---
# <a name="registering-ndis-qos-capabilities"></a>注册 NDIS QoS 功能


小型端口驱动程序在网络适配器初始化过程中 regsiter 以下服务质量（QoS）功能：

- 网络适配器支持的 NDIS QoS 硬件功能。

  **注意** 从 NDIS 6.30 开始，如果注册表中存在<strong>\*QoS</strong> INF 关键字设置，微型端口驱动程序必须注册该适配器支持的 NDIS QoS 硬件功能。 在这种情况下，无论适配器上启用还是禁用了这些功能，驱动程序都必须注册其 NDIS QoS 硬件功能。

     

- 当前在网络适配器上启用的 NDIS QoS 硬件功能。

  **注意** 可通过注册表中的 " **\*QoS** INF 关键字" 设置来启用或禁用微型端口驱动程序的 NDIS QoS 硬件功能。 此设置显示在网络适配器的 "**高级**" 属性页上。

     

有关 NDIS QoS INF 关键字设置的详细信息，请参阅[Ndis qos 的标准化 INF 关键字](standardized-inf-keywords-for-ndis-qos.md)。

微型端口驱动程序通过通过[**NDIS\_qos\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities)结构，通过以下方式来报告基础网络适配器的硬件 NDIS QoS 功能：

1.  微型端口驱动程序初始化**标头**成员。 驱动程序将**标头**的**类型**成员设置为\_对象\_类型\_QOS\_功能。

    从 NDIS 6.30 开始，微型端口驱动程序会将**标头**的**修订**成员设置为 NDIS\_QOS\_功能\_修订版本\_1，将**Size**成员设置为 ndis\_SIZEOF\_qos\_功能\_修订版\_1。

2.  如果网络适配器支持严格优先级传输选择算法（TSA），微型端口驱动程序会将 NDIS\_QOS\_功能\_STRICT\_\_在**Flags**成员中支持 有关此算法的详细信息，请参阅[Strict 优先级算法](strict-priority-algorithm.md)。

    **注意**  从 NDIS 6.30 开始，支持用于 IEEE 数据中心桥接（DCB）的 NDIS QoS 的微型端口驱动程序和网络适配器必须支持严格优先级的 TSA。

     

3.  如果网络适配器支持绕过媒体访问控制安全性（MACsec）处理的功能，微型端口驱动程序会将 NDIS\_QOS\_功能\_\_绕过**标志**中的\_支持的标志职员. 有关 MACsec 的详细信息，请参阅 IEEE 802.1 AE-2006 标准。

    **请注意**  从 NDIS 6.30 开始，网络适配器不需要支持绕过 MACsec 处理。

     

4.  微型端口驱动程序将**MaxNumTrafficClasses**成员设置为网络适配器支持的最大 NDIS QoS 流量类数。 流量类定义 QoS 的传输或*出口*策略，如 IEEE 802.1 p priority level 和带宽分配。 有关流量类的详细信息，请参阅[NDIS QoS 流量类](ndis-qos-traffic-classes.md)。

    **注意**  从 NDIS 6.30 开始，网络适配器必须支持至少三个通信类。

     

5.  微型端口驱动程序将**MaxNumEtsCapableTrafficClasses**成员设置为网络适配器可用于增强的传输选择（ETS）算法的 NDIS QoS 流量类的最大数目。 此值必须小于或等于**MaxNumTrafficClasses**成员的值。

    有关 ETS 的详细信息，请参阅[增强的传输选择（ETS）算法](enhanced-transmission-selection--ets--algorithm.md)。

    **请注意**，  网络适配器支持 NDIS QoS，则它必须至少支持两个支持 ETS 的通信类。

     

6.  微型端口驱动程序将**MaxNumPfcEnabledTrafficClasses**成员设置为网络适配器可用于基于优先级的流控制（PFC）算法的 NDIS QoS 流量类的最大数目。 此值必须小于或等于**MaxNumTrafficClasses**成员的值。

    有关 PFC 的详细信息，请参阅[基于优先级的流控制（PFC）](priority-based-flow-control--pfc.md)。

    **请注意**，  网络适配器支持 NDIS QoS，则它必须至少支持一个支持 PFC 的通信类。

     

当 NDIS 调用微型端口驱动程序的[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数时，驱动程序会按照以下步骤注册网络适配器的 NDIS QoS 属性：

1.  微型端口驱动程序初始化[**NDIS\_微型端口\_适配器\_硬件\_帮助\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)结构。

    微型端口驱动程序将**HardwareQOSCapabilities**成员设置为指向 previouslyinitialized [**NDIS\_QOS\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities)结构的指针。

    如果 **\*QOS** INF 关键字的注册表设置值为1，则将在网络适配器上启用 NDIS QOS 功能。 微型端口驱动程序将**CurrentQOSCapabilities**成员设置为指向同一[**NDIS\_QOS\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities)结构的指针。

    如果 **\*QOS** INF 关键字的注册表设置值为零，则将在网络适配器上禁用 NDIS QOS 功能。 微型端口驱动程序必须将**CurrentQOSCapabilities**成员设置为 NULL。

2.  驱动程序调用[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes) ，并将*MiniportAttributes*参数设置为指向[**NDIS\_微型端口的指针\_适配器\_硬件\_帮助\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)结构。

有关适配器初始化过程的详细信息，请参阅[初始化微型端口适配器](initializing-a-miniport-adapter.md)。

 

 





