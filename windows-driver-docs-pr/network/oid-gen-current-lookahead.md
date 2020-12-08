---
title: OID_GEN_CURRENT_LOOKAHEAD
description: 作为查询，OID_GEN_CURRENT_LOOKAHEAD OID 返回接收到的数据包数据的字节数，这些字节将向协议驱动程序指示。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_CURRENT_LOOKAHEAD 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 519325a18f4096aeaa2fb20a0ff80b7d8948941c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837669"
---
# <a name="oid_gen_current_lookahead"></a>OID \_ 生成 \_ 当前 \_ 预测先行


作为查询，OID 生成 \_ \_ 当前 \_ 预测先行 oid 返回将向协议驱动程序指示的已接收数据包数据的字节数。 此规范不包含标头。

作为集，OID \_ GEN \_ 当前 \_ 预测先行 oid 指定微型端口驱动程序应向协议驱动程序指示的已接收数据包数据的字节数。 此规范不包含标头。

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

NDIS 处理 NDIS 6.0 和更高的小型小型小型驱动程序的查询和未成功的设置请求。 在初始化期间，NDIS 将从微型端口驱动程序中获取信息，而微型端口适配器将重新启动。 但是，NDIS 会将有效的 set 请求发送到微型端口驱动程序。

对于查询，NDIS 返回所有绑定中的最大预测先行大小。 协议驱动程序可以为要在其绑定中使用的字节数设置建议值;但是，根本无需将基础微型端口驱动程序限制为值集的指示。

如果基础驱动程序支持 multipacket 接收指示，则会在每次指示时为绑定协议驱动程序提供完整的网络数据包。 因此，此值与为 [OID 生成 \_ \_ 接收 \_ 块 \_ 大小](oid-gen-receive-block-size.md)返回的值相同。

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


[OID \_ 生成 \_ 接收 \_ 块 \_ 大小](oid-gen-receive-block-size.md)

 

 




