---
title: OID_GEN_TRANSMIT_BLOCK_SIZE
description: 作为查询，OID_GEN_TRANSMIT_BLOCK_SIZE OID 指定单个网络数据包在 NIC 的传输缓冲区空间中所占的最小字节数。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_TRANSMIT_BLOCK_SIZE 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 8b645245cd7ce0560c02ef3b31588e674b2b598a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825427"
---
# <a name="oid_gen_transmit_block_size"></a>OID \_ 代 \_ 传输 \_ 块 \_ 大小


作为查询，OID \_ 代 \_ 传输 \_ 块 \_ 大小 OID 指定单个网络数据包在 NIC 的传输缓冲区空间中所占用的最小字节数。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
必需。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需。

<a href="" id="windows-xp"></a>Windows XP  
支持。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需。

<a name="remarks"></a>备注
-------

OID \_ GEN \_ 传输 \_ 块 \_ 大小 OID 指定单个网络数据包在 NIC 的传输缓冲区空间中所占用的最小字节数。 例如，将传输空间划分为256字节块的 NIC 的传输块大小为256字节。 若要计算这种 NIC 上的总传输缓冲区空间，其驱动程序会按照传输块大小将 NIC 上的传输缓冲区数量相乘。

对于其他 Nic，传输块大小与它的最大数据包大小完全相同。

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

 

 




