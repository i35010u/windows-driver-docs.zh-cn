---
title: 设置 VMQ 筛选器
description: 设置 VMQ 筛选器
ms.assetid: d40b6806-6ba8-4073-b802-57cb886ffcfb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da692ecad229f9aa87d9a288db66573faf1badda
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346676"
---
# <a name="setting-a-vmq-filter"></a>设置 VMQ 筛选器


接收队列分配后，过量驱动程序可以设置在接收队列上的筛选器。 分配接收队列的驱动程序可以在该队列上设置筛选器。

**请注意**  因为默认接收队列 (**NDIS\_默认\_接收\_队列\_ID**) 始终存在，过量驱动程序也可以随时设置接收默认的队列上的筛选器。 基础驱动程序并不拥有默认队列。 因此，绑定到的网络适配器的所有协议驱动程序可以都使用默认的队列。

 

## <a name="setting-a-filter-on-a-receive-queue"></a>在接收队列上设置筛选器


若要设置的配置参数最初的一接收队列筛选器，基础驱动程序将发出[OID\_接收\_筛选器\_设置\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569795)方法对象标识符 (OID) 的请求。 **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构最初包含一个指向[**NDIS\_接收\_筛选器\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567181)结构。 通过 OID 方法请求成功返回后**InformationBuffer**的成员**NDIS\_OID\_请求**结构包含一个指向**NDIS\_接收\_筛选器\_参数**结构与新的筛选器标识符。

基础驱动程序初始化[ **NDIS\_接收\_筛选器\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567181)结构的以下筛选器配置参数接收队列：

-   通过指定的筛选器类型[ **NDIS\_接收\_筛选器\_类型**](https://msdn.microsoft.com/library/windows/hardware/ff567186)枚举值。

    **请注意**  仅从 NDIS 6.20 **NdisReceiveFilterTypeVMQueue**虚拟机队列 (VMQ) 接口支持筛选器类型。

     

-   队列标识符。

-   将格式化的一个或多个字段测试参数[ **NDIS\_接收\_筛选器\_字段\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567169)结构。 对于 VMQ，定义以下字段测试参数。

    -   在包中的目标媒体访问控制 (MAC) 地址等于指定的 MAC 地址。

    -   在包中的虚拟 LAN (VLAN) 标识符等于指定的 VLAN 标识符。

[ **NDIS\_接收\_筛选器\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567181)结构用于[OID\_接收\_筛选器\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569792)OID 并[OID\_接收\_筛选器\_设置\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569795)OID 来指定的配置参数筛选器。

**FieldParametersArrayOffset**， **FieldParametersArrayNumElements**，并**FieldParametersArrayElementSize**的成员[ **NDIS\_接收\_筛选器\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567181)结构定义的一个数组[ **NDIS\_接收\_筛选器\_字段\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567169)结构。 每个**NDIS\_接收\_筛选器\_域\_参数**结构数组中的网络标头中设置一个字段的筛选器测试条件。

**标志**的成员[ **NDIS\_接收\_筛选器\_字段\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567169)结构指定为接收筛选器执行的操作。 以下几点适用于**NDIS\_接收\_筛选器\_域\_MAC\_标头\_VLAN\_UNTAGGED\_或\_零**标志：

-   如果**NDIS\_接收\_筛选器\_域\_MAC\_标头\_VLAN\_UNTAGGED\_或\_零**中设置了标志**标志**的成员[ **NDIS\_接收\_筛选器\_字段\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567169)结构，网络适配器必须指示只有与所有以下测试条件匹配的接收的数据包：

    -   MAC 地址匹配数据包。

    -   数据包没有 VLAN 标记或包含零为 VLAN 标识符。

    如果**NDIS\_接收\_筛选器\_域\_MAC\_标头\_VLAN\_UNTAGGED\_或\_零**设置标志，则网络适配器必须指示具有匹配的 MAC 地址和非零的 VLAN 标识符的数据包。

    **请注意**  如果 HYPER-V 可扩展交换机设置 MAC 地址筛选器，且没有 VLAN 标识符筛选器中配置[OID\_接收\_筛选器\_设置\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569795)，还会设置此开关**NDIS\_接收\_筛选器\_字段\_MAC\_标头\_VLAN\_UNTAGGED\_或者\_零**标志。

     

-   如果**NDIS\_接收\_筛选器\_域\_MAC\_标头\_VLAN\_UNTAGGED\_或\_零**未设置标志，并且不没有配置由 OID 集请求的任何 VLAN 标识符筛选器[OID\_接收\_筛选器\_设置\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569795)，微型端口驱动程序必须执行下列任一操作：

    -   如果微型端口驱动程序支持 NDIS 6.20，它必须返回失败的状态的 OID 请求[OID\_接收\_筛选器\_设置\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569795)。

    -   如果微型端口驱动程序支持 NDIS 6.30 和更高版本的 NDIS，它必须配置网络适配器，以检查并筛选指定的 MAC 地址字段。 如果接收到的数据包中存在的 VLAN 标记，则网络适配器必须从数据包数据中删除它。 微型端口驱动程序必须将 VLAN 标记放在[ **NDIS\_NET\_缓冲区\_列表\_8021Q\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff566565)关联数据包[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构。

-   如果协议驱动程序设置 MAC 地址筛选器和具有的 VLAN 标识符筛选器[OID\_接收\_筛选器\_设置\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569795)OID，它不会设置**NDIS\_接收\_筛选器\_字段\_MAC\_标头\_VLAN\_UNTAGGED\_或者\_零**标记中筛选器字段之一。 在这种情况下，微型端口驱动程序应指示指定的 MAC 地址和 VLAN 标识符匹配的数据包。 也就是说，微型端口驱动程序不应指示具有匹配的 MAC 地址的数据包的零个 VLAN 标识符，或者已无标记的数据包。

## <a name="using-the-filter-identifier"></a>使用筛选器标识符


NDIS 分配中的筛选器标识符**FilterId**的成员[ **NDIS\_接收\_筛选器\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567181)结构，并将传递的 OID 方法请求[OID\_接收\_筛选器\_设置\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569795)为基础的微型端口驱动程序。 在接收队列设置每个筛选器具有唯一的筛选器标识符为网络适配器。 也就是说，筛选器标识符未在不同的队列，用于管理网络适配器上复制。

基础驱动程序必须使用 NDIS 提供更高版本的 OID 请求; 中的筛选器标识符例如，若要修改筛选器参数，或以释放一个筛选器。

当 NDIS 收到 OID 请求接收队列上设置筛选器时，它会验证筛选器参数。 NDIS 分配所需的资源和筛选器标识符后，它将提交到基础的网络适配器的 OID 请求。 如果网络适配器能够成功地分配必要的软件和硬件资源的筛选器，完成时具有的 OID 请求**NDIS\_状态\_成功**。

微型端口驱动程序必须保留已分配的接收筛选器的筛选器标识符。 NDIS 使用更高版本的 OID 请求以更改接收筛选器参数或清除接收筛选器的筛选器的筛选器标识符。 有关如何更改参数时，清除筛选器的详细信息，请参阅[Obtaining 和更新虚拟机队列参数](obtaining-and-updating-vm-queue-parameters.md)并[清除 VMQ 筛选器](clearing-a-vmq-filter.md)。

## <a name="handling-the-filter-on-a-receive-queue"></a>处理接收队列上的筛选器


微型端口驱动程序基于如下所示的筛选器的网络适配器：

-   为了将数据包分配给该队列必须匹配特定筛选器的所有字段测试参数。

-   可以在队列上设置多个筛选器。

-   如果传递任何筛选器，必须将数据包分配给接收队列。

网络适配器将从所有字段测试结果与逻辑组合**AND**操作。 也就是说，如果任何字段测试包含在的数组[ **NDIS\_接收\_筛选器\_字段\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567169)结构失败，网络数据包不符合指定的筛选器条件。

网络适配器测试后对这些筛选器条件接收的数据包，它必须忽略数据包中没有指定的测试条件的所有字段。

## <a name="receiving-packets-from-a-receive-queue"></a>接收队列中接收数据包


后微型端口驱动程序收到[OID\_接收\_筛选器\_队列\_分配\_完成](https://msdn.microsoft.com/library/windows/hardware/ff569793)请求且具有队列设置的筛选器，队列是在中*运行*状态。 此状态队列时，微型端口驱动程序可以指示队列上的数据包。 队列状态的详细信息，请参阅[队列状态和操作](queue-states-and-operations.md)。

如果微型端口驱动程序已收到[OID\_接收\_筛选器\_队列\_分配\_完成](https://msdn.microsoft.com/library/windows/hardware/ff569793)OID 请求队列，但在没有筛选器设置队列，微型端口驱动程序必须指示任何接收该队列上的数据包。 在这种情况下，当微型端口驱动程序收到[OID\_接收\_筛选器\_设置\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569795)OID 请求队列，并可能在完成 OID 请求之前，它可以指示该队列上的数据包。 如果正在进行的 OID，微型端口驱动程序将指示队列上的数据包\_接收\_筛选器\_设置\_请求筛选器 OID，微型端口驱动程序必须完成 OID\_接收\_筛选器\_设置\_筛选器请求具有**NDIS\_状态\_成功**返回代码。

 

 





