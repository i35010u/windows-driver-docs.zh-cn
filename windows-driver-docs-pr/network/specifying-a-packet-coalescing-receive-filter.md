---
title: 指定数据包合并接收筛选器
description: 指定数据包合并接收筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a926366c71188965071e0a840656eb5a11b1304
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248039"
---
# <a name="specifying-a-packet-coalescing-receive-filter"></a>指定数据包合并接收筛选器


过量驱动程序可以在支持 NDIS 数据包合并的微型端口驱动程序上设置一个或多个接收筛选器。 过量驱动程序最多可以指定在 [**NDIS \_ 接收 \_ 筛选器 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构的 **MaxPacketCoalescingFilters** 成员中指定的微型端口驱动程序的接收筛选器的最大数量。

**注意** 过量协议驱动程序在 [**ndis \_ 绑定 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)结构中获取 [**ndis \_ 接收 \_ 筛选器 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构。 过量筛选器驱动程序在 [**ndis \_ 筛选器 \_ 附加 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)结构中获取 **ndis \_ 接收 \_ 筛选器 \_ 功能** 结构。

 

过量驱动程序通过发出 [oid \_ 接收 \_ 筛选器 \_ 集 \_ 筛选器](./oid-receive-filter-set-filter.md)的 oid 方法请求，将接收筛选器下载到微型端口驱动程序。 此 OID 请求的 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含指向调用方分配的缓冲区的指针。 此缓冲区的格式设置为包含以下内容：

-   用于指定 NDIS 接收筛选器参数的 [**ndis \_ 接收 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters) 结构。

    有关如何初始化此结构的详细信息，请参阅 [指定接收筛选器](#specifying-a-receive-filter)。

-   用于指定网络数据包标头中的字段筛选器测试条件的 [**NDIS \_ 接收 \_ 筛选器 \_ 字段 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters) 结构的数组。

    有关如何初始化这些结构的详细信息，请参阅 [指定标头字段测试](#specifying-header-field-tests)。

## <a name="specifying-a-receive-filter"></a>指定接收筛选器


过量驱动程序通过使用筛选器的配置参数初始化 [**NDIS \_ 接收 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters) 结构来指定数据包合并接收筛选器。 初始化 **NDIS \_ 接收 \_ 筛选器 \_ 参数** 结构时，过量驱动程序必须遵循以下规则：

-   **FilterType** 成员必须设置为 **NdisReceiveFilterTypePacketCoalescing** 的 [**NDIS \_ 接收 \_ 筛选器 \_ 类型**](/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_receive_filter_type)枚举值。

-   **QueueId** 成员必须设置为 NDIS \_ 默认 \_ 接收 \_ 队列 \_ ID。

    **注意**  从 NDIS 6.30 开始，仅在网络适配器的默认接收队列中支持数据包合并接收筛选器。 此接收队列具有 NDIS \_ 默认 \_ 接收 \_ 队列 ID 的标识符 \_ 。

     

-   如果过量驱动程序正在创建新的接收筛选器，则必须将 **FilterId** 成员设置为 NDIS \_ 默认 \_ 接收 \_ 筛选器 \_ ID。

    **注意** 在将 Oid 请求的 oid 方法请求转发到微型端口驱动程序之前，NDIS 将生成接收筛选器的唯一筛选器标识符 (ID) 。 [ \_ \_ \_ \_](./oid-receive-filter-set-filter.md)     

-  如果过量驱动程序正在修改现有的接收筛选器，则必须将 **FilterId** 成员设置为接收筛选器的非零筛选器 ID。 当过量驱动程序发出 [oid \_ 接收 \_ 筛选器 \_ 枚举 \_ 筛选](./oid-receive-filter-enum-filters.md)器的 oid 方法请求时，将获取接收筛选器的筛选器 ID。 有关如何修改接收筛选器的详细信息，请参阅 [修改包合并接收筛选器](modifying-packet-coalescing-receive-filters.md)。

-   必须将 [**NDIS \_ 接收 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构的 **FieldParametersArrayOffset**、 **FieldParametersArrayNumElements** 和 **FieldParametersArrayElementSize** 成员设置为定义字段参数的数组。 数组中的每个元素都是一个 [**NDIS \_ 接收 \_ 筛选器 \_ 字段 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters) 结构，用于指定接收筛选器的标头字段测试的参数。

-   **RequestedFilterIdBitCount** 成员必须设置为零。

-   **MaxCoalescingDelay** 必须设置为与接收筛选器匹配的第一个数据包在网络适配器上保存并合并的最长时间（以毫秒为单位）。 一旦收到第一个与筛选器匹配的数据包，网络适配器就会将数据包合并，并启动一个将过期时间设置为 **MaxCoalescingDelay** 成员值的硬件计时器。

过量驱动程序必须对字段参数数组中的标头字段测试进行排序，使其顺序与关联 MAC 和协议标头在数据包中的顺序相同。

例如，在过量驱动程序为 IP 版本4指定筛选器参数 (IPv4) 协议字段之前，必须先为 MAC 标头协议字段指定筛选器参数 (NdisMacHeaderFieldProtocol) 。 通过这种方式，驱动程序将指定一个标头字段测试，该测试验证是否已将字段设置为正确的 EtherType 值 (0x0800) 用于 IPv4 数据包。 如果测试失败，则适配器不需要执行 IPV4 协议字段的测试。

## <a name="specifying-header-field-tests"></a>指定标头字段测试


每个接收筛选器都可以指定一个或多个测试条件 () 的 *标头字段测试* 。 网络适配器执行这些测试来确定是否应将接收的数据包合并到适配器上的硬件合并缓冲器中。 此外，过量驱动程序可以为不同的媒体访问控制指定单独的筛选器测试 (MAC) 、IP 版本 4 (IPv4) 和 IP 版本 6 (IPv6) 标头字段。

为了优化网络适配器上的筛选，标头字段测试基于标准化标头字段名称，而不是数据包数据中的字节偏移量/长度规范。 通过使用标头/字段名称，网络适配器的硬件或固件可以优化多个标头字段测试在收到的数据包上的执行方式。

每个接收筛选器都可以包含一个或多个由 [**NDIS \_ 接收 \_ 筛选器 \_ 字段 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters) 结构指定的标头字段测试。 每 **个 \_ ndis \_ 接收筛选器 \_ 字段 \_ 参数** 结构是字段参数数组的一个元素，由 [**NDIS \_ 接收 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构的 **FieldParametersArrayOffset**、 **FieldParametersArrayNumElements** 和 **FieldParametersArrayElementSize** 成员引用。

当微型端口驱动程序处理 [oid \_ 接收 \_ 筛选器 \_ 集 \_ 筛选器](./oid-receive-filter-set-filter.md)的 oid 方法请求时，必须遵循以下准则：

-   如果在 [**ndis \_ 接收 \_ 筛选器 \_ 字段 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)结构的 **Flags** 成员中设置了 **ndis \_ 接收 \_ 筛选器 \_ 字段 \_ MAC \_ 标头 VLAN 无标记 \_ \_ \_ 或 \_ 零** 标志，则该网络适配器必须仅指示具有匹配的 MAC 地址的接收数据包，以及未标记的数据包或 VLAN 标识符为零的数据包。 也就是说，网络适配器不能指示具有匹配 MAC 地址和非零 VLAN 标识符的数据包。

-   如果未设置 **NDIS \_ 接收 \_ 筛选器 \_ 字段 \_ MAC \_ 标头 VLAN 无标记 \_ \_ \_ 或 \_ 零** 标志，并且没有 oid 集请求的 oid [ \_ 接收筛选器 \_ \_ 集 \_ 筛选](./oid-receive-filter-set-filter.md)器配置 VLAN 标识符筛选器，则微型端口驱动程序必须执行下列操作之一：

    -   如果微型端口驱动程序支持 NDIS 6.20，则它必须返回 [oid \_ 接收 \_ 筛选器 \_ 集 \_ 筛选器](./oid-receive-filter-set-filter.md)oid 请求的失败状态。

    -   如果微型端口驱动程序支持 ndis 6.30 或更高版本的 NDIS，则必须配置网络适配器以检查并筛选指定的 MAC 地址字段。 如果已接收的数据包中有 VLAN 标记，则网络适配器必须将其从数据包数据中删除。 微型端口驱动程序必须将 VLAN 标记放在与数据包的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list)结构相关联的 [**\_ \_ \_ \_ 8021Q \_ 信息**](/windows-hardware/drivers/ddi/nbl8021q/ns-nbl8021q-ndis_net_buffer_list_8021q_info)中。

-   如果过量驱动程序在 [**NDIS \_ 接收 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters) 结构中设置 MAC 地址筛选器和 VLAN 标识符筛选器，则不会在任一筛选器字段中设置 **ndis \_ 接收 \_ 筛选器 \_ 字段 \_ mac \_ 标头 VLAN 无标记 \_ \_ \_ 或 \_ 零** 标志。 在这种情况下，微型端口驱动程序应指示与指定的 MAC 地址和 VLAN 标识符相匹配的数据包。 也就是说，微型端口驱动程序不应指示具有具有零 VLAN 标识符或未标记数据包的匹配 MAC 地址的数据包。

 

