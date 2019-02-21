---
title: OID_SWITCH_NIC_REQUEST
description: 对象标识符 (OID) 方法请求的 OID_SWITCH_NIC_REQUEST 用于封装和 OID 请求转发到 HYPER-V 可扩展交换机外部网络适配器。
ms.assetid: 7EF4D950-D18E-400A-B1DD-39768A16E4C4
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_NIC_REQUEST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: dce1228aa7cbbdb554536ed635b8eb69f09f15b5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541283"
---
# <a name="oidswitchnicrequest"></a>OID\_交换机\_NIC\_请求


对象标识符 (OID) 方法请求的 OID\_切换\_NIC\_请求用于封装和 OID 请求转发到 HYPER-V 可扩展交换机外部网络适配器。 这允许传递到绑定到外部网络适配器的基础物理网络适配器的驱动程序封装的 OID 请求。

此 OID 请求还用于封装 OID 请求颁发给已连接到可扩展交换机端口的其他网络适配器。 在这种情况下，封装 OID 将该请求转发通过检查可扩展交换机驱动程序堆栈的扩展。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_交换机\_NIC\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/hh598214)结构。 此结构指定 OID 请求转发的信息。 此结构还包含指向原始的指针**NDIS\_OID\_请求**转发 OID 请求的结构。

<a name="remarks"></a>备注
-------

当 OID 请求到达的 HYPER-V 可扩展交换机接口时，它封装它们才能转发可扩展交换机控制路径下。 这些 OID 请求包括：

-   硬件卸载 OID 请求，包括 Internet 协议安全 (IPsec)、 虚拟机队列 (VMQ) 和单个根 I/O 虚拟化 (SR-IOV) 的请求。 这些 OID 请求颁发的基础协议或管理操作系统的 HYPER-V 父分区中运行的筛选器驱动程序。

    当这些 OID 请求在可扩展交换机接口，可扩展交换机的协议边缘封装 OID 请求内的[ **NDIS\_切换\_NIC\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/hh598214)结构。 协议边缘按以下方式设置此结构的成员：

    -   **DestinationPortId**并**DestinationNicIndex**成员设置为外部网络适配器的相应值。

    -   如果从 HYPER-V 子分区中，已发出 OID 请求**SourcePortId**并**SourceNicIndex**成员设置为使用的端口和网络适配器的相应值分区。 否则为**SourcePortId**并**SourceNicIndex**成员设置为零。

        **请注意**扩展必须保留这些成员的值，如果它转发或 OID 请求重定向。



    -   **OidRequest**成员设置为指向的指针[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)封装 OID 请求的结构。

    协议边缘然后发出 OID\_切换\_NIC\_请求请求下可扩展交换机控制路径将封装的 OID 请求转发到外部网络适配器。

    基础的转发扩展可以封装的硬件卸载 OID 请求重定向到绑定到外部网络适配器的物理网络适配器。 例如，如果该扩展支持来自可扩展交换机团队均绑定到外部网络适配器的物理网络适配器，它可以转发 OID\_切换\_NIC\_请求中的物理适配器的请求负载平衡故障转移 (LBFO) 组支持硬件的卸载。 此过程的详细信息，请参阅[管理硬件卸载 OID 请求到物理网络适配器](https://msdn.microsoft.com/library/windows/hardware/hh598194)。

    有关可扩展交换机团队详细信息，请参阅[的物理网络适配器配置的类型](https://msdn.microsoft.com/library/windows/hardware/hh582274)。

-   多播的 OID 请求，包括[OID\_802\_3\_添加\_多播\_地址](oid-802-3-add-multicast-address.md)并[OID\_802\_3\_删除\_多播\_地址](oid-802-3-delete-multicast-address.md)。 这些 OID 请求颁发的基础协议和在管理操作系统或 HYPER-V 子分区的来宾操作系统中运行的筛选器驱动程序。

    当这些 OID 请求在可扩展交换机接口，可扩展交换机的协议边缘封装 OID 请求内的[ **NDIS\_切换\_NIC\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/hh598214)结构。 此外设置协议边缘**SourcePortId**并**SourceNicIndex** OID 请求所源自的端口和网络适配器的相应值的成员。 协议边缘然后发出 OID\_切换\_NIC\_请求请求下检查可扩展交换机控制路径将封装的 OID 请求转发基础扩展插件。

    **请注意**这种情况下，设置协议边缘**DestinationPortId**并**DestinationNicIndex**为零的成员。 这指定封装的 OID 请求是要传递到中的控制路径的扩展。

    基础转发扩展可以检查这些封装的 OID 请求并保留他们指定的多播的地址信息。 例如，该扩展可能需要此信息，如果它源自其转发到可扩展交换机端口的多路广播的数据包。

    有关详细信息，请参阅[转发来自 HYPER-V 子分区的 OID 请求](https://msdn.microsoft.com/library/windows/hardware/hh598150)。

转发扩展还可以颁发 OID\_交换机\_NIC\_请求，以便转发封装到绑定到外部网络适配器的物理网络适配器的 OID 请求。 这样，源自其自身的 OID 请求或将现有的 OID 请求重定向到绑定到外部网络适配器的物理网络适配器的扩展。 若要执行此操作，该扩展必须执行以下步骤：

1.  扩展调用[ *ReferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598294)递增引用计数器，用于目标物理网络适配器的索引。 这可以保证可扩展交换机接口不会删除物理网络适配器连接时它的引用计数器为非零值。

    **请注意**其引用计数器为非零值时，可扩展交换机接口无法断开连接的物理网络适配器连接。 有关详细信息，请参阅[HYPER-V 可扩展交换机端口和网络适配器状态](https://msdn.microsoft.com/library/windows/hardware/hh598182)。

2.  扩展方法为： 初始化封装 OID 请求[ **NDIS\_交换机\_NIC\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/hh598214)结构如下所示：

    -   **DestinationPortId**成员必须设置为外部网络适配器连接到可扩展的交换机端口的标识符。
    -   **DestinationNicIndex**成员必须设置为非零的索引值的基础物理网络适配器。
    -   如果扩展代表 HYPER-V 子分区中，发起**SourcePortId**并**SourceNicIndex**成员设置为使用的端口和网络适配器的相应值分区。 否则为**SourcePortId**并**SourceNicIndex**成员设置为零。

        例如，如果扩展管理子分区的硬件卸载资源，它必须设置**SourcePortId**并**SourceNicIndex**成员，以指定要对哪个分区封装硬件卸载 OID 请求针对的是。

    -   **OidRequest**成员必须设置为指向一个已初始化的指针[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)封装 OID 请求的结构.

3.  扩展调用[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830) OID 请求转发到指定的目标可扩展交换机端口和网络适配器。

4.  当调用 NDIS [ *FilterOidRequestComplete* ](https://msdn.microsoft.com/library/windows/hardware/ff549956)函数，扩展将调用[ *DereferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598141)清除目标物理网络适配器的索引的引用计数器。

### <a name="return-status-codes"></a>返回状态代码

可扩展交换机的基础的微型端口边缘完成 OID 查询请求的 OID\_切换\_NIC\_请求并返回一个的以下状态代码。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状态代码</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NDIS_STATUS_SUCCESS</p></td>
<td><p>OID 请求已成功完成。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_<em>Xxx</em></p></td>
<td><p>请求由于其他原因而失败。</p></td>
</tr>
</tbody>
</table>



<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>支持在 NDIS 6.30 和更高版本。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


****
[**NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

[**NDIS\_SWITCH\_NIC\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/hh598214)