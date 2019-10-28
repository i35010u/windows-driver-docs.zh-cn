---
title: NDIS QoS 参数概述
description: NDIS QoS 参数概述
ms.assetid: E9321805-2930-410A-81BC-F7978517E89E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5dd9a4e97ad50a50b689b79a2c93ebb86c354f5e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843740"
---
# <a name="overview-of-ndis-qos-parameters"></a>NDIS QoS 参数概述


NDIS 服务质量（QoS）参数指定网络适配器用于传输或*传出*数据包传递的通信类的策略和设置。 NDIS QoS 参数包含以下设置：

-   优先级别和流控制设置。 这些设置定义 IEEE 802.1 p 优先级以及用于传输或*传出*流量的可选流控制算法。

    有关详细信息，请参阅[优先级别和流控制](priority-levels-and-flow-control.md)。

-   流量选择算法（TSA）设置。 这些设置定义网络适配器如何从其传输队列中选择传出流量。 例如，适配器可以使用 strict 优先级的 TSA，并选择仅基于 IEEE 802.1 p 优先级的传出数据包。 适配器还可以使用增强的传输选择（ETS） TSA，在通信类之间根据带宽分配来 moderates 传出流量。

    有关详细信息，请参阅[传输选择算法（TSAs）](transmission-selection-algorithms--tsas-.md)。

-   指定为包含与分类条件匹配的数据（如 EtherType 或目标 TCP 端口）的数据包指定 IEEE 802.1 p 优先级别分配的流量分类。 有关详细信息，请参阅[NDIS QoS 流量分类](ndis-qos-traffic-classifications.md)。

    **请注意**，  流量分类也称为 IEEE 802.1 规范中的 "应用程序优先级"。

     

NDIS QoS 定义以下类型的参数：

<a href="" id="local-ndis-qos-parameters"></a>本地 NDIS QoS 参数  
本地 NDIS QoS 参数指定微型端口驱动程序及其网络适配器的核心 QoS 设置。 这些参数将保留在系统注册表中，并按以下方式通过本地方式管理到微型端口驱动程序：

-   通过[\_QOS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-parameters)的 NDIS 对象标识符（oid）方法请求\_由 DCB 组件颁发的参数。 此 OID 请求包含一个[**NDIS\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构，用于指定本地 NDIS QOS 参数。

    有关 DCB 组件的详细信息，请参阅[用于数据中心桥接的 NDIS QoS 体系结构](ndis-qos-architecture-for-data-center-bridging.md)。

-   通过网络适配器的专有注册表设置。 当[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数由 NDIS 调用时，微型端口驱动程序将读取这些设置。

-   通过独立硬件供应商（IHV）开发的管理应用程序，通过颁发给微型端口驱动程序的设置。

有关微型端口驱动程序如何获取其本地 NDIS QoS 参数的详细信息，请参阅[设置本地 Ndis Qos 参数](setting-local-ndis-qos-parameters.md)。

<a href="" id="remote-ndis-qos-parameters"></a>远程 NDIS QoS 参数  
远程 NDIS QoS 参数是在网络适配器通过数据链路连接到的远程对等机上配置的参数。 微型端口驱动程序通过由 IEEE 802.1 Qaz 草案标准指定的数据中心桥接交换（DCBX）协议来发现这些参数。

DCBX 要求微型端口驱动程序只保留一组从单个数据链路对等端接收的远程 QoS 参数。 当首次从对等端接收或更改其远程 QoS 参数时，微型端口驱动程序必须发出 NDIS 状态指示。 例如，驱动程序可能会更改其远程 NDIS QoS 参数，因为它收到了来自其远程对等端的一组不同的 QoS 参数。 有关此过程的详细信息，请参阅[指示对远程 NDIS QoS 参数所做的更改](indicating-changes-to-the-remote-ndis-qos-parameters.md)。

有关微型端口驱动程序如何获取其远程 NDIS QoS 参数的详细信息，请参阅[接收远程 Ndis Qos 参数](receiving-remote-ndis-qos-parameters.md)。

<a href="" id="operational-ndis-qos-parameters"></a>操作 NDIS QoS 参数  
操作 NDIS QoS 参数是微型端口驱动程序为流量优先级解析的参数，这些参数通过数据链路连接到远程对等方。 微型端口驱动程序通过其本地或远程 NDIS QoS 参数解析其操作的 NDIS QoS 参数。

小型端口驱动程序必须在其操作 QoS 参数首次解析或稍后更改时发出 NDIS 状态指示。 例如，驱动程序可能会更改其操作 NDIS QoS 参数，因为它从其远程对等机接收了一组不同的 QoS 参数。 有关如何生成此状态指示的详细信息，请参阅[指示对操作 NDIS QoS 参数的更改](indicating-changes-to-the-operational-ndis-qos-parameters.md)。

有关微型端口驱动程序如何解析其操作的 NDIS QoS 参数的详细信息，请参阅[解决操作 Ndis Qos 参数](resolving-operational-ndis-qos-parameters.md)。

 

 





