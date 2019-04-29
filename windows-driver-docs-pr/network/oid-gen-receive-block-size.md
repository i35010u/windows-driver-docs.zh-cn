---
title: OID_GEN_RECEIVE_BLOCK_SIZE
description: 作为查询。
ms.assetid: 92a7a388-4a41-41cf-96e5-a65b5559553d
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_RECEIVE_BLOCK_SIZE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f320cf7bebb06e6a861c9835cee573b1024f0edf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367533"
---
# <a name="oidgenreceiveblocksize"></a>OID\_GEN\_RECEIVE\_BLOCK\_SIZE


作为查询。 OID\_GEN\_接收\_阻止\_大小 OID 指定的存储，以字节为单位，NIC 的接收缓冲区空间中占用单个数据包

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

OID\_GEN\_接收\_阻止\_大小 OID 指定的存储，以字节为单位，NIC 的接收缓冲区空间中占用单个数据包

可以从当前和最大值获取相同的信息*预测先行*大小。 但是，这些 Oid 之一可以强制验证彼此。 协议驱动程序还可以确定是否基础驱动程序，则表示完整数据包接收通过比较的值对于该驱动程序将返回[OID\_代\_当前\_预测先行](oid-gen-current-lookahead.md)和 OID\_GEN\_接收\_阻止\_大小 Oid。

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


[OID\_GEN\_当前\_预测先行](oid-gen-current-lookahead.md)

 

 




