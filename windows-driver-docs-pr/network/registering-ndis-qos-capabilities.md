---
title: 注册 NDIS QoS 功能
description: 注册 NDIS QoS 功能
ms.assetid: 03D70079-37A4-4FAA-BF18-ACED3A9E8267
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50632ad1dfc185fa50afb961b97a10d672f5fc0b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373857"
---
# <a name="registering-ndis-qos-capabilities"></a>注册 NDIS QoS 功能


微型端口驱动程序 regsiter NDIS 与以下服务 (QoS) 功能的质量在网络适配器初始化过程中：

- 支持的网络适配器的 NDIS QoS 硬件功能。

  **请注意**NDIS 6.30 从开始，微型端口驱动程序必须注册该适配器支持仅当的 NDIS QoS 硬件功能<strong>\*QOS</strong> INF 关键字设置是在注册表中存在。 在这种情况下，该驱动程序必须注册而不考虑这些功能是启用还是禁用的适配器上其 NDIS QoS 硬件功能。

     

- 当前已启用网络适配器的 NDIS QoS 硬件功能。

  **请注意**微型端口驱动程序的 NDIS QoS 硬件功能可以启用或禁用通过 **\*QOS** INF 关键字注册表中的设置。 此设置显示在**高级**网络适配器的属性页。

     

有关 NDIS QoS INF 关键字设置的详细信息，请参阅[NDIS QoS 的标准化 INF 关键字](standardized-inf-keywords-for-ndis-qos.md)。

微型端口驱动程序报告通过基础的网络适配器的硬件 NDIS QoS 功能[ **NDIS\_QOS\_功能**](https://msdn.microsoft.com/library/windows/hardware/hh451629)初始化的结构按以下方式：

1.  微型端口驱动程序初始化**标头**成员。 驱动程序集**类型**的成员**标头**到 NDIS\_对象\_类型\_QOS\_功能。

    从开始 NDIS 6.30，微型端口驱动程序设置**修订**的成员**标头**到 NDIS\_QOS\_功能\_修订\_1 和**大小**成员添加到 NDIS\_SIZEOF\_QOS\_功能\_修订\_1。

2.  如果网络适配器支持严格的优先级传输选择算法 (TSA)，微型端口驱动程序设置 NDIS\_QOS\_功能\_STRICT\_TSA\_中的支持标志**标志**成员。 有关此算法的详细信息，请参阅[严格优先级算法](strict-priority-algorithm.md)。

    **请注意**  从 NDIS 6.30，微型端口驱动程序和支持 NDIS QoS 对 IEEE 数据中心桥接 (DCB) 的网络适配器必须支持严格的优先级 TSA。

     

3.  如果网络适配器支持绕过媒体访问控制安全 (MACsec) 处理的功能，微型端口驱动程序设置 NDIS\_QOS\_功能\_MACSEC\_绕过\_支持中的标志**标志**成员。 有关 MACsec 的详细信息，请参阅 IEEE 802.1AE-2006 标准。

    **请注意**  从 NDIS 6.30 开始，网络适配器不需要支持的 MACsec 处理绕过。

     

4.  微型端口驱动程序集**MaxNumTrafficClasses**成员添加到的网络适配器支持的 NDIS QoS 流量类的最大数量。 流量类定义传输，或*出口*策略的 QoS，例如 IEEE 802.1p 优先级级别和带宽分配。 有关流量类的详细信息，请参阅[NDIS QoS 通信类](ndis-qos-traffic-classes.md)。

    **请注意**  从 NDIS 6.30，网络适配器必须支持至少三个通信类。

     

5.  微型端口驱动程序集**MaxNumEtsCapableTrafficClasses**成员添加到的网络适配器可用于增强传输选择 (ETS) 算法的 NDIS QoS 流量类的最大数量。 此值必须小于或等于的值**MaxNumTrafficClasses**成员。

    ETS 的详细信息，请参阅[增强传输选择 (ETS) 算法](enhanced-transmission-selection--ets--algorithm.md)。

    **请注意**  为支持 NDIS QoS 使网络适配器，则它必须支持至少两个支持 ETS 的流量类。

     

6.  微型端口驱动程序集**MaxNumPfcEnabledTrafficClasses**成员添加到的网络适配器可以使用基于优先级的流控制 (PFC) 算法与的 NDIS QoS 流量类的最大数量。 此值必须小于或等于的值**MaxNumTrafficClasses**成员。

    PFC 的详细信息，请参阅[基于优先级的流控制 (PFC)](priority-based-flow-control--pfc.md)。

    **请注意**  为支持 NDIS QoS 使网络适配器，则它必须支持至少一个支持 PFC 的流量类。

     

当 NDIS 调用微型端口驱动程序[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数，该驱动程序注册的网络适配器的 NDIS QoS 属性通过执行以下步骤：

1.  微型端口驱动程序初始化[ **NDIS\_微型端口\_适配器\_硬件\_协助\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565924)结构。

    微型端口驱动程序集**HardwareQOSCapabilities**成员为指向 previouslyinitialized [ **NDIS\_QOS\_功能**](https://msdn.microsoft.com/library/windows/hardware/hh451629)结构。

    如果的注册表设置 **\*QOS** INF 关键字的一个值，则网络适配器上启用的 NDIS QoS 功能。 微型端口驱动程序集**CurrentQOSCapabilities**指向相同的指针到成员[ **NDIS\_QOS\_功能**](https://msdn.microsoft.com/library/windows/hardware/hh451629)结构。

    如果的注册表设置 **\*QOS** INF 关键字的值为零、 NDIS QoS 功能已禁用网络适配器上。 微型端口驱动程序必须设置**CurrentQOSCapabilities**为 NULL 的成员。

2.  驱动程序调用[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)并设置*MiniportAttributes*参数指向的指针[ **NDIS\_微型端口\_适配器\_硬件\_帮助\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565924)结构。

有关适配器初始化过程的详细信息，请参阅[初始化微型端口适配器](initializing-a-miniport-adapter.md)。

 

 





