---
title: 在虚拟端口上设置接收筛选器
description: 在虚拟端口上设置接收筛选器
ms.assetid: F0137D59-1701-4DFC-BB30-27E477FC0706
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 741567752447d1052544ef89bc2ce39577dc6cf3
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216582"
---
# <a name="setting-a-receive-filter-on-a-virtual-port"></a>在虚拟端口上设置接收筛选器


在网络适配器的 NIC 交换机上创建虚拟端口 (VPort) 后，过量驱动程序可以在 VPort 上设置接收筛选器。 只有创建 VPort 的驱动程序才能在该 VPort 上设置接收筛选器。

本主题包含以下信息：

[设置 VPort 的接收筛选器](#setting-a-receive-filter-on-a-vport)

[使用 NDIS \_ 接收 \_ 筛选器 \_ 字段 \_ MAC \_ 标头 \_ VLAN 无 \_ \_ \_ 标记或零标志](#using-the-ndis_receive_filter_field_mac_header_vlan_untagged_or_zero-flag)

[使用筛选器标识符](#using-the-filter-identifier)

[处理 VPort 上的接收筛选器](#handling-receive-filters-on-a-vport)

有关如何创建 VPort 的详细信息，请参阅 [创建虚拟端口](creating-a-virtual-port.md)。

**注意**   因为默认 VPort 始终存在并且永远不会被显式创建，所以任何过量驱动程序都可以在默认的 VPort 上设置接收筛选器。 过量驱动程序没有默认的 VPort。 因此，绑定到网络适配器的所有协议驱动程序都可以使用默认的 VPort。 默认 VPort 的标识符值为 NDIS \_ default \_ VPort \_ ID。

 

## <a name="setting-a-receive-filter-on-a-vport"></a>设置 VPort 的接收筛选器


若要设置和配置 VPort 的筛选器，过量驱动程序) [oid \_ 接收 \_ 筛选器 \_ 集 \_ 筛选](./oid-receive-filter-set-filter.md)器 (oid 发出对象标识符。 [**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员最初包含指向[**ndis \_ 接收 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构的指针。

在过量驱动程序发出此 OID 方法请求之前，它必须初始化 [**NDIS \_ 接收 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters) 结构。 驱动程序必须按以下方式设置此结构的成员：

-   **FilterType**成员必须设置为[**NDIS \_ 接收 \_ 筛选器 \_ 类型**](/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_receive_filter_type)枚举值。

    **注意**   从 NDIS 6.30 开始，只有**NdisReceiveFilterTypeVMQueue**的筛选器类型支持 (sr-iov) 接口的单个根 i/o 虚拟化。

     

-   **QueueId**成员必须设置为 NDIS \_ 默认 \_ 接收 \_ 队列 \_ ID。

-   **VPortId**成员必须设置为与 VPort 关联的标识符。 过量驱动程序通过以下方式之一获取 VPort 标识符：

    -   从 Oid NIC 交换机的上一个 OID 方法请求 [ \_ \_ \_ 创建 \_ VPORT](./oid-nic-switch-create-vport.md)。

    -   从 [oid \_ NIC \_ 交换机 \_ 枚举 \_ VPORTS](./oid-nic-switch-enum-vports.md)的上一个 oid 方法请求开始。

-   **FilterId**成员必须设置为 NDIS \_ 默认 \_ 接收 \_ 筛选器 \_ ID。

    **注意**   在将 OID 请求转发到微型端口驱动程序以进行处理之前，NDIS 在此成员中分配一个唯一的筛选器标识符。

     

-   必须适当地设置[**ndis \_ 接收 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构的**FieldParametersArrayOffset**、 **FieldParametersArrayNumElements**和**FieldParametersArrayElementSize**成员，才能定义[**ndis \_ 接收 \_ 筛选器 \_ 字段 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)结构的数组。 数组中的每个 **NDIS \_ 接收 \_ 筛选器 \_ 字段 \_ 参数** 结构都为网络标头中的一个字段设置筛选器测试条件。

    对于 SR-IOV 接口，定义了以下字段测试参数：

    -   数据包中 (MAC) 地址的目标媒体访问控制与指定的 MAC 地址相同。

    -   数据包中的虚拟 LAN (VLAN) 标识符与指定的 VLAN 标识符相等。

成功从 OID 方法请求返回后， [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向带有新筛选器标识符的[**NDIS \_ 接收 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构的指针。

## <a name="using-the-ndis_receive_filter_field_mac_header_vlan_untagged_or_zero-flag"></a><a name="using-the-ndis_receive_filter_field_mac_header_vlan_untagged_or_zero-flag"></a>使用 NDIS \_ 接收 \_ 筛选器 \_ 字段 \_ MAC \_ 标头 \_ VLAN 无 \_ \_ \_ 标记或零标志


[**NDIS \_ 接收 \_ 筛选器 \_ 字段 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)结构的**Flags**成员指定要为接收筛选器执行的操作。 以下几点适用于 **NDIS \_ 接收 \_ 筛选器 \_ 字段 \_ MAC \_ 标头 VLAN 无标记 \_ \_ \_ 或 \_ 零** 标志：

-   如果在**Flags**成员中设置了**NDIS \_ 接收 \_ 筛选器 \_ 字段 " \_ MAC \_ 标头 VLAN 无标记 \_ \_ \_ 或 \_ 零**标志"，则网络适配器必须仅指示接收的符合以下所有测试标准的数据包：

    -   具有匹配 MAC 地址的数据包。

    -   没有 VLAN 标记或 VLAN 标识符为零的数据包。

    如果设置了 **NDIS \_ 接收 \_ 筛选器 \_ 字段 " \_ MAC \_ 标头 VLAN 无标记 \_ \_ \_ 或 \_ 零** 标志"，则网络适配器不能指示具有匹配 MAC 地址和非零 VLAN 标识符的数据包。

    **注意**   如果虚拟化堆栈设置 MAC 地址筛选器，而不是由[OID \_ 接收 \_ 筛选 \_ \_ ](./oid-receive-filter-set-filter.md)器集筛选器集请求配置任何 VLAN 标识符筛选器，则此开关还会设置**NDIS \_ 接收 \_ 筛选器 \_ 字段 \_ MAC \_ 标头 VLAN 无标记 \_ \_ \_ 或 \_ 零**标志。

     

-   从 NDIS 6.30 开始，如果未设置 **ndis \_ 接收 \_ 筛选器 \_ 字段 \_ MAC \_ 标头 VLAN 无标记 \_ \_ \_ 或 \_ 零** 标志，并且 [OID \_ 接收筛选器 \_ \_ 集 \_ 筛选](./oid-receive-filter-set-filter.md) 器方法请求未配置 VLAN 标识符筛选器，则微型端口驱动程序必须执行下列操作之一：

    -   微型端口驱动程序必须返回 [OID \_ 接收 \_ 筛选器 \_ 集 \_ 筛选器](./oid-receive-filter-set-filter.md) 方法请求的失败状态。

    -   微型端口驱动程序必须将网络适配器配置为检查和筛选指定的 MAC 地址字段。 如果已接收的数据包中有 VLAN 标记，则网络适配器必须将其从数据包数据中删除。 微型端口驱动程序必须将 VLAN 标记放在与数据包的[**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构相关联的[** \_ \_ \_ \_ 8021Q \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_net_buffer_list_8021q_info)中。

-   如果协议驱动程序使用 [OID \_ 接收 \_ 筛选器 \_ 集 \_ 筛选](./oid-receive-filter-set-filter.md) 器方法请求设置 MAC 地址筛选器和 VLAN 标识符筛选器，则不会在任一筛选器字段中设置 **NDIS \_ 接收 \_ 筛选器 \_ 字段 \_ MAC \_ 标头 VLAN 无标记 \_ \_ \_ 或 \_ 零** 标志。 在这种情况下，微型端口驱动程序应指示与指定的 MAC 地址和 VLAN 标识符相匹配的数据包。 也就是说，微型端口驱动程序不应指示具有具有零 VLAN 标识符或未标记数据包的匹配 MAC 地址的数据包。

## <a name="using-the-filter-identifier"></a>使用筛选器标识符


NDIS 在[**ndis \_ 接收 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构的**FilterId**成员中分配筛选器标识符，并将[OID \_ 接收 \_ 筛选器 \_ 集 \_ 筛选器](./oid-receive-filter-set-filter.md)的 oid 方法请求传递到基础微型端口驱动程序。 在 VPort 上设置的每个筛选器都有一个用于网络适配器的唯一筛选器标识符。 也就是说，筛选器标识符不会复制到网络适配器管理的不同队列。

过量驱动程序必须使用 NDIS 在以后 OID 请求中提供的筛选器标识符来更改筛选器参数或释放筛选器。

当 NDIS 收到 OID 请求以便在 VPort 上设置筛选器时，它将验证筛选器参数。 在 NDIS 分配所需的资源和筛选器标识符后，它会将 OID 请求提交到基础网络适配器。 如果网络适配器可以成功分配筛选器所需的软件和硬件资源，则它将完成具有 **NDIS \_ 状态 \_ 成功**的 OID 请求。

微型端口驱动程序必须保留已分配接收筛选器的筛选标识符。 NDIS 使用筛选器的筛选器标识符和更高版本 OID 请求来更改接收筛选器参数或清除接收筛选器。 有关如何更改参数和清除筛选器的详细信息，请参阅 [获取和更新 VM 队列参数](obtaining-and-updating-vm-queue-parameters.md) 和 [清除 VMQ 筛选器](clearing-a-vmq-filter.md)。

## <a name="handling-receive-filters-on-a-vport"></a>处理 VPort 上的接收筛选器


微型端口驱动程序会按照以下方式基于筛选器来计划网络适配器：

-   特定筛选器的所有字段测试参数必须匹配才能将数据包分配给 VPort。

-   可以在 VPort 上设置多个筛选器。

-   如果有任何筛选器通过，则必须将数据包分配给 VPort。

网络适配器将所有字段测试的结果与逻辑 **AND** 运算组合在一起。 也就是说，如果在 [**NDIS \_ 接收 \_ 筛选器 \_ 字段 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters) 结构的数组中包含的任何字段测试失败，则网络数据包不满足指定的筛选条件。

当网络适配器根据这些筛选条件测试接收的数据包时，必须忽略数据包中没有指定的测试条件的所有字段。

 

