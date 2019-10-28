---
title: 指定数据包合并接收筛选器
description: 指定数据包合并接收筛选器
ms.assetid: 0369A63D-4CDE-448A-8472-EEEB7B859B8D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: acf4455ee98b9827555743e52a20e0ba8c3a00f1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841874"
---
# <a name="specifying-a-packet-coalescing-receive-filter"></a>指定数据包合并接收筛选器


过量驱动程序可以在支持 NDIS 数据包合并的微型端口驱动程序上设置一个或多个接收筛选器。 过量驱动程序最多可以指定在 NDIS\_的**MaxPacketCoalescingFilters**成员中指定的最大接收筛选器数[ **\_筛选\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构。

**请注意**  过量协议驱动程序在[**ndis\_绑定\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)结构中获取[**NDIS\_接收\_筛选器\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构。 过量筛选器驱动程序获取**ndis\_接收\_筛选**器中的\_功能结构[ **\_，\_附加\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)结构。

 

过量驱动程序通过发出 oid [\_接收\_FILTER\_集\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)来向微型端口驱动程序下载接收筛选器。 此 OID 请求[ **\_请求结构的 NDIS\_OID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)的**InformationBuffer**成员包含指向调用方分配的缓冲区的指针。 此缓冲区的格式设置为包含以下内容：

-   [**Ndis\_接收\_筛选器，\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构，用于指定 NDIS 接收筛选器的参数。

    有关如何初始化此结构的详细信息，请参阅[指定接收筛选器](#specifying-a-receive-filter)。

-   一组[**NDIS\_接收\_筛选器\_字段\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)结构，后者指定网络数据包标头中的字段的筛选器测试条件。

    有关如何初始化这些结构的详细信息，请参阅[指定标头字段测试](#specifying-header-field-tests)。

## <a name="specifying-a-receive-filter"></a>指定接收筛选器


过量驱动程序通过使用筛选器的配置参数初始化[**NDIS\_接收\_筛选器\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构来指定数据包合并接收筛选器。 初始化**NDIS\_接收\_筛选器\_参数**结构时，过量驱动程序必须遵循以下规则：

-   必须将**FilterType**成员设置为[**NDIS\_接收\_筛选器\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_receive_filter_type)枚举值为**NdisReceiveFilterTypePacketCoalescing**。

-   **QueueId**成员必须设置为 NDIS\_默认\_接收\_队列\_ID。

    **注意**  从 NDIS 6.30 开始，仅在网络适配器的默认接收队列中支持数据包合并接收筛选器。 此接收队列具有 NDIS\_默认\_接收\_队列\_ID 的标识符。

     

-   如果过量驱动程序正在创建新的接收筛选器，则必须将**FilterId**成员设置为 NDIS\_默认\_接收\_筛选器\_ID。

    **请注意**  NDIS 将为接收筛选器生成唯一筛选器标识符（ID），然后再将 OID 的 oid 方法请求[\_接收\_筛选器\_将\_筛选器设置](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)为微型端口驱动程序。     

-  如果过量驱动程序正在修改现有的接收筛选器，则必须将**FilterId**成员设置为接收筛选器的非零筛选器 ID。 当过量驱动程序发出 Oid 的 OID 方法请求（ [\_接收\_filter\_枚举\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)）时，将获取接收筛选器的筛选器 ID。 有关如何修改接收筛选器的详细信息，请参阅[修改包合并接收筛选器](modifying-packet-coalescing-receive-filters.md)。

-   必须将[**NDIS\_接收\_筛选\_器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)的**FieldParametersArrayOffset**、 **FieldParametersArrayNumElements**和**FieldParametersArrayElementSize**成员设置为定义字段参数的数组。 数组中的每个元素都是一个[**NDIS\_接收\_筛选器\_字段\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)结构，用于指定接收筛选器的标头字段测试的参数。

-   **RequestedFilterIdBitCount**成员必须设置为零。

-   **MaxCoalescingDelay**必须设置为与接收筛选器匹配的第一个数据包在网络适配器上保存并合并的最长时间（以毫秒为单位）。 一旦收到第一个与筛选器匹配的数据包，网络适配器就会将数据包合并，并启动一个将过期时间设置为**MaxCoalescingDelay**成员值的硬件计时器。

过量驱动程序必须对字段参数数组中的标头字段测试进行排序，使其顺序与关联 MAC 和协议标头在数据包中的顺序相同。

例如，在过量驱动程序为 IP 版本4（IPv4）协议字段指定筛选器参数之前，必须先为 MAC 标头协议字段指定筛选器参数（NdisMacHeaderFieldProtocol）。 通过这种方式，驱动程序将指定一个标头字段测试，用于验证是否将该字段设置为 IPv4 数据包的正确 EtherType 值（0x0800）。 如果测试失败，则适配器不需要执行 IPV4 协议字段的测试。

## <a name="specifying-header-field-tests"></a>指定标头字段测试


每个接收筛选器都可以指定一个或多个测试条件（*标头字段测试*）。 网络适配器执行这些测试来确定是否应将接收的数据包合并到适配器上的硬件合并缓冲器中。 而且，过量驱动程序可以为各种媒体访问控制（MAC）、IP 版本4（IPv4）和 IP 版本6（IPv6）标头字段指定单独的筛选器测试。

为了优化网络适配器上的筛选，标头字段测试基于标准化标头字段名称，而不是数据包数据中的字节偏移量/长度规范。 通过使用标头/字段名称，网络适配器的硬件或固件可以优化多个标头字段测试在收到的数据包上的执行方式。

每个接收筛选器都可以包含一个或多个由 NDIS 指定的标头字段测试[ **\_接收\_筛选器\_字段\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)结构。 每个**NDIS\_接收\_筛选器\_字段\_参数**结构是**FieldParametersArrayOffset**、 **FieldParametersArrayNumElements**引用的字段参数数组的元素。和**FieldParametersArrayElementSize** [**NDIS\_接收\_FILTER\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构的成员。

小型端口驱动程序在处理 Oid 的 OID 方法请求时必须遵循这些准则[\_接收\_filter\_集\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)：

-   如果**ndis\_接收\_筛选器\_字段\_MAC\_标头\_VLAN**\_在 NDIS\_接收的**Flags**成员中设置\_或\_零标志 @no__t_ [**14_ 筛选器\_字段\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)结构，网络适配器必须仅指示具有匹配的 MAC 地址的接收数据包和未标记的数据包或 VLAN 标识符为零的数据包。\_ 也就是说，网络适配器不能指示具有匹配 MAC 地址和非零 VLAN 标识符的数据包。

-   如果**NDIS\_接收\_筛选器\_字段\_MAC\_标头\_VLAN\_未标记\_或\_零**标志未设置，并且没有 OID 集配置的 VLAN 标识符筛选器[\_接收\_筛选器的 OID 请求\_设置\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)，微型端口驱动程序必须执行下列操作之一：

    -   如果微型端口驱动程序支持 NDIS 6.20，则它必须为[oid\_接收\_filter\_集\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)返回失败的状态。

    -   如果微型端口驱动程序支持 ndis 6.30 或更高版本的 NDIS，则必须配置网络适配器以检查并筛选指定的 MAC 地址字段。 如果已接收的数据包中有 VLAN 标记，则网络适配器必须将其从数据包数据中删除。 微型端口驱动程序必须将 VLAN 标记放在[**NDIS\_NET\_缓冲器\_列表\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_net_buffer_list_8021q_info)与数据包的[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构相关联的 8021Q\_INFO。

-   如果过量驱动程序在[**NDIS\_接收\_筛选器\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构中设置 MAC 地址筛选器和 VLAN 标识符筛选器，则不会将**ndis\_接收\_筛选器\_\_MAC\_标头\_VLAN\_** 任何筛选器字段中的未标记\_或\_零标志。 在这种情况下，微型端口驱动程序应指示与指定的 MAC 地址和 VLAN 标识符相匹配的数据包。 也就是说，微型端口驱动程序不应指示具有具有零 VLAN 标识符或未标记数据包的匹配 MAC 地址的数据包。

 

 





