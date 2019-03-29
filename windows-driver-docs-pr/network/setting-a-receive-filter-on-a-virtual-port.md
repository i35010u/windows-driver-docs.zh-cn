---
title: 在虚拟端口上设置接收筛选器
description: 在虚拟端口上设置接收筛选器
ms.assetid: F0137D59-1701-4DFC-BB30-27E477FC0706
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47be2c6633368f628e4b3dbfacbdcfd336785c9d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565559"
---
# <a name="setting-a-receive-filter-on-a-virtual-port"></a>在虚拟端口上设置接收筛选器


上创建虚拟端口 (VPort) 后 NIC 交换机的网络适配器，过量驱动程序可以设置接收 VPort 上的筛选器。 创建 VPort 的驱动程序可以设置该 VPort 接收筛选器

本主题包含下列信息：

[设置 VPort 接收筛选器](#set)

[使用 NDIS\_接收\_筛选器\_字段\_MAC\_标头\_VLAN\_UNTAGGED\_或\_零标志](#flag)

[使用筛选器标识符](#filter-id)

[处理接收 VPort 上的筛选器](#handle)

有关如何创建 VPort 的详细信息，请参阅[创建虚拟端口](creating-a-virtual-port.md)。

**请注意**  任何基础驱动程序默认 VPort 始终存在，并且永远不会显式创建，因为可以将接收筛选器设置默认 VPort 上。 基础驱动程序并不拥有默认 VPort。 因此，绑定到的网络适配器的所有协议驱动程序可以都使用默认 VPort。 默认 VPort 具有标识符值的 NDIS\_默认\_VPORT\_id。

 

## <a name="setting-a-receive-filter-on-a-vport"></a>设置 VPort 接收筛选器


若要设置和 VPort 上配置筛选器，基础驱动程序发出的对象标识符 (OID) 方法请求[OID\_接收\_筛选器\_设置\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569795)。 **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构最初包含一个指向[**NDIS\_接收\_筛选器\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567181)结构。

基础驱动程序将发出此 OID 方法请求之前，必须将格式化[ **NDIS\_接收\_筛选器\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567181)结构。 该驱动程序必须按以下方式设置此结构的成员：

-   **FilterType**成员必须设置为[ **NDIS\_接收\_筛选器\_类型**](https://msdn.microsoft.com/library/windows/hardware/ff567186)枚举值。

    **请注意**  仅从 NDIS 6.30 **NdisReceiveFilterTypeVMQueue**单根 I/O 虚拟化 (SR-IOV) 接口支持筛选器类型。

     

-   **QueueId**成员必须设置为 NDIS\_默认\_接收\_队列\_id。

-   **VPortId**成员必须设置为与 VPort 关联的标识符。 基础驱动程序将获取通过以下方式之一的 VPort 标识符：

    -   从上一个 OID 方法请求的[OID\_NIC\_交换机\_创建\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451816)。

    -   从上一个 OID 方法请求的[OID\_NIC\_交换机\_枚举\_VPORTS](https://msdn.microsoft.com/library/windows/hardware/hh451821)。

-   **FilterId**成员必须设置为 NDIS\_默认\_接收\_筛选器\_id。

    **请注意**  NDIS 分配此成员中唯一的筛选器标识符之前其 OID 将请求转发到处理的微型端口驱动程序。

     

-   **FieldParametersArrayOffset**， **FieldParametersArrayNumElements**，并**FieldParametersArrayElementSize**的成员[ **NDIS\_接收\_筛选器\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567181)结构必须正确设置，以定义数组[ **NDIS\_接收\_筛选器\_字段\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567169)结构。 每个**NDIS\_接收\_筛选器\_域\_参数**结构数组中的网络标头中设置一个字段的筛选器测试条件。

    对于 SR-IOV 接口中，定义以下字段测试参数：

    -   在包中的目标媒体访问控制 (MAC) 地址等于指定的 MAC 地址。

    -   在包中的虚拟 LAN (VLAN) 标识符等于指定的 VLAN 标识符。

通过 OID 方法请求成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_接收\_筛选器\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567181)结构与新的筛选器标识符。

## <a name="using-the-ndisreceivefilterfieldmacheadervlanuntaggedorzero-flag"></a>使用 NDIS\_接收\_筛选器\_字段\_MAC\_标头\_VLAN\_UNTAGGED\_或\_零标志


**标志**的成员[ **NDIS\_接收\_筛选器\_字段\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567169)结构指定为接收筛选器执行的操作。 以下几点适用于**NDIS\_接收\_筛选器\_域\_MAC\_标头\_VLAN\_UNTAGGED\_或\_零**标志：

-   如果**NDIS\_接收\_筛选器\_域\_MAC\_标头\_VLAN\_UNTAGGED\_或\_零**中设置了标志**标志**成员，网络适配器必须指示只有与所有以下测试条件匹配的接收的数据包：

    -   MAC 地址匹配数据包。

    -   数据包没有 VLAN 标记或包含零为 VLAN 标识符。

    如果**NDIS\_接收\_筛选器\_域\_MAC\_标头\_VLAN\_UNTAGGED\_或\_零**设置标志，则网络适配器必须指示具有匹配的 MAC 地址和非零的 VLAN 标识符的数据包。

    **请注意**  如果虚拟化堆栈设置 MAC 地址筛选器，且没有 VLAN 标识符筛选器由配置[OID\_接收\_筛选器\_设置\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569795)集还设置请求，该交换机**NDIS\_接收\_筛选器\_字段\_MAC\_标头\_VLAN\_无标记\_或者\_零**标志。

     

-   如果使用 NDIS 6.30，启动**NDIS\_接收\_筛选器\_域\_MAC\_标头\_VLAN\_UNTAGGED\_或\_零**未设置标志，并且不没有配置的任何 VLAN 标识符筛选器[OID\_接收\_筛选器\_设置\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569795)方法请求微型端口驱动程序必须执行以下任一操作：

    -   微型端口驱动程序必须返回的失败状态[OID\_接收\_筛选器\_设置\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569795)方法请求。

    -   微型端口驱动程序必须配置网络适配器，以检查并筛选指定的 MAC 地址字段。 如果接收到的数据包中存在的 VLAN 标记，则网络适配器必须从数据包数据中删除它。 微型端口驱动程序必须将 VLAN 标记放在[ **NDIS\_NET\_缓冲区\_列表\_8021Q\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff566565)关联数据包[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构。

-   如果协议驱动程序设置 MAC 地址筛选器和具有的 VLAN 标识符筛选器[OID\_接收\_筛选器\_设置\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569795)方法请求，它不会设置**NDIS\_接收\_筛选器\_字段\_MAC\_标头\_VLAN\_UNTAGGED\_或者\_零**中的筛选器字段中的标记。 在这种情况下，微型端口驱动程序应指示指定的 MAC 地址和 VLAN 标识符匹配的数据包。 也就是说，微型端口驱动程序不应指示具有匹配的 MAC 地址的数据包的零个 VLAN 标识符，或者已无标记的数据包。

## <a name="using-the-filter-identifier"></a>使用筛选器标识符


NDIS 分配中的筛选器标识符**FilterId**的成员[ **NDIS\_接收\_筛选器\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567181)结构，并将传递的 OID 方法请求[OID\_接收\_筛选器\_设置\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569795)为基础的微型端口驱动程序。 VPort 设置每个筛选器具有唯一的筛选器标识符为网络适配器。 也就是说，筛选器标识符未在不同的队列，用于管理网络适配器上复制。

基础驱动程序必须使用筛选器标识符 NDIS 提供更高版本的 OID 的请求以更改筛选器参数或免费筛选器。

当 NDIS 收到 OID 请求 VPort 上设置筛选器时，它会验证筛选器参数。 NDIS 分配所需的资源和筛选器标识符后，它将提交到基础的网络适配器的 OID 请求。 如果网络适配器能够成功地分配必要的软件和硬件资源的筛选器，完成时具有的 OID 请求**NDIS\_状态\_成功**。

微型端口驱动程序必须保留已分配的接收筛选器的筛选器标识符。 NDIS 与更高版本的 OID 请求使用筛选器的筛选器的标识符，若要更改接收筛选器参数或清除接收筛选器。 有关如何更改参数时，清除筛选器的详细信息，请参阅[Obtaining 和更新虚拟机队列参数](obtaining-and-updating-vm-queue-parameters.md)并[清除 VMQ 筛选器](clearing-a-vmq-filter.md)。

## <a name="handling-receive-filters-on-a-vport"></a>处理接收 VPort 上的筛选器


微型端口驱动程序基于如下所示的筛选器的网络适配器：

-   必须匹配特定筛选器的所有字段测试参数才能将数据包分配给 VPort。

-   可以在 VPort 上设置多个筛选器。

-   如果传递任何筛选器，必须将数据包分配给 VPort。

网络适配器将从所有字段测试结果与逻辑组合**AND**操作。 也就是说，如果任何字段测试包含在的数组[ **NDIS\_接收\_筛选器\_字段\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567169)结构失败，网络数据包不符合指定的筛选器条件。

网络适配器测试后对这些筛选器条件接收的数据包，它必须忽略数据包中没有指定的测试条件的所有字段。

 

 





