---
title: 设置 VMQ 筛选器
description: 设置 VMQ 筛选器
ms.assetid: d40b6806-6ba8-4073-b802-57cb886ffcfb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60cc8c2f42b28e22f93acaa484e0b7b9ff894d3a
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216580"
---
# <a name="setting-a-vmq-filter"></a>设置 VMQ 筛选器


分配接收队列后，过量驱动程序可以对接收队列设置筛选器。 只有分配有接收队列的驱动程序可以对该队列设置筛选器。

**注意**   因为默认接收队列 (**NDIS \_ 默认 \_ 接收 \_ 队列 \_ ID**) 始终存在，所以过量驱动程序始终可以在默认队列上设置接收筛选器。 过量驱动程序没有默认队列。 因此，绑定到网络适配器的所有协议驱动程序都可以使用默认队列。

 

## <a name="setting-a-filter-on-a-receive-queue"></a>在接收队列中设置筛选器


如果要使用一组初始配置参数对接收队列设置筛选器，则过量驱动程序会发出 [oid \_ 接收 \_ 筛选器 \_ 集 \_ 筛选器](./oid-receive-filter-set-filter.md) 方法对象标识符 (oid) 请求。 [**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员最初包含指向[**ndis \_ 接收 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构的指针。 成功从 OID 方法请求返回后， **ndis \_ OID \_ 请求**结构的**InformationBuffer**成员包含指向带有新筛选器标识符的**NDIS \_ 接收 \_ 筛选器 \_ 参数**结构的指针。

过量驱动程序用接收队列的下列筛选器配置参数初始化 [**NDIS \_ 接收 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters) 结构：

-   通过 [**NDIS \_ 接收 \_ 筛选器 \_ 类型**](/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_receive_filter_type) 枚举值指定的筛选器类型。

    **注意**   从 NDIS 6.20 开始，虚拟机队列只支持**NdisReceiveFilterTypeVMQueue**筛选器类型， (VMQ) 接口。

     

-   队列标识符。

-   格式化为 [**NDIS \_ 接收 \_ 筛选器 \_ 字段 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters) 结构的一个或多个字段测试参数。 对于 VMQ，定义了以下字段测试参数。

    -   数据包中 (MAC) 地址的目标媒体访问控制与指定的 MAC 地址相同。

    -   数据包中的虚拟 LAN (VLAN) 标识符与指定的 VLAN 标识符相等。

[**NDIS \_ 接收 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构与[oid \_ 接收 \_ \_ ](./oid-receive-filter-parameters.md)筛选器参数的结构一起使用，后者用于指定筛选器的配置参数。 [ \_ \_ \_ \_ ](./oid-receive-filter-set-filter.md)

[**Ndis \_ 接收 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构的**FieldParametersArrayOffset**、 **FieldParametersArrayNumElements**和**FieldParametersArrayElementSize**成员定义了一组[**ndis \_ 接收 \_ 筛选器 \_ 字段 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)结构。 数组中的每个 **NDIS \_ 接收 \_ 筛选器 \_ 字段 \_ 参数** 结构都为网络标头中的一个字段设置筛选器测试条件。

[**NDIS \_ 接收 \_ 筛选器 \_ 字段 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)结构的**Flags**成员指定要为接收筛选器执行的操作。 以下几点适用于 **NDIS \_ 接收 \_ 筛选器 \_ 字段 \_ MAC \_ 标头 VLAN 无标记 \_ \_ \_ 或 \_ 零** 标志：

-   如果在[**ndis \_ 接收 \_ 筛选器 \_ 字段 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)结构的**Flags**成员中设置了**ndis \_ 接收 \_ 筛选器 \_ 字段 " \_ MAC \_ 标头 VLAN 无标记 \_ \_ \_ 或 \_ 零**标志"，则网络适配器必须仅指示接收的符合以下所有测试条件的数据包：

    -   具有匹配 MAC 地址的数据包。

    -   没有 VLAN 标记或 VLAN 标识符为零的数据包。

    如果设置了 **NDIS \_ 接收 \_ 筛选器 \_ 字段 " \_ MAC \_ 标头 VLAN 无标记 \_ \_ \_ 或 \_ 零** 标志"，则网络适配器不能指示具有匹配 MAC 地址和非零 VLAN 标识符的数据包。

    **注意**   如果 Hyper-v 可扩展交换机设置 MAC 地址筛选器，并且在[OID \_ 接收 \_ 筛选器 \_ 集 \_ 筛选](./oid-receive-filter-set-filter.md)器中未配置 VLAN 标识符筛选器，则此开关还会设置**NDIS \_ 接收 \_ 筛选器 \_ 字段 \_ MAC \_ 标头 VLAN 无标记 \_ \_ \_ 或 \_ 零**标志。

     

-   如果未设置 **NDIS \_ 接收 \_ 筛选器 \_ 字段 \_ MAC \_ 标头 VLAN 无标记 \_ \_ \_ 或 \_ 零** 标志，并且没有 oid 集请求的 oid [ \_ 接收筛选器 \_ \_ 集 \_ 筛选](./oid-receive-filter-set-filter.md)器配置 VLAN 标识符筛选器，则微型端口驱动程序必须执行下列操作之一：

    -   如果微型端口驱动程序支持 NDIS 6.20，则它必须返回 [oid \_ 接收 \_ 筛选器 \_ 集 \_ 筛选器](./oid-receive-filter-set-filter.md)oid 请求的失败状态。

    -   如果微型端口驱动程序支持 ndis 6.30 或更高版本的 NDIS，则必须配置网络适配器以检查并筛选指定的 MAC 地址字段。 如果已接收的数据包中有 VLAN 标记，则网络适配器必须将其从数据包数据中删除。 微型端口驱动程序必须将 VLAN 标记放在与数据包的[**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构相关联的[** \_ \_ \_ \_ 8021Q \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_net_buffer_list_8021q_info)中。

-   如果协议驱动程序设置 MAC 地址筛选器和具有 [OID \_ 接收 \_ 筛选器 \_ 设置 \_ 筛选](./oid-receive-filter-set-filter.md) 器 oid 的 VLAN 标识符筛选器，则不会在任一筛选器字段中设置 **NDIS \_ 接收 \_ 筛选器 \_ 字段 \_ mac \_ 标头 VLAN 无标记 \_ \_ \_ 或 \_ 零** 标志。 在这种情况下，微型端口驱动程序应指示与指定的 MAC 地址和 VLAN 标识符相匹配的数据包。 也就是说，微型端口驱动程序不应指示具有具有零 VLAN 标识符或未标记数据包的匹配 MAC 地址的数据包。

## <a name="using-the-filter-identifier"></a>使用筛选器标识符


NDIS 在[**ndis \_ 接收 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构的**FilterId**成员中分配筛选器标识符，并将[OID \_ 接收 \_ 筛选器 \_ 集 \_ 筛选器](./oid-receive-filter-set-filter.md)的 oid 方法请求传递到基础微型端口驱动程序。 在接收队列上设置的每个筛选器都有一个用于网络适配器的唯一筛选器标识符。 也就是说，筛选器标识符不会复制到网络适配器管理的不同队列。

过量驱动程序必须使用 NDIS 在以后 OID 请求中提供的筛选器标识符;例如，修改筛选器参数或释放筛选器。

当 NDIS 接收到在接收队列上设置筛选器的 OID 请求时，它将验证筛选器参数。 在 NDIS 分配所需的资源和筛选器标识符后，它会将 OID 请求提交到基础网络适配器。 如果网络适配器可以成功分配筛选器所需的软件和硬件资源，则它将完成具有 **NDIS \_ 状态 \_ 成功**的 OID 请求。

微型端口驱动程序必须保留已分配接收筛选器的筛选标识符。 NDIS 使用筛选器的筛选器标识符和更高版本的 OID 请求来更改接收筛选器参数或清除接收筛选器。 有关如何更改参数和清除筛选器的详细信息，请参阅 [获取和更新 VM 队列参数](obtaining-and-updating-vm-queue-parameters.md) 和 [清除 VMQ 筛选器](clearing-a-vmq-filter.md)。

## <a name="handling-the-filter-on-a-receive-queue"></a>处理接收队列中的筛选器


微型端口驱动程序会按照以下方式基于筛选器来计划网络适配器：

-   特定筛选器的所有字段测试参数必须匹配才能将数据包分配给队列。

-   可以在队列中设置多个筛选器。

-   如果有任何筛选器通过，则必须将数据包分配给接收队列。

网络适配器将所有字段测试的结果与逻辑 **AND** 运算组合在一起。 也就是说，如果在 [**NDIS \_ 接收 \_ 筛选器 \_ 字段 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters) 结构的数组中包含的任何字段测试失败，则网络数据包不满足指定的筛选条件。

当网络适配器根据这些筛选条件测试接收的数据包时，必须忽略未指定测试条件的数据包中的所有字段。

## <a name="receiving-packets-from-a-receive-queue"></a>接收接收队列中的数据包


当微型端口驱动程序收到 [OID \_ 接收 \_ 筛选器 \_ 队列 \_ 分配 \_ 完成](./oid-receive-filter-queue-allocation-complete.md) 请求并具有在队列中设置的筛选器后，该队列将处于 " *正在运行* " 状态。 当队列处于此状态时，微型端口驱动程序可以指示队列中的数据包。 有关队列状态的详细信息，请参阅 [队列状态和操作](queue-states-and-operations.md)。

如果微型端口驱动程序已收到一个队列的 [oid \_ 接收 \_ 筛选器 \_ 队列 \_ 分配 \_ 完成](./oid-receive-filter-queue-allocation-complete.md) oid 请求，但没有在该队列上设置任何筛选器，则微型端口驱动程序不得指示该队列上的任何接收数据包。 在这种情况下，当微型端口驱动程序收到队列的 [OID \_ 接收 \_ 筛选器 \_ 集 \_ 筛选器](./oid-receive-filter-set-filter.md) oid 请求，并可能在完成 OID 请求之前，它可以指示该队列中的数据包。 如果微型端口驱动程序在处理 OID \_ 接收 \_ 筛选器设置筛选器 OID 请求时指示队列上的数据包 \_ \_ ，微型端口驱动程序必须完成 \_ \_ \_ \_ 具有 **NDIS \_ 状态 \_ 成功** 返回代码的 OID 接收筛选器集筛选器请求。

 

