---
title: OID_GEN_MAXIMUM_TOTAL_SIZE
description: 作为查询，OID_GEN_MAXIMUM_TOTAL_SIZE OID 指定 NIC 支持的最大数据包总长度（以字节为单位）。
ms.assetid: 4973b4bd-58a5-4242-b33f-1ff8c3a7ec4b
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_MAXIMUM_TOTAL_SIZE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 89089a839e2acd692410f6de483b395edc0e202b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843065"
---
# <a name="oid_gen_maximum_total_size"></a>OID\_GEN\_最大\_总\_大小


作为查询，OID\_GEN\_最大\_总数\_大小 OID 指定 NIC 支持的最大数据包总长度（以字节为单位）。 此规范包括标头。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
必需.

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需.

<a href="" id="windows-xp"></a>Windows XP  
支持。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需.

<a name="remarks"></a>备注
-------

返回的长度为基础介质指定了最大的数据包大小。 因此，返回的长度取决于特定介质。 协议驱动程序可以使用此返回长度作为仪表来确定微型端口驱动程序可以转发给协议驱动程序的最大大小的数据包。 如果协议驱动程序预分配缓冲区，则会相应地分配缓冲区。 返回的长度还指定了协议驱动程序可传递给[**NdisSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissendnetbufferlists)函数的最大数据包。

如果 NIC 的微型端口驱动程序启用了[802.1 p 数据包优先级](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff562331(v=vs.85))（即微型端口驱动程序指定了 NDIS\_MAC\_选项\_8021P\_优先级位在[OID\_代\_mac\_MAC OPTIONS](oid-gen-mac-options.md) oid位掩码），则微型端口驱动程序必须将其最大数据包长度指定为比通过网络接收或发送的最大数据包大小的4个字节。 例如，如果启用了 802.1 p 数据包优先级的 NIC 接收并发送长度为1514字节的线路上的数据包，则 NIC 的微型端口驱动程序必须将其最大数据包长度报告为1510字节。 微型端口驱动程序永远不能指示通过网络接收的绑定协议驱动程序包，其长度超过 OID 指定的数据包大小\_代\_最大\_总数\_大小。 也就是说，即使微型端口驱动程序通过网络接收的数据包未标记为优先级值，但仍是基础介质所支持的最大大小，小型小型驱动程序驱动程序才能指示超出大小的数据包由 OID 指定\_GEN\_最大\_总\_大小。

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
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NdisSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissendnetbufferlists)

[OID\_代\_MAC\_选项](oid-gen-mac-options.md)

 

 




