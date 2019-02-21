---
title: OID_GEN_MAXIMUM_LOOKAHEAD
description: 为查询，OID_GEN_MAXIMUM_LOOKAHEAD OID 指定最大 NIC 可以提供作为预测先行数据的字节数。
ms.assetid: 086581f7-c0a5-4355-82fe-22f53201b540
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_MAXIMUM_LOOKAHEAD 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f73390c6a8ec9289b122865a914ea898c20e1e22
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527075"
---
# <a name="oidgenmaximumlookahead"></a>OID\_GEN\_最大\_预测先行


为查询，OID\_GEN\_最大\_预测先行 OID 作为预测先行数据指定最大 NIC 可以提供的字节数。 此规范不包括标头。

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

NDIS 6.0 和更高版本的微型端口驱动程序不会收到此 OID 请求。 NDIS 处理此 OID 微型端口驱动程序在初始化过程中提供的缓存值。

上层驱动程序检查预测先行数据以确定是否与预期数据关联的数据包适用于一个或多个其客户端。

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

 

 




