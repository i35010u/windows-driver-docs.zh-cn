---
title: 设置 VMQ 筛选器
description: 设置 VMQ 筛选器
ms.assetid: d40b6806-6ba8-4073-b802-57cb886ffcfb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb9b904525c35af921aa686fe55536a2064bd103
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841951"
---
# <a name="setting-a-vmq-filter"></a>设置 VMQ 筛选器


分配接收队列后，过量驱动程序可以对接收队列设置筛选器。 只有分配有接收队列的驱动程序可以对该队列设置筛选器。

**请注意**  因为默认接收队列（**NDIS\_默认\_接收\_队列\_ID**）始终存在，所以过量驱动程序始终可以在默认队列上设置接收筛选器。 过量驱动程序没有默认队列。 因此，绑定到网络适配器的所有协议驱动程序都可以使用默认队列。

 

## <a name="setting-a-filter-on-a-receive-queue"></a>在接收队列中设置筛选器


如果要使用一组初始配置参数对接收队列设置筛选器，则该驱动程序会发出[OID\_接收\_筛选器\_设置\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)方法对象标识符（OID）请求。 [**Ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员最初包含指向[**NDIS\_接收\_筛选器\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构的指针。 成功从 OID 方法请求返回后， **ndis\_OID\_请求**结构的**InformationBuffer**成员包含指向**NDIS\_接收\_筛选器的指针\_参数**带有新筛选器标识符的结构。

上层驱动程序通过接收队列的下列筛选器配置参数来初始化[**NDIS\_接收\_筛选器\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构：

-   通过 NDIS 指定的筛选器类型[ **\_接收\_筛选器\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_receive_filter_type)枚举值。

    **注意**  从 NDIS 6.20 开始，虚拟机队列（VMQ）接口仅支持**NdisReceiveFilterTypeVMQueue**筛选器类型。

     

-   队列标识符。

-   格式为[**NDIS\_接收\_筛选器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)的一个或多个字段测试参数\_参数结构\_字段。 对于 VMQ，定义了以下字段测试参数。

    -   数据包中的目标媒体访问控制（MAC）地址等于指定的 MAC 地址。

    -   数据包中的虚拟 LAN （VLAN）标识符与指定的 VLAN 标识符相等。

[**NDIS\_接收\_筛选器\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构与 oid 一起使用[\_接收\_筛选器\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-parameters)OID 和[OID\_\_\_集接收\_筛选](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)OID 以指定筛选器的配置参数。

[**NDIS\_接收\_FILTER\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构中的**FieldParametersArrayOffset**、 **FieldParametersArrayNumElements**和**FieldParametersArrayElementSize**成员定义了一个数组，该数组由[**NDIS\_接收\_筛选器\_字段\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)结构。 每个**NDIS\_接收\_筛选器\_字段\_参数**结构在数组中为网络标头中的一个字段设置筛选器测试条件。

[**NDIS\_接收\_FILTER\_字段**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)的**FLAGS**成员\_参数结构指定要为接收筛选器执行的操作。 以下几点适用于**NDIS\_接收\_筛选器\_字段\_MAC\_标头\_VLAN\_未标记\_或\_零**标志：

-   如果**ndis\_接收\_筛选器\_字段\_MAC\_标头\_VLAN**\_在 NDIS\_接收的**Flags**成员中设置\_或\_零标志 @no__t_ [**14_ 筛选器\_字段\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)结构，网络适配器必须仅指示接收的与以下所有测试标准匹配的数据包：

    -   具有匹配 MAC 地址的数据包。

    -   没有 VLAN 标记或 VLAN 标识符为零的数据包。

    如果**NDIS\_接收\_筛选器\_字段\_MAC\_标头\_未标记\_或\_零**标记，则网络适配器不能指示具有匹配 MAC 地址的数据包和非零 VLAN 标识符。

    **请注意**  如果 hyper-v 可扩展交换机设置 MAC 地址筛选器，并且未在[OID\_接收\_筛选](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)器中配置任何 VLAN 标识符筛选器\_设置\_筛选器，则此开关还会设置**NDIS\_接收\_筛选器\_字段\_MAC\_标头\_VLAN\_未标记\_或\_零**标志。

     

-   如果**NDIS\_接收\_筛选器\_字段\_MAC\_标头\_VLAN\_未标记\_或\_零**标志未设置，并且没有 OID 集配置的 VLAN 标识符筛选器[\_接收\_筛选器的 OID 请求\_设置\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)，微型端口驱动程序必须执行下列操作之一：

    -   如果微型端口驱动程序支持 NDIS 6.20，则它必须为[oid\_接收\_filter\_集\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)返回失败的状态。

    -   如果微型端口驱动程序支持 ndis 6.30 或更高版本的 NDIS，则必须配置网络适配器以检查并筛选指定的 MAC 地址字段。 如果已接收的数据包中有 VLAN 标记，则网络适配器必须将其从数据包数据中删除。 微型端口驱动程序必须将 VLAN 标记放在[**NDIS\_NET\_缓冲器\_列表\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_net_buffer_list_8021q_info)与数据包的[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构相关联的 8021Q\_INFO。

-   如果协议驱动程序使用 OID 设置 MAC 地址筛选器和 VLAN 标识符筛选器[\_接收\_筛选器\_设置\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)OID，则不会将**NDIS\_接收\_筛选器\_"字段设置\_MAC\_标头\_VLAN\_无标记\_或**在任一筛选器字段中\_零标志。 在这种情况下，微型端口驱动程序应指示与指定的 MAC 地址和 VLAN 标识符相匹配的数据包。 也就是说，微型端口驱动程序不应指示具有具有零 VLAN 标识符或未标记数据包的匹配 MAC 地址的数据包。

## <a name="using-the-filter-identifier"></a>使用筛选器标识符


NDIS 在[**ndis\_接收\_筛选器\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构的**FilterId**成员中分配筛选器标识符，并传递 oid 的 OID 方法请求[\_接收\_筛选器\_集\_筛选](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)到基础微型端口驱动程序。 在接收队列上设置的每个筛选器都有一个用于网络适配器的唯一筛选器标识符。 也就是说，筛选器标识符不会复制到网络适配器管理的不同队列。

过量驱动程序必须使用 NDIS 在以后 OID 请求中提供的筛选器标识符;例如，修改筛选器参数或释放筛选器。

当 NDIS 接收到在接收队列上设置筛选器的 OID 请求时，它将验证筛选器参数。 在 NDIS 分配所需的资源和筛选器标识符后，它会将 OID 请求提交到基础网络适配器。 如果网络适配器可以成功分配筛选器所需的软件和硬件资源，则它将完成 OID 请求，并将**NDIS\_状态\_SUCCESS**。

微型端口驱动程序必须保留已分配接收筛选器的筛选标识符。 NDIS 使用筛选器的筛选器标识符和更高版本的 OID 请求来更改接收筛选器参数或清除接收筛选器。 有关如何更改参数和清除筛选器的详细信息，请参阅[获取和更新 VM 队列参数](obtaining-and-updating-vm-queue-parameters.md)和[清除 VMQ 筛选器](clearing-a-vmq-filter.md)。

## <a name="handling-the-filter-on-a-receive-queue"></a>处理接收队列中的筛选器


微型端口驱动程序会按照以下方式基于筛选器来计划网络适配器：

-   特定筛选器的所有字段测试参数必须匹配才能将数据包分配给队列。

-   可以在队列中设置多个筛选器。

-   如果有任何筛选器通过，则必须将数据包分配给接收队列。

网络适配器将所有字段测试的结果与逻辑**AND**运算组合在一起。 也就是说，如果在[**NDIS\_接收\_筛选\_器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)的数组中包含的任何字段测试\_参数结构出现故障，则网络数据包不满足指定的筛选条件。

当网络适配器根据这些筛选条件测试接收的数据包时，必须忽略未指定测试条件的数据包中的所有字段。

## <a name="receiving-packets-from-a-receive-queue"></a>接收接收队列中的数据包


在微型端口驱动程序接收[OID 后\_接收\_筛选器\_队列\_分配\_完成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-queue-allocation-complete)请求，并包含在队列中设置的筛选器，队列处于 "*正在运行*" 状态。 当队列处于此状态时，微型端口驱动程序可以指示队列中的数据包。 有关队列状态的详细信息，请参阅[队列状态和操作](queue-states-and-operations.md)。

如果微型端口驱动程序已收到[OID\_接收\_筛选器\_队列\_分配\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-queue-allocation-complete)为队列完成 OID 请求，但没有在队列上设置筛选器，则微型端口驱动程序不得指示任何接收队列中的数据包。 在这种情况下，当微型端口驱动程序收到[OID\_接收\_筛选器\_为队列设置\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)OID 请求，并可能在完成 OID 请求之前，它可以指示队列中的数据包。 如果微型端口驱动程序在处理 OID\_接收\_筛选器\_设置\_筛选器 OID 请求时，在该队列上指示数据包，则微型端口驱动程序必须完成 OID\_\_\_\_具有**NDIS\_状态**的 FILTER 请求\_成功返回代码。

 

 





