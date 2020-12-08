---
title: 队列对的对称和非对称分配
description: 队列对的对称和非对称分配
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed659031e34e3b327cc23ac6167bc5333cbede4e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840889"
---
# <a name="symmetric-and-asymmetric-assignment-of-queue-pairs"></a>队列对的对称和非对称分配


队列对由网络适配器上的单独传输队列和接收队列组成。 创建 VPort 时，将在虚拟端口 (VPort) 上配置队列对。 与默认 VPort 关联的队列对是在创建交换机时通过 oid [ \_ NIC \_ 交换机 \_ CREATE \_ switch](./oid-nic-switch-create-switch.md)的 oid 方法请求配置的。 通过 oid [ \_ NIC \_ SWITCH \_ CREATE \_ VPort](./oid-nic-switch-create-vport.md)的 Oid 方法请求在非默认 VPort 上配置一个或多个队列对。

每个非默认 VPort 可以配置为具有不同的队列对数。 这称为队列对的 *非对称分配* 。 如果微型端口驱动程序不支持非对称分配，则每个非默认 VPort 将配置为具有相同数量的队列对。 这称为队列对的 *对称分配* 。

小型小型驱动程序使用 [**NDIS \_ NIC \_ 交换机 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)结构在 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)期间公布其 VPort 和队列对功能。 该驱动程序通过 \_ \_ \_ \_ \_ \_ \_ 为 \_ \_ \_ 此结构的 **NicSwitchCapabilities** 成员中的非默认 VPORT 支持标志设置 NDIS NIC 交换机头非对称队列对，来公布其对队列对非对称分配的支持。

如果微型端口驱动程序支持非对称队列对分配，则虚拟化堆栈会将每个非默认 VPort 配置为具有不同的队列对数。 如果微型端口驱动程序支持对称队列对分配，则虚拟化堆栈会将每个 VPort 配置为具有相同数量的队列对。

**注意**  支持非默认 VPorts 上的对称或非对称队列对分配的微型端口驱动程序必须支持在默认 VPort 上分配不同的队列对数。 默认 VPort 始终连接到网络适配器的 PF。

 

如果使用 [oid \_ nic \_ switch \_ CREATE \_ VPort](./oid-nic-switch-create-vport.md) 和 [oid \_ nic \_ switch \_ VPort \_ 参数](./oid-nic-switch-vport-parameters.md)的 oid 请求创建或更新非默认 VPort，则指定队列对配置。 在与两个 OID 请求关联的 [**NDIS \_ NIC \_ 交换机 \_ VPORT \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters) 结构中指定配置参数。

例如，假设微型端口驱动程序通过设置以下 [**NDIS \_ NIC \_ 交换机 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities) 结构的成员，在 NIC 交换机上公布 VPorts 和 queue 对的配置：

-   **MaxNumQueuePairs** 设置为128。

-   **MaxNumVPorts** 设置为64。

-   **MaxNumQueuePairsPerNonDefaultPort** 设置为4。

如果微型端口驱动程序不支持非默认 VPorts 上队列对的非对称配置，则在创建 VPorts 时，虚拟化堆栈可以指定以下队列对配置：

-   63非默认的 VF VPorts 每个队列对，其中每个都包含一个队列对，默认 PF 为 VPort。
-   31个非默认的 VF VPorts 每个队列对，其中每个都有一个队列对，默认 PF 为 VPort。

**注意**  从 Windows Server 2012 开始，仅支持一个默认 VPort，并始终连接到网络适配器的 PF。

 

 

