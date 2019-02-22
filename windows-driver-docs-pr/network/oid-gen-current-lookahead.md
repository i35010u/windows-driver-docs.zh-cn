---
title: OID_GEN_CURRENT_LOOKAHEAD
description: 为查询，OID_GEN_CURRENT_LOOKAHEAD OID 到协议驱动程序返回接收到的数据包将指示的数据的字节数。
ms.assetid: ccfcb5ca-04bd-416b-91ec-690e78daeda0
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_CURRENT_LOOKAHEAD 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 245d4dbee3cf8173d1164ad1d8b9bda1223114ca
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520835"
---
# <a name="oidgencurrentlookahead"></a>OID\_GEN\_当前\_预测先行


为查询，OID\_GEN\_当前\_预测先行 OID 给协议驱动程序返回接收到的数据包将指示的数据的字节数。 此规范不包括标头。

作为一组 OID\_GEN\_当前\_预测先行 OID 指定的微型端口驱动程序应指示给协议驱动程序的接收的数据包数据的字节数。 此规范不包括标头。

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

NDIS NDIS 6.0 和更高版本的微型端口驱动程序处理查询和不成功的集请求。 NDIS 获取微型端口驱动程序在初始化和微型端口适配器重新启动信息。 但是，NDIS 将有效的集请求发送到微型端口驱动程序。

对于查询，NDIS 返回中的所有绑定进行的最大预期大小。 协议驱动程序可以设置要在其绑定; 中使用的字节数的建议的值但是，底层的微型端口驱动程序永远不会需要限制其指示为设置的值。

如果基础驱动程序支持 multipacket 接收迹象，绑定的协议驱动程序提供每个指示完整网络数据包。 因此，此值等同于返回[OID\_代\_接收\_阻止\_大小](oid-gen-receive-block-size.md)。

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


[OID\_GEN\_RECEIVE\_BLOCK\_SIZE](oid-gen-receive-block-size.md)

 

 




