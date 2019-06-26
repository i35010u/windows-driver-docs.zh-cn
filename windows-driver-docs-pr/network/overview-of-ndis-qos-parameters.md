---
title: NDIS QoS 参数概述
description: NDIS QoS 参数概述
ms.assetid: E9321805-2930-410A-81BC-F7978517E89E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70335c6f3e8dbbb465baafab667412ea2a8676a1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384382"
---
# <a name="overview-of-ndis-qos-parameters"></a>NDIS QoS 参数概述


NDIS 服务质量 (QoS) 参数指定的策略和设置的流量类的网络适配器将使用传输，或*出口*，数据包发送。 NDIS QoS 参数包含以下设置：

-   优先级别和流控制设置。 这些设置用于定义传输，IEEE 802.1p 优先级级别和可选的流控制算法或*出口*，流量。

    有关详细信息，请参阅[优先级别和流控制](priority-levels-and-flow-control.md)。

-   流量选择算法 (TSA) 设置。 这些设置定义的网络适配器如何从其传输队列选择传出流量。 例如，适配器可以使用严格的优先级 TSA 并选择仅根据 IEEE 802.1p 优先级的流出数据包。 适配器也可以使用增强传输选择 (ETS) TSA 减少基于其带宽分配的流量类之间的传出流量。

    有关详细信息，请参阅[传输选择算法 (TSAs)](transmission-selection-algorithms--tsas-.md)。

-   指定的包，其中包含与分类条件，如 EtherType 或目标的 TCP 端口匹配的数据为 IEEE 802.1p 优先级级别分配的流量分类。 有关详细信息，请参阅[NDIS QoS 流量分类](ndis-qos-traffic-classifications.md)。

    **请注意**  流量分类也被称为"应用程序优先级"IEEE 802.1 规范中的。

     

NDIS QoS 用于定义以下类型的参数：

<a href="" id="local-ndis-qos-parameters"></a>本地的 NDIS QoS 参数  
本地的 NDIS QoS 参数指定的微型端口驱动程序和其网络适配器的核心 QoS 设置。 这些参数保留在系统注册表中和本地管理到微型端口驱动程序如下所示：

-   通过的 NDIS 对象标识符 (OID) 方法请求[OID\_QOS\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-parameters)DCB 组件颁发。 此 OID 请求包含[ **NDIS\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构，它指定本地的 NDIS QoS 参数。

    有关 DCB 组件的详细信息，请参阅[NDIS QoS 体系结构的数据中心桥接](ndis-qos-architecture-for-data-center-bridging.md)。

-   通过网络适配器的专有注册表设置。 微型端口驱动程序将读取这些设置时其[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize) NDIS 调用函数。

-   通过颁发给通过管理应用程序由独立硬件供应商 (IHV) 开发的微型端口驱动程序的设置。

微型端口驱动程序如何获取其本地的 NDIS QoS 参数的详细信息，请参阅[设置本地 NDIS QoS 参数](setting-local-ndis-qos-parameters.md)。

<a href="" id="remote-ndis-qos-parameters"></a>远程 NDIS QoS 参数  
远程 NDIS QoS 参数是通过数据链接的网络适配器连接到远程对等方上配置。 微型端口驱动程序将发现这些参数通过 IEEE 802.1Qaz 由指定的数据中心桥接交换 (DCBX) 协议草案标准。

DCBX 需要微型端口驱动程序维护只有一组从单个数据链接对等方接收到的远程 QoS 参数。 其远程 QoS 参数既接收来自对等方第一次或更高版本更改时，微型端口驱动程序必须发出 NDIS 状态指示。 例如，驱动程序可能会更改其远程 NDIS QoS 参数，因为它从其远程对等方接收到一组不同的 QoS 参数。 此过程的详细信息，请参阅[对远程 NDIS QoS 参数，该值指示更改](indicating-changes-to-the-remote-ndis-qos-parameters.md)。

微型端口驱动程序如何获取其远程 NDIS QoS 参数的详细信息，请参阅[接收远程 NDIS QoS 参数](receiving-remote-ndis-qos-parameters.md)。

<a href="" id="operational-ndis-qos-parameters"></a>操作的 NDIS QoS 参数  
操作的 NDIS QoS 参数是那些微型端口驱动程序可为通信优先级解析通过数据链路连接到远程对等方。 微型端口驱动程序解析其操作的 NDIS QoS 参数从其本地或远程 NDIS QoS 参数。

其操作的 QoS 参数或者解决第一次或更高版本更改时，微型端口驱动程序必须发出 NDIS 状态指示。 例如，驱动程序可能会更改其操作的 NDIS QoS 参数，因为它从其远程对等方接收到一组不同的 QoS 参数。 有关如何生成此状态指示的详细信息，请参阅[对操作的 NDIS QoS 参数，该值指示更改](indicating-changes-to-the-operational-ndis-qos-parameters.md)。

有关如何微型端口驱动程序解决其操作的 NDIS QoS 参数的详细信息，请参阅[解析操作的 NDIS QoS 参数](resolving-operational-ndis-qos-parameters.md)。

 

 





