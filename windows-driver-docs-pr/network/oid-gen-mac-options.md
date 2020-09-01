---
title: OID_GEN_MAC_OPTIONS
description: 作为查询，OID_GEN_MAC_OPTIONS OID 指定了一个位掩码，用于定义基础驱动程序或 NIC 的可选属性。
ms.assetid: 2a093bcb-ae6f-491c-a596-03e6f47b0b86
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_MAC_OPTIONS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 3d96e7bd1e0de98eaa4d231c8dce6131173e4003
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214605"
---
# <a name="oid_gen_mac_options"></a>OID \_ 生成 \_ MAC \_ 选项


作为查询，OID \_ GEN \_ MAC \_ 选项 oid 指定了一个位掩码，用于定义基础驱动程序或 NIC 的可选属性。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需。

<a href="" id="windows-xp"></a>Windows XP  
支持。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需。

<a name="remarks"></a>备注
-------

NDIS 处理 NDIS 6.0 和更高版本的小型小型驱动程序的此 OID。

启动此查询的协议可以确定基础驱动程序集的哪些标志，还可以选择利用它们。

当前定义了下列标志：

<a href="" id="ndis-mac-option-copy-lookahead-data"></a>NDIS \_ MAC \_ 选项 \_ 复制 \_ 预测先行 \_ 数据  
协议驱动程序可以通过任何方式免费访问指定的数据。 某些快速复制功能在访问板设备内存时遇到问题。 小型端口驱动程序指示映射的设备内存之外的数据绝不应设置此标志。 如果微型端口驱动程序设置了此标志，则会放宽对快速复制函数的限制。

<a href="" id="ndis-mac-option-receive-serialized"></a>NDIS \_ MAC \_ 选项 \_ 接收 \_ 序列化  
微型端口驱动程序以串行方式指示数据包。 也就是说，此类驱动程序在以前的接收（如果有）已完成之前，不会输入新的接收指示。

<a href="" id="ndis-mac-option-transfers-not-pend"></a>\_ \_ \_ \_ 未挂起 NDIS MAC 选项 \_ 传输  
微型端口驱动程序绝不会以异步方式完成接收指示。

使用 [**NdisMIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists) 函数指示接收操作的微型端口驱动程序应设置此标志。

<a href="" id="ndis-mac-option-no-loopback"></a>NDIS \_ MAC \_ 选项 \_ 无 \_ 环回  
NIC 没有内部环回支持，因此 NDIS 将代表此驱动程序管理环回。 微型端口驱动程序无法提供自己的软件环回作为 NDIS 的有效环回，因此每个微型端口驱动程序应设置此标志，除非 NIC 有硬件环回支持。 WAN 微型端口驱动程序必须设置此标志。

<a href="" id="ndis-mac-option-full-duplex"></a>NDIS \_ MAC \_ 选项 \_ 全双工 \_  
微型端口驱动程序支持 SMP 平台上的全双工传输和指示。

**注意**   此标志已弃用，无法供 NDIS 5.0 和更高版本小型端口驱动程序使用。 NDIS 5.0 和更高版本忽略此标志。

 

<a href="" id="ndis-mac-option-eotx-indication"></a>NDIS \_ MAC \_ 选项 \_ EOTX \_ 指示  
此标志已过时。

<a href="" id="ndis-mac-option-8021p-priority"></a>NDIS \_ MAC \_ 选项 \_ 8021P \_ 优先级  
NIC 及其驱动程序支持 802.1 p 包优先级。 有关详细信息，请参阅 [数据包优先级](/previous-versions/windows/hardware/network/ff562331(v=vs.85))。 数据包优先级值是从较高层驱动程序的 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) 结构接收的。 适当的信息在数据包的 MAC 标头中生成并通过网络传输。 此外，此 NIC 及其驱动程序支持从网络接收的数据包的 MAC 标头提取相应的信息。 此信息将在网络 \_ 缓冲区结构中转发到更高层的驱动程序。

**注意**   NDIS 6.0 和更高版本及更高版本的微型端口驱动程序必须设置 NDIS \_ MAC \_ 选项 \_ 8021P \_ PRIORITY 标志。

 

<a href="" id="ndis-mac-option-supports-mac-address-overwrite"></a>NDIS \_ MAC \_ 选项 \_ 支持 \_ MAC \_ 地址 \_ 覆盖  
当微型端口驱动程序调用 [**NdisReadNetworkAddress**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreadnetworkaddress) 函数时，NDIS 将设置此标志。

<a href="" id="ndis-mac-option-receive-at-dpc"></a>\_ \_ \_ \_ 在 DPC 处接收 NDIS MAC 选项 \_  
此标志已过时。

<a href="" id="ndis-mac-option-8021q-vlan"></a>NDIS \_ MAC \_ 选项 \_ 8021Q \_ VLAN  
微型端口驱动程序可以分配和删除 VLAN 标识符 (ID) 在数据包的 MAC 标头中标记。 驱动程序将为驱动程序处理的每个 NIC 维护一个已配置的 VLAN ID。 驱动程序筛选出不属于 NIC 关联的 VLAN 的传入数据包，并使用 VLAN ID 标记传出数据包。 在驱动程序的 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数中，对于特定 NIC，驱动程序最初将 NIC 的 VLAN ID 设置为零。 然后，驱动程序的 *MiniportInitializeEx* 函数从注册表读取以下配置参数，如果该参数存在，则将 NIC 的 VLAN ID 设置为参数的值。

```syntax
VlanId, REG_DWORD
```

<a href="" id="ndis-mac-option-reserved"></a>已 \_ 保留 NDIS MAC \_ 选项 \_  
保留以供 NDIS 内部使用。

**注意**   设置 NDIS \_ mac 选项 8021Q VLAN 标志的微型端口驱动程序 \_ \_ \_ 还必须设置 ndis \_ mac \_ 选项 \_ 8021P \_ 优先级标志。 换句话说，支持 802.1 Q 的微型端口驱动程序还必须支持 802.1 p。

 

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

[**NdisReadNetworkAddress**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreadnetworkaddress)

[**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)

 

