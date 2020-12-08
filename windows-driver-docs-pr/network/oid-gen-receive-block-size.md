---
title: OID_GEN_RECEIVE_BLOCK_SIZE
description: 作为查询。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_RECEIVE_BLOCK_SIZE 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 9f6b36cb96134a882dee723c28619b9b70b4e4a8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836747"
---
# <a name="oid_gen_receive_block_size"></a>OID \_ 生成 \_ 接收 \_ 块 \_ 大小


作为查询。 OID 生成 \_ \_ 接收 \_ 块 \_ 大小 oid 指定单个数据包在 NIC 的接收缓冲区空间中所占的存储量（以字节为单位）。

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

OID 生成 \_ \_ 接收 \_ 块 \_ 大小 oid 指定单个数据包在 NIC 的接收缓冲区空间中所占的存储量（以字节为单位）。

可以从当前和最大 *预测先行* 大小获取相同的信息。 但是，其中一个 Oid 可能是必需的，以便彼此验证。 此外，协议驱动程序可以通过比较驱动程序为 [OID 生成 \_ 当前的 \_ \_ 预测先行](oid-gen-current-lookahead.md) 和 Oid 生成 \_ \_ 接收 \_ 块 \_ 大小 oid 返回的值，来确定基础驱动程序是否指示完整数据包接收。

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

## <a name="see-also"></a>请参阅


[OID \_ 生成 \_ 当前 \_ 预测先行](oid-gen-current-lookahead.md)

 

 




