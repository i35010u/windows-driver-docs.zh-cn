---
title: 注册 NDIS QoS 功能
description: 注册 NDIS QoS 功能
ms.assetid: 03D70079-37A4-4FAA-BF18-ACED3A9E8267
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22efd79d1370425868bd18e1e633f07837317f84
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211979"
---
# <a name="registering-ndis-qos-capabilities"></a>注册 NDIS QoS 功能


小型端口驱动程序在网络适配器初始化过程中 regsiter 以下服务质量 (QoS) 功能：

- 网络适配器支持的 NDIS QoS 硬件功能。

  **注意** 从 NDIS 6.30 开始，微型端口驱动程序必须注册该适配器支持的 NDIS QoS 硬件功能，前提是在注册表中存在<strong> \* QoS</strong> INF 关键字设置。 在这种情况下，无论适配器上启用还是禁用了这些功能，驱动程序都必须注册其 NDIS QoS 硬件功能。

     

- 当前在网络适配器上启用的 NDIS QoS 硬件功能。

  **注意** 可通过注册表中的** \* QoS** INF 关键字设置启用或禁用微型端口驱动程序的 NDIS QoS 硬件功能。 此设置显示在网络适配器的 " **高级** " 属性页上。

     

有关 NDIS QoS INF 关键字设置的详细信息，请参阅 [Ndis qos 的标准化 INF 关键字](standardized-inf-keywords-for-ndis-qos.md)。

微型端口驱动程序通过使用以下方法初始化的 [**NDIS \_ qos \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities) 结构报告基础网络适配器的硬件 NDIS qos 功能：

1.  微型端口驱动程序初始化 **标头** 成员。 驱动程序将**标头**的**类型**成员设置为 NDIS \_ 对象 \_ 类型 \_ QOS \_ 功能。

    从 NDIS 6.30 开始，微型端口驱动程序会将**标头**的**修订**成员设置为 ndis \_ qos \_ 功能 \_ 修订版本 \_ 1，并将**Size**成员设置为 ndis \_ SIZEOF \_ qos \_ 功能 \_ 修订版本 \_ 1。

2.  如果网络适配器支持严格优先级传输选择算法 (TSA) ，微型端口驱动程序会在 \_ \_ Flags 成员中设置 NDIS QOS 功能 \_ 严格的 \_ TSA \_ 支持标志。 **Flags** 有关此算法的详细信息，请参阅 [Strict 优先级算法](strict-priority-algorithm.md)。

    **注意**   从 NDIS 6.30 开始，为 IEEE 数据中心桥接 (DCB) 支持 NDIS QoS 的微型端口驱动程序和网络适配器必须支持严格优先级的 TSA。

     

3.  如果网络适配器支持绕过 media access control security (MACsec) 处理，微型端口驱动程序会在 \_ \_ Flags 成员中设置 NDIS QOS 功能 \_ MACsec \_ 绕过 \_ 受**Flags**支持的标志。 有关 MACsec 的详细信息，请参阅 IEEE 802.1 AE-2006 标准。

    **注意**   从 NDIS 6.30 开始，网络适配器不需要支持绕过 MACsec 处理。

     

4.  微型端口驱动程序将 **MaxNumTrafficClasses** 成员设置为网络适配器支持的最大 NDIS QoS 流量类数。 流量类定义 QoS 的传输或 *出口* 策略，如 IEEE 802.1 p priority level 和带宽分配。 有关流量类的详细信息，请参阅 [NDIS QoS 流量类](ndis-qos-traffic-classes.md)。

    **注意**   从 NDIS 6.30 开始，网络适配器必须支持至少三个通信类。

     

5.  微型端口驱动程序将 **MaxNumEtsCapableTrafficClasses** 成员设置为网络适配器可用于增强的传输选择 (ETS) 算法的 NDIS QoS 流量类的最大数目。 此值必须小于或等于 **MaxNumTrafficClasses** 成员的值。

    有关 ETS 的详细信息，请参阅 [增强的传输选择 (ETS) 算法](enhanced-transmission-selection--ets--algorithm.md)。

    **注意**   要使网络适配器支持 NDIS QoS，它必须支持两个支持 ETS 的通信类。

     

6.  微型端口驱动程序将 **MaxNumPfcEnabledTrafficClasses** 成员设置为网络适配器可将其与基于优先级的流控制（ (PFC) 算法）结合使用的 NDIS QoS 流量类的最大数目。 此值必须小于或等于 **MaxNumTrafficClasses** 成员的值。

    有关 PFC 的详细信息，请参阅 [)  (PFC 的基于优先级的流控制 ](priority-based-flow-control--pfc.md)。

    **注意**   要使网络适配器支持 NDIS QoS，它必须至少支持一个支持 PFC 的通信类。

     

当 NDIS 调用微型端口驱动程序的 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数时，驱动程序会按照以下步骤注册网络适配器的 NDIS QoS 属性：

1.  微型端口驱动程序初始化 [**NDIS \_ 微型端口 \_ 适配器 \_ 硬件 \_ 辅助 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes) 结构。

    微型端口驱动程序将 **HardwareQOSCapabilities** 成员设置为指向 previouslyinitialized [**NDIS \_ QOS \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities) 结构的指针。

    如果** \* QOS** INF 关键字的注册表设置的值为1，则将在网络适配器上启用 NDIS QOS 功能。 微型端口驱动程序将 **CurrentQOSCapabilities** 成员设置为指向相同 [**NDIS \_ QOS \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities) 结构的指针。

    如果** \* QOS** INF 关键字的注册表设置值为零，则将在网络适配器上禁用 NDIS QOS 功能。 微型端口驱动程序必须将 **CurrentQOSCapabilities** 成员设置为 NULL。

2.  驱动程序调用 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes) ，并将 *MiniportAttributes* 参数设置为指向 [**NDIS \_ 微型端口 \_ 适配器 \_ 硬件 \_ 协助 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes) 结构的指针。

有关适配器初始化过程的详细信息，请参阅 [初始化微型端口适配器](initializing-a-miniport-adapter.md)。

 

