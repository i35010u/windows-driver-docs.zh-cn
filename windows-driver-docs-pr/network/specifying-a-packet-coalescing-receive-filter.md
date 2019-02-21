---
title: 指定数据包合并接收筛选器
description: 指定数据包合并接收筛选器
ms.assetid: 0369A63D-4CDE-448A-8472-EEEB7B859B8D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 384e3acaeecaf2f7730dd854ee4e352f964bfe67
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544274"
---
# <a name="specifying-a-packet-coalescing-receive-filter"></a>指定数据包合并接收筛选器


基础驱动程序可以设置一个或多个接收支持 NDIS 数据包合并微型端口驱动程序筛选器。 基础驱动程序可以指定最大数量的微型端口驱动程序中指定的接收筛选器**MaxPacketCoalescingFilters**的成员[ **NDIS\_接收\_筛选器\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)结构。

**请注意**  过量协议驱动程序将获取[ **NDIS\_接收\_筛选器\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)结构中[ **NDIS\_绑定\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff564832)结构。 基础筛选器驱动程序将获取**NDIS\_接收\_筛选器\_功能**结构内[ **NDIS\_筛选器\_ATTACH\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff565481)结构。

 

过量的驱动程序下载到微型端口驱动程序筛选器接收通过发出的 OID 方法请求[OID\_接收\_筛选器\_设置\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569795)。 **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构为此 OID 请求包含的指针调用方分配的缓冲区。 此缓冲区已格式化为包含以下信息：

-   [ **NDIS\_接收\_筛选器\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567181) ndis 指定的参数的结构接收筛选器。

    有关如何初始化此结构的详细信息，请参阅[指定一个接收筛选器](#specifying-receive-filter)。

-   一个数组[ **NDIS\_接收\_筛选器\_字段\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567169)结构指定的筛选器测试条件中的字段网络数据包标头。

    有关如何初始化这些结构的详细信息，请参阅[指定标头字段测试](#specifying-header-field-test)。

## <a name="specifying-a-receive-filter"></a>指定接收筛选器


基础驱动程序指定数据包合并筛选器接收通过初始化[ **NDIS\_接收\_筛选器\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567181)结构筛选器的配置参数。 当它初始化**NDIS\_接收\_筛选器\_参数**结构，基础驱动程序必须遵循下列规则：

-   **FilterType**成员必须设置为[ **NDIS\_接收\_筛选器\_类型**](https://msdn.microsoft.com/library/windows/hardware/ff567186)枚举值的**NdisReceiveFilterTypePacketCoalescing**。

-   **QueueId**成员必须设置为 NDIS\_默认\_接收\_队列\_id。

    **请注意**  从 NDIS 6.30 开始，数据包合并接收筛选器仅支持在默认接收的网络适配器的队列。 此接收队列具有的 NDIS 标识符\_默认\_接收\_队列\_id。

     

-   如果基础驱动程序创建新的接收筛选器，它必须设置**FilterId**成员添加到 NDIS\_默认\_接收\_筛选器\_id。

    **请注意**  NDIS 将为接收筛选器生成唯一的筛选器标识符 (ID)，将转发的 OID 方法请求之前[OID\_接收\_筛选器\_集\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569795)微型端口驱动程序。     

-  如果基础驱动程序正在修改现有的接收筛选器，它必须设置**FilterId**成员添加到接收筛选器的非零值的筛选器 ID。 基础驱动程序时它所颁发的 OID 方法请求获取接收筛选器的筛选器 ID [OID\_接收\_筛选器\_枚举\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569787)。 有关如何修改接收筛选器的详细信息，请参阅[修改数据包合并接收筛选器](modifying-packet-coalescing-receive-filters.md)。

-   **FieldParametersArrayOffset**， **FieldParametersArrayNumElements**，并**FieldParametersArrayElementSize**的成员[ **NDIS\_接收\_筛选器\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567181)结构必须设置为定义字段参数的数组。 数组中的每个元素均[ **NDIS\_接收\_筛选器\_字段\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567169)结构，它指定为标头的参数字段的接收筛选器的测试。

-   **RequestedFilterIdBitCount**成员必须设置为零。

-   **MaxCoalescingDelay**保存并合并上的网络适配器与接收筛选器匹配的第一个数据包必须设置为最大的时间，以毫秒为单位。 一旦收到第一个数据包与筛选器匹配时，网络适配器将合并数据包并将启动其过期时间设置的值为一个硬件计时器**MaxCoalescingDelay**成员。

基础驱动程序必须对标头字段测试字段参数数组中的相关联的 MAC 和协议标头将在包中存在的相同顺序中进行排序。

例如，在基础驱动程序指定的筛选器参数的 IP 版本 4 (IPv4) 协议字段，它必须首先指定一个 MAC 标头协议字段 (NdisMacHeaderFieldProtocol) 的筛选器参数。 以这种方式，该驱动程序指定的标头字段测试，验证该字段设置为 IPv4 数据包的正确 EtherType 值 (0x0800)。 如果测试失败，不必执行 IPV4 协议字段的测试适配器。

## <a name="specifying-header-field-tests"></a>指定标头字段测试


每个接收筛选器可以指定一个或多个测试条件 (*标头字段测试*)。 网络适配器执行这些测试，以确定是否应在适配器上的硬件合并缓冲区中合并接收的数据包。 此外，基础驱动程序可以指定单独的筛选器测试的各种媒体访问控制 (MAC)、 IP 版本 4 (IPv4) 和 IP 版本 6 (IPv6) 的标头字段。

若要优化的网络适配器上的筛选，标头字段测试基于标准化标头字段名称而不是在数据包数据中的字节偏移量/长度规范。 通过使用标头/字段名称时，网络适配器的硬件或固件将可以优化如何将多个标头字段测试执行上接收的数据包。

每个接收筛选器可以包含一个或多个标头字段测试指定的[ **NDIS\_接收\_筛选器\_字段\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567169)结构。 每个**NDIS\_接收\_筛选器\_域\_参数**结构是引用的字段参数数组的元素**FieldParametersArrayOffset**， **FieldParametersArrayNumElements**，和**FieldParametersArrayElementSize**成员[ **NDIS\_接收\_筛选器\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567181)结构。

微型端口驱动程序必须处理的 OID 方法请求时请遵循以下准则[OID\_接收\_筛选器\_设置\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569795):

-   如果**NDIS\_接收\_筛选器\_域\_MAC\_标头\_VLAN\_UNTAGGED\_或\_零**中设置了标志**标志**的成员[ **NDIS\_接收\_筛选器\_字段\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567169)结构，网络适配器必须仅指示接收到具有匹配的 MAC 地址和无标记的数据包的数据包或数据包，其中零为 VLAN 标识符。 也就是说，网络适配器必须指示具有匹配的 MAC 地址和一个非零的 VLAN 标识符的数据包。

-   如果**NDIS\_接收\_筛选器\_域\_MAC\_标头\_VLAN\_UNTAGGED\_或\_零**未设置标志，并且不没有配置由 OID 集请求的任何 VLAN 标识符筛选器[OID\_接收\_筛选器\_设置\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569795)，微型端口驱动程序必须执行下列任一操作：

    -   如果微型端口驱动程序支持 NDIS 6.20，它必须返回失败的状态的 OID 请求[OID\_接收\_筛选器\_设置\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569795)。

    -   如果微型端口驱动程序支持 NDIS 6.30 和更高版本的 NDIS，它必须配置网络适配器，以检查并筛选指定的 MAC 地址字段。 如果接收到的数据包中存在的 VLAN 标记，则网络适配器必须从数据包数据中删除它。 微型端口驱动程序必须将 VLAN 标记放在[ **NDIS\_NET\_缓冲区\_列表\_8021Q\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff566565)关联数据包[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构。

-   如果基础驱动程序设置 MAC 地址筛选器和中的 VLAN 标识符筛选器[ **NDIS\_接收\_筛选器\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567181)结构，它不会设置**NDIS\_接收\_筛选器\_域\_MAC\_标头\_VLAN\_UNTAGGED\_或\_零**任一筛选器字段中的标志。 在这种情况下，微型端口驱动程序应指示指定的 MAC 地址和 VLAN 标识符匹配的数据包。 也就是说，微型端口驱动程序不应指示具有匹配的 MAC 地址的数据包的零个 VLAN 标识符，或者已无标记的数据包。

 

 





