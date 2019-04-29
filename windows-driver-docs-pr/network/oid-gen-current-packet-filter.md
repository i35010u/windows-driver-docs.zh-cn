---
title: OID_GEN_CURRENT_PACKET_FILTER
description: 为查询，OID_GEN_CURRENT_PACKET_FILTER OID 报告类型的网络数据包中的微型端口驱动程序从接收的指示。
ms.assetid: d5a32626-caff-4708-a134-d80a845dee91
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_CURRENT_PACKET_FILTER 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b7ac4d4f4033f6f4082f9aa5e44eb189bbf99b73
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368953"
---
# <a name="oidgencurrentpacketfilter"></a>OID\_GEN\_当前\_数据包\_筛选器


为查询，OID\_GEN\_当前\_数据包\_筛选器 OID 报告类型的网络数据包中的微型端口驱动程序从接收的指示。

作为一组 OID\_GEN\_当前\_数据包\_筛选器 OID 指定的净数据包协议从微型端口驱动程序收到指示的类型。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
必需。 (请参阅备注部分)

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需。

<a href="" id="windows-xp"></a>Windows XP  
支持。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需。

<a name="remarks"></a>备注
-------

NDIS 6.0 和更高版本的微型端口驱动程序，该查询未请求和集是必需的。 NDIS 处理查询的微型端口驱动程序。 微型端口驱动程序报告在初始化过程中的数据包筛选器信息。

微型端口驱动程序将报告为一个系统为其提供一个筛选器库，其介质类型。 数据包筛选器使用或运算 （含限值） 组合使用以下类型：

<a href="" id="ndis-packet-type-directed"></a>NDIS\_数据包\_类型\_定向  
定向的数据包。 定向的数据包包含目标地址都等于站地址的 nic。

<a href="" id="ndis-packet-type-multicast"></a>NDIS\_数据包\_类型\_多播  
多播的地址数据包发送到多播的地址列表中的地址。

协议驱动程序可以接收以太网 (802.3) 通过指定多路广播或无法正常工作的地址的数据包类型的多路广播的数据包。 设置多路广播的地址列表或功能的地址确定哪个多播的地址组 NIC 驱动程序启用。

<a href="" id="ndis-packet-type-all-multicast"></a>NDIS\_数据包\_类型\_所有\_多播  
所有多播的地址数据包，而不仅仅是多播的地址列表中枚举。

<a href="" id="ndis-packet-type-broadcast"></a>NDIS\_数据包\_类型\_广播  
广播的数据包。

<a href="" id="ndis-packet-type-promiscuous"></a>NDIS\_数据包\_类型\_PROMISCUOUS  
指定无论是否 VLAN 已启用筛选或未，VLAN 标识符匹配或未的所有数据包。

<a href="" id="ndis-packet-type-all-functional"></a>NDIS\_数据包\_类型\_所有\_功能  
所有功能地址数据包，而不仅仅是当前函数的地址。

<a href="" id="ndis-packet-type-all-local"></a>NDIS\_数据包\_类型\_所有\_本地  
通过安装协议发送的所有数据包和标识的 NIC 所指示的所有数据包给定*NdisBindingHandle* 。

<a href="" id="ndis-packet-type-functional"></a>NDIS\_数据包\_类型\_功能  
函数地址数据包发送到当前功能地址中包含的地址。

<a href="" id="ndis-packet-type-group"></a>NDIS\_数据包\_类型\_组  
与当前的组地址发送的数据包。

<a href="" id="ndis-packet-type-mac-frame"></a>NDIS\_PACKET\_TYPE\_MAC\_FRAME  
令牌环 NIC 会收到的 NIC 驱动程序框架。

<a href="" id="ndis-packet-type-smt"></a>NDIS\_数据包\_类型\_SMT  
SMT FDDI NIC 会收到的数据包。

<a href="" id="ndis-packet-type-source-routing"></a>NDIS\_数据包\_类型\_源\_路由  
所有源路由数据包。 如果协议驱动程序将设置此位，NDIS 库将尝试充当源路由桥。

适用于其媒体类型的微型端口适配器**NdisMedium802\_3**或**NdisMedium802\_5**，NDIS 禁用数据包接收，其他多播功能的地址在调用期间[ **NdisOpenAdapterEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563715)函数。

对于所有其他媒体类型的微型端口适配器，，协议驱动程序可以开始在任何时间期间接收数据包[ **NdisOpenAdapterEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563715)调用。 请注意，该协议甚至可以接收数据包之前**NdisOpenAdapterEx**返回。 一般情况下，数据包筛选是最大努力，和协议驱动程序必须准备好处理接收的指示，即使数据包筛选器为零。

对于查询，NDIS 返回使用 OR 运算符组合的绑定筛选器。

对于一组，指定的数据包筛选器将替换以前的数据包筛选器的绑定。 如果微型端口驱动程序之前启用数据包类型，但协议驱动程序未指定该类型的新筛选器中，协议驱动程序不会收到此类型的数据包。

适用于其媒体类型的微型端口适配器**NdisMedium802\_3**或**NdisMedium802\_5**，如果微型端口驱动程序不会在响应中为特定的数据包类型有点设置此查询中，协议驱动程序将不会收到该类型的数据包。 因此，协议驱动程序可以通过调用禁用数据包接收[ **NdisOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff563710)或[ **NdisCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561711)使用筛选器为零的函数。

对于所有其他媒体类型的微型端口适配器，NDIS 不会检查数据包类型。 对于这些媒体类型，协议驱动程序不能禁用数据包接收通过指定筛选器为零。

当微型端口驱动程序[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)调用函数，微型端口驱动程序的数据包筛选器应设置为零。 当数据包筛选器为零时，会收到指示已禁用。 微型端口驱动程序的后*MiniportInitializeEx*函数返回，协议驱动程序可以设置 OID\_常规\_当前\_数据包\_为非零值，从而筛选正在启用微型端口驱动程序，以指示该协议接收的数据包。

如果在混合模式下启用了 NDIS\_数据包\_类型\_混杂位协议驱动程序将继续接收数据包，即使发送的网络节点不会不将它们定向到它。 NDIS 然后发送协议驱动程序则 NIC 会收到所有数据包。

将特定的数据包筛选器设置不会更改为其他协议驱动程序绑定到 （或更高版本） 的数据包筛选器同一 nic。 例如，如果一种绑定的协议启用混合模式，其他绑定的协议驱动程序不会收到所不具有其自己的数据包筛选器专门请求的数据包。

**本机 802.11 数据包筛选器**

本机 802.11 微型端口驱动程序必须仅支持以下标准的数据包筛选器类型：

-   NDIS\_数据包\_类型\_定向

-   NDIS\_数据包\_类型\_多播

-   NDIS\_数据包\_类型\_广播

-   NDIS\_数据包\_类型\_PROMISCUOUS

启用时，这些标准的数据包筛选器都仅适用于 802.11 数据包。

此外，本机 802.11 微型端口驱动程序必须支持以下的数据包筛选器类型，它们是特定于本机 802.11 媒体：

<a href="" id="ndis-packet-type-802-11-raw-data"></a>NDIS\_PACKET\_TYPE\_802\_11\_RAW\_DATA  
802.11 媒体访问控制 (MAC) 协议数据单元 (MPDU) 框架，其中包含所有 802.11 站的接收到的格式中的数据。 当设置此筛选器时，该驱动程序必须指示每个未修改的 MPDU 片段之前它指示 MAC 服务数据单元 (MSDU) 数据包重新合并从 MPDU 片段。

如果 MPDU 片段进行加密，则它必须解密片段之前会出现。 但是，微型端口驱动程序必须对每个 MPDU 片段解密组装并指示 MSDU 数据包之前。

如果启用，此筛选器类型仅会影响其他标准的数据包筛选器，例如 NDIS\_数据包\_类型\_定向或 NDIS\_数据包\_类型\_广播。

有关用于指示原始 802.11 数据包的方法的详细信息，请参阅[，该值指示原始 802.11 数据包](https://msdn.microsoft.com/library/windows/hardware/ff554833)。

<a href="" id="ndis-packet-type-802-11-directed-mgmt"></a>NDIS\_数据包\_类型\_802\_11\_定向\_MGMT  
定向 802.11 管理数据包。 定向的数据包包含目标地址都等于站地址的 nic。

<a href="" id="ndis-packet-type-802-11-multicast-mgmt"></a>NDIS\_数据包\_类型\_802\_11\_多播\_MGMT  
发送到多播的地址列表中的地址的多路广播的 802.11 管理数据包。

<a href="" id="ndis-packet-type-802-11-all-multicast-mgmt"></a>NDIS\_数据包\_类型\_802\_11\_所有\_多播\_MGMT  
所有多播 802.11 管理接收的数据包的 802.11 工作站，而不管 802.11 MAC 报头中的目标地址是多播的地址列表中。

<a href="" id="ndis-packet-type-802-11-broadcast-mgmt"></a>NDIS\_PACKET\_TYPE\_802\_11\_BROADCAST\_MGMT  
广播接收的 802.11 工作站的 802.11 管理数据包。

<a href="" id="ndis-packet-type-802-11-promiscuous-mgmt"></a>NDIS\_数据包\_类型\_802\_11\_PROMISCUOUS\_MGMT  
接收的 802.11 工作站的所有的 802.11 管理数据包。

<a href="" id="ndis-packet-type-802-11-raw-mgmt"></a>NDIS\_数据包\_类型\_802\_11\_RAW\_MGMT  
802.11 MPDU 管理框架，其中包含所有 802.11 站的接收到的格式中的数据。 当设置此筛选器时，该驱动程序必须指示每个未修改的 MPDU 片段之前它指示 MAC 管理协议数据单元 (MMPDU) 数据包重新合并从 MPDU 片段。

如果启用，此筛选器类型仅会影响其他 802.11 的管理数据包筛选器，例如 NDIS\_数据包\_类型\_802\_11\_定向\_MGMT 或 NDIS\_数据包\_类型\_802\_11\_多播\_管理。

有关用于指示原始 802.11 管理数据包的方法的详细信息，请参阅[，该值指示原始 802.11 数据包](https://msdn.microsoft.com/library/windows/hardware/ff554833)。

<a href="" id="ndis-packet-type-802-11-directed-ctrl"></a>NDIS\_数据包\_类型\_802\_11\_定向\_CTRL  
定向 802.11 控制数据包。 定向的数据包包含目标地址都等于站地址的 nic。

<a href="" id="ndis-packet-type-802-11-broadcast-ctrl"></a>NDIS\_PACKET\_TYPE\_802\_11\_BROADCAST\_CTRL  
广播 802.11 接收的 802.11 工作站的控制数据包。

<a href="" id="ndis-packet-type-802-11-promiscuous-ctrl"></a>NDIS\_PACKET\_TYPE\_802\_11\_PROMISCUOUS\_CTRL  
所有接收的 802.11 工作站的 802.11 控制数据包。

如果微型端口驱动程序在本机 802.11 网络监视器 (NetMon) 或可扩展接入点 (AP) 模式下运行，则驱动程序必须启用 OID 的集请求通过以下的数据包筛选器\_GEN\_当前\_数据包\_筛选器。

-   NDIS\_数据包\_类型\_PROMISCUOUS

-   NDIS\_PACKET\_TYPE\_802\_11\_RAW\_DATA

-   NDIS\_数据包\_类型\_802\_11\_PROMISCUOUS\_MGMT

-   NDIS\_数据包\_类型\_802\_11\_RAW\_MGMT

-   NDIS\_数据包\_类型\_802\_11\_PROMISCUOUS\_CTRL

除了 NetMon 必须启用这些数据包筛选器设置，但 NDIS 除外，在其他本机 802.11 模式下运行的微型端口驱动程序\_数据包\_类型\_802\_11\_PROMISCUOUS\_CTRL。 不在 NetMon 模式下运行的微型端口驱动程序可以选择性地启用 NDIS\_数据包\_类型\_802\_11\_PROMISCUOUS\_OID 的集请求通过 CTRL\_GEN\_当前\_数据包\_筛选器。

**请注意**  微型端口驱动程序时在本机 802.11 NetMon 和 OID 以外的模式下\_常规\_当前\_数据包\_设置筛选器，如果有，驱动程序不得失败集请求OID 数据中启用混杂或原始筛选器设置。

 

有关 NetMon 和 ExtAP 操作模式的详细信息，请参阅以下主题：

[网络监视器操作模式](https://msdn.microsoft.com/library/windows/hardware/ff568369)

[可扩展的访问点操作模式](https://msdn.microsoft.com/library/windows/hardware/ff549858)

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[*MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)

[**NdisCoOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff561711)

[**NdisOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff563710)

[**NdisOpenAdapterEx**](https://msdn.microsoft.com/library/windows/hardware/ff563715)

 

 




