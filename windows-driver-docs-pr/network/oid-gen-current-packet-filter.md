---
title: OID_GEN_CURRENT_PACKET_FILTER
description: 作为查询，OID_GEN_CURRENT_PACKET_FILTER OID 报告来自微型端口驱动程序的接收指示的网络数据包类型。
ms.assetid: d5a32626-caff-4708-a134-d80a845dee91
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_CURRENT_PACKET_FILTER 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: adee25ece0078bf1e891653df64fe606356edf60
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217014"
---
# <a name="oid_gen_current_packet_filter"></a>OID \_ GEN \_ 当前 \_ 数据包 \_ 筛选器


作为查询，OID \_ GEN \_ 当前 \_ 数据包 \_ 筛选器 oid 报告来自微型端口驱动程序的接收指示的网络数据包类型。

作为集，OID 生成 \_ \_ 当前 \_ 数据包 \_ 筛选器 oid 指定协议从微型端口驱动程序接收指示的网络数据包类型。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
必需。  (参见 "备注" 部分) 

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需。

<a href="" id="windows-xp"></a>Windows XP  
支持。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需。

<a name="remarks"></a>备注
-------

对于 NDIS 6.0 和更高的微型端口驱动程序，不会请求该查询，并且该集是必需的。 NDIS 处理微型端口驱动程序的查询。 小型端口驱动程序在初始化期间报告数据包筛选器信息。

微型端口驱动程序将其中型类型报告为系统为其提供筛选器库的类型。 数据包筛选器使用或操作来合并以下类型：

<a href="" id="ndis-packet-type-directed"></a>NDIS \_ 数据包 \_ 类型 \_ 定向  
定向数据包。 定向数据包包含等于 NIC 工作站地址的目标地址。

<a href="" id="ndis-packet-type-multicast"></a>NDIS \_ 数据包 \_ 类型 \_ 多播  
多播地址数据包发送到多播地址列表中的地址。

协议驱动程序可以通过指定多播或功能地址数据包类型来接收以太网 (802.3) 多播数据包。 设置多播地址列表或功能地址会确定 NIC 驱动程序启用的多播地址组。

<a href="" id="ndis-packet-type-all-multicast"></a>NDIS \_ 数据包 \_ 类型 \_ 所有 \_ 多播  
所有多播地址数据包，不仅仅是在多播地址列表中枚举的数据包。

<a href="" id="ndis-packet-type-broadcast"></a>NDIS \_ 数据包 \_ 类型 \_ 广播  
广播数据包。

<a href="" id="ndis-packet-type-promiscuous"></a>NDIS \_ 数据包 \_ 类型 \_ 混杂  
指定所有数据包，无论 vlan 筛选是否已启用，以及 VLAN 标识符是否匹配。

<a href="" id="ndis-packet-type-all-functional"></a>NDIS \_ 数据包 \_ 类型 \_ 全部 \_ 正常运行  
所有功能地址包，而不仅仅是当前功能地址中的数据包。

<a href="" id="ndis-packet-type-all-local"></a>NDIS \_ 数据包 \_ 类型 \_ 全部 \_ 本地  
所有由已安装协议发送的数据包，以及由给定 *NdisBindingHandle* 标识的 NIC 所指示的所有数据包。

<a href="" id="ndis-packet-type-functional"></a>NDIS \_ 数据包 \_ 类型 \_ 功能  
发送到当前功能地址中包含的地址的功能地址包。

<a href="" id="ndis-packet-type-group"></a>NDIS \_ 数据包 \_ 类型 \_ 组  
发送到当前组地址的数据包。

<a href="" id="ndis-packet-type-mac-frame"></a>NDIS \_ 数据包 \_ 类型 \_ MAC \_ 帧  
令牌环 NIC 接收的 NIC 驱动程序帧。

<a href="" id="ndis-packet-type-smt"></a>NDIS \_ 数据包 \_ 类型 \_ SMT  
SMT FDDI NIC 接收的数据包。

<a href="" id="ndis-packet-type-source-routing"></a>NDIS \_ 数据包 \_ 类型 \_ 源 \_ 路由  
所有源路由数据包。 如果协议驱动程序设置此位，NDIS 库将尝试充当源路由桥。

对于其媒体类型为 **NdisMedium802 \_ 3** 或 **NdisMedium802 \_ 5**的微型端口适配器，NDIS 在调用 [**NdisOpenAdapterEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenadapterex) 函数期间禁用数据包接收，以及多播和功能地址。

对于具有所有其他媒体类型的微型端口适配器，协议驱动程序可在 [**NdisOpenAdapterEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenadapterex) 调用期间随时开始接收数据包。 请注意，该协议甚至可以在 **NdisOpenAdapterEx** 返回之前接收数据包。 通常，数据包筛选是最重要的，即使数据包筛选器为零，协议驱动程序也必须准备好处理接收指示。

对于查询，NDIS 返回使用 OR 运算符组合的绑定筛选器。

对于集，指定的数据包筛选器将替换绑定的以前的数据包筛选器。 如果微型端口驱动程序以前启用了数据包类型，但协议驱动程序未在新筛选器中指定该类型，则协议驱动程序将不会接收此类型的数据包。

对于媒体类型为 **NdisMedium802 \_ 3** 或 **NdisMedium802 \_ 5**的微型端口适配器，如果小型端口驱动程序没有为特定数据包类型设置位来响应此查询，则协议驱动程序将不会接收该类型的数据包。 因此，协议驱动程序可以通过使用零筛选器调用 [**NdisOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest) 或 [**NdisCoOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest) 函数来禁用数据包接收。

对于包含所有其他媒体类型的微型端口适配器，NDIS 不检查数据包类型。 对于这些媒体类型，协议驱动程序无法通过指定筛选器来禁用数据包接收。

调用微型端口驱动程序的 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数时，微型端口驱动程序的数据包筛选器应设置为零。 当数据包筛选器为零时，将禁用接收指示。 在微型端口驱动程序的 *MiniportInitializeEx* 函数返回后，协议驱动程序可以将 OID 生成 \_ \_ 当前 \_ 数据包 \_ 筛选器设置为一个非零值，从而使微型端口驱动程序指示接收到该协议的数据包。

如果在 NDIS 数据包类型为 "非混杂" 的情况下启用了混杂模式 \_ \_ \_ ，则即使发送网络节点未将数据包定向到该协议驱动程序，协议驱动程序仍将继续接收这些数据包。 然后，NDIS 将发送 NIC 接收的所有数据包的协议驱动程序。

设置特定数据包筛选器不会更改绑定到相同 NIC (或更高) 的其他协议驱动程序的数据包筛选器。 例如，如果一个绑定协议启用了混杂模式，则其他绑定协议驱动程序将不会接收这些数据包，这些数据包未使用其自己的数据包筛选器专门请求。

**本机802.11 数据包筛选器**

本机802.11 微型端口驱动程序必须仅支持以下标准数据包筛选器类型：

-   NDIS \_ 数据包 \_ 类型 \_ 定向

-   NDIS \_ 数据包 \_ 类型 \_ 多播

-   NDIS \_ 数据包 \_ 类型 \_ 广播

-   NDIS \_ 数据包 \_ 类型 \_ 混杂

启用后，这些标准数据包筛选器仅适用于802.11 数据包。

此外，本机802.11 微型端口驱动程序必须支持以下数据包筛选器类型，这些类型特定于本机802.11 媒体：

<a href="" id="ndis-packet-type-802-11-raw-data"></a>NDIS \_ 数据包 \_ 类型 \_ 802 \_ 11 \_ 原始 \_ 数据  
802.11 media access control (MAC) 协议数据单位 (MPDU) 帧，其中包含802.11 工作站收到的格式的所有数据。 设置此筛选器时，驱动程序必须指出每个未修改的 MPDU 片段，然后指示 MAC 服务数据单元 (MSDU 从 MPDU 片段重新组合) 包。

如果对 MPDU 片段进行了加密，则在指定片段之前，不能对其进行解密。 但是，微型端口驱动程序必须在 reassembling 之前解密每个 MPDU 片段，并指示 MSDU 数据包。

如果启用，此筛选器类型将只影响其他标准数据包筛选器，如 NDIS \_ 数据包 \_ 类型 \_ 定向或 ndis \_ 数据包 \_ 类型 \_ 广播。

有关指示原始802.11 数据包的方法的详细信息，请参阅 [指示原始802.11 数据包](/previous-versions/windows/hardware/wireless/indicating-raw-802-11-packets)。

<a href="" id="ndis-packet-type-802-11-directed-mgmt"></a>NDIS \_ 数据包 \_ 类型 \_ 802 \_ 11 \_ 定向 \_ 管理  
定向802.11 管理包。 定向数据包包含等于 NIC 工作站地址的目标地址。

<a href="" id="ndis-packet-type-802-11-multicast-mgmt"></a>NDIS \_ 数据包 \_ 类型 \_ 802 \_ 11 \_ 多播 \_ 管理  
多播802.11 管理包发送到多播地址列表中的地址。

<a href="" id="ndis-packet-type-802-11-all-multicast-mgmt"></a>NDIS \_ 数据包 \_ 类型 \_ 802 \_ 11 \_ 所有 \_ 多播 \_ 管理  
802.11 工作站收到的所有多播802.11 管理数据包，不管 802.11 MAC 标头中的目标地址是否在多播地址列表中。

<a href="" id="ndis-packet-type-802-11-broadcast-mgmt"></a>NDIS \_ 数据包 \_ 类型 \_ 802 \_ 11 \_ 广播 \_ 管理  
802.11 工作站接收的广播802.11 管理包。

<a href="" id="ndis-packet-type-802-11-promiscuous-mgmt"></a>NDIS \_ 数据包 \_ 类型 \_ 802 \_ 11 \_ 混杂 \_ 管理  
802.11 工作站接收的所有802.11 管理包。

<a href="" id="ndis-packet-type-802-11-raw-mgmt"></a>NDIS \_ 数据包 \_ 类型 \_ 802 \_ 11 \_ 原始 \_ 管理  
802.11 MPDU 管理框架，其中包含802.11 工作站收到的格式的所有数据。 设置此筛选器时，驱动程序必须指出每个未修改的 MPDU 片段，然后再指示 MAC 管理协议数据单元 (MMPDU 从 MPDU 片段重新组合) 包。

如果启用，此筛选器类型将只影响其他802.11 管理数据包筛选器，如 NDIS \_ 数据包 \_ 类型 \_ 802 \_ 11 \_ 定向 \_ 管理或 ndis \_ 数据包 \_ 类型 \_ 802 \_ 11 \_ 多播 \_ 管理。

有关指示原始802.11 管理包的方法的详细信息，请参阅 [指示原始802.11 数据包](/previous-versions/windows/hardware/wireless/indicating-raw-802-11-packets)。

<a href="" id="ndis-packet-type-802-11-directed-ctrl"></a>NDIS \_ 数据包 \_ 类型 \_ 802 \_ 11 \_ 定向 \_ CTRL  
定向802.11 控制数据包。 定向数据包包含等于 NIC 工作站地址的目标地址。

<a href="" id="ndis-packet-type-802-11-broadcast-ctrl"></a>NDIS \_ 数据包 \_ 类型 \_ 802 \_ 11 \_ 广播 \_ CTRL  
广播802.11 控制802.11 工作站接收的数据包。

<a href="" id="ndis-packet-type-802-11-promiscuous-ctrl"></a>NDIS \_ 数据包 \_ 类型 \_ 802 \_ 11 \_ 混杂 \_ CTRL  
802.11 工作站收到的所有802.11 控制数据包。

如果微型端口驱动程序在本机802.11 网络监视器中运行 (NetMon) 或 (AP) 模式的可扩展访问点，则驱动程序必须通过 OID 第一 \_ 代 \_ 当前 \_ 数据包 \_ 筛选器的集请求启用以下数据包筛选器。

-   NDIS \_ 数据包 \_ 类型 \_ 混杂

-   NDIS \_ 数据包 \_ 类型 \_ 802 \_ 11 \_ 原始 \_ 数据

-   NDIS \_ 数据包 \_ 类型 \_ 802 \_ 11 \_ 混杂 \_ 管理

-   NDIS \_ 数据包 \_ 类型 \_ 802 \_ 11 \_ 原始 \_ 管理

-   NDIS \_ 数据包 \_ 类型 \_ 802 \_ 11 \_ 混杂 \_ CTRL

除 NetMon 以外的其他本机802.11 模式下操作的微型端口驱动程序必须启用这些数据包筛选器设置，但 NDIS \_ 数据包 \_ 类型 \_ 802 \_ 11 \_ 混杂 CTRL 除外 \_ 。 未在 NetMon 模式下操作的微型端口驱动程序可以选择启用 NDIS \_ 包 \_ 类型 \_ 802 \_ 11 混杂 CTRL，然后 \_ \_ 执行 OID 生成 \_ \_ 当前 \_ 数据包 \_ 筛选器的设置请求。

**注意**   如果微型端口驱动程序处于 NetMon 以外的本机802.11 模式下，并且设置了 OID 生成 \_ \_ 当前 \_ 数据包 \_ 筛选器，则当 oid 数据中启用了任何混杂或原始筛选器设置时，驱动程序不得使集请求失败。

 

有关 NetMon 和 ExtAP 运行模式的详细信息，请参阅以下主题：

[网络监视器操作模式](/previous-versions/windows/hardware/wireless/network-monitor-operation-mode)

[可扩展访问点操作模式](/previous-versions/windows/hardware/wireless/extensible-access-point-operation-mode)

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)

[**NdisCoOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)

[**NdisOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)

[**NdisOpenAdapterEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenadapterex)

 

