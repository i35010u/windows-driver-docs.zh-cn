---
title: OID_GEN_MAC_OPTIONS
description: 为查询，OID_GEN_MAC_OPTIONS OID 指定的位掩码，用于定义基础驱动程序或 NIC 的可选属性
ms.assetid: 2a093bcb-ae6f-491c-a596-03e6f47b0b86
ms.date: 08/08/2017
keywords: -OID_GEN_MAC_OPTIONS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 23254474b06ed189ad93c274aad890b4f7893bdf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524265"
---
# <a name="oidgenmacoptions"></a>OID\_GEN\_MAC\_选项


为查询，OID\_GEN\_MAC\_选项 OID 指定的位掩码，用于定义基础驱动程序或 NIC 的可选属性

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

NDIS NDIS 6.0 和更高版本的微型端口驱动程序处理此 OID。

一个协议此查询可以确定该启动其中的标志的基础驱动程序设置，并 （可选） 可以充分利用它们。

当前定义的以下标志：

<a href="" id="ndis-mac-option-copy-lookahead-data"></a>NDIS\_MAC\_选项\_副本\_预测先行\_数据  
协议驱动程序就可以通过任何方式访问所指示的数据。 某些快速复制函数时遇到访问板载设备内存的问题。 指示数据映射的设备内存不足的微型端口驱动程序应永远不会设置此标志。 如果微型端口驱动程序未设置此标志，它会放松对快速复制函数的限制。

<a href="" id="ndis-mac-option-receive-serialized"></a>NDIS\_MAC\_选项\_接收\_已序列化  
微型端口驱动程序以串行方式指示数据包。 也就是说，这样的驱动程序不会进入一个新如果任何，完成后会收到指示上一接收，直到。

<a href="" id="ndis-mac-option-transfers-not-pend"></a>NDIS\_MAC\_选项\_传输\_不\_挂起  
微型端口驱动程序永远不会完成异步接收的指示。

指示的微型端口驱动程序收到具有操作[ **NdisMIndicateReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff563598)函数应设置此标志。

<a href="" id="ndis-mac-option-no-loopback"></a>NDIS\_MAC\_选项\_否\_环回  
因此 NDIS 将代表此驱动程序管理环回的 NIC 具有任何内部环回支持。 微型端口驱动程序不能提供其自己的软件环回高效的方式 NDIS，因此每个微型端口驱动程序应设置此标志，除非 NIC 有硬件环回支持。 WAN 微型端口驱动程序必须设置此标志。

<a href="" id="ndis-mac-option-full-duplex"></a>NDIS\_MAC\_选项\_完整\_双工  
微型端口驱动程序支持完全双工传输和 SMP 平台上的指示。

**请注意**  此标志不推荐使用 NDIS 5.0 和更高版本的微型端口驱动程序。 NDIS 5.0 及更高版本将忽略此标志。

 

<a href="" id="ndis-mac-option-eotx-indication"></a>NDIS\_MAC\_选项\_EOTX\_指示  
此标志已过时。

<a href="" id="ndis-mac-option-8021p-priority"></a>NDIS\_MAC\_选项\_8021 P\_优先级  
NIC 及其驱动程序支持的 802.1p 数据包优先级。 有关详细信息，请参阅[数据包优先级](https://msdn.microsoft.com/library/windows/hardware/ff562331)。 在接收数据包优先级值[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)更高层的驱动程序的结构。 数据包的 MAC 标头中生成相应的信息并将其通过网络传输。 此外，此 NIC 和其驱动程序支持来自从网络接收的数据包 MAC 标头中提取适当的信息。 此信息转发在 NET\_缓冲区到更高层的驱动程序的结构。

**请注意**  NDIS 6.0 和更高版本和更高版本及更高版本的微型端口驱动程序必须设置 NDIS\_MAC\_选项\_8021 P\_优先级标志。

 

<a href="" id="ndis-mac-option-supports-mac-address-overwrite"></a>NDIS\_MAC\_选项\_支持\_MAC\_地址\_覆盖  
NDIS 微型端口驱动程序调用时设置此标志[ **NdisReadNetworkAddress** ](https://msdn.microsoft.com/library/windows/hardware/ff564512)函数。

<a href="" id="ndis-mac-option-receive-at-dpc"></a>NDIS\_MAC\_OPTION\_RECEIVE\_AT\_DPC  
此标志已过时。

<a href="" id="ndis-mac-option-8021q-vlan"></a>NDIS\_MAC\_OPTION\_8021Q\_VLAN  
微型端口驱动程序可以分配和数据包的 MAC 标头中删除 VLAN 标识符 (ID) 标记。 该驱动程序维护驱动程序处理每个 NIC 配置的 VLAN ID。 该驱动程序筛选掉不属于的 VLAN 到的 NIC 相关联，并将标记与 VLAN ID 的传出数据包的传入数据包 在驱动程序的过程[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数特定的 NIC，驱动程序的最初设置为零的 NIC 的 VLAN ID。 在驱动程序*MiniportInitializeEx*函数然后读取以下配置参数从注册表中，并，如果存在，参数，则 NIC 的 VLAN ID 设置为参数的值。

```syntax
VlanId, REG_DWORD
```

<a href="" id="ndis-mac-option-reserved"></a>NDIS\_MAC\_选项\_保留  
保留供 NDIS 内部使用。

**请注意**  微型端口驱动程序，用于设置 NDIS\_MAC\_选项\_8021Q\_VLAN 标志还必须设置 NDIS\_MAC\_选项\_8021 P\_优先级标志。 换而言之，支持 802.1Q 的微型端口驱动程序还必须支持 802.1 p。

 

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
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[*MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)

[**NdisReadNetworkAddress**](https://msdn.microsoft.com/library/windows/hardware/ff564512)

[**NET\_BUFFER**](https://msdn.microsoft.com/library/windows/hardware/ff568376)

 

 




