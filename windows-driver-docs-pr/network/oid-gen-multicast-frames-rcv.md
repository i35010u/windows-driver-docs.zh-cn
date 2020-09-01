---
title: OID_GEN_MULTICAST_FRAMES_RCV
description: 作为查询，OID_GEN_MULTICAST_FRAMES_RCV OID 指定接收的没有错误的多播/函数数据包的数目。
ms.assetid: 6001dc07-43ab-420d-b29b-1138485ce218
ms.date: 11/01/2019
keywords: -从 Windows Vista 开始 OID_GEN_MULTICAST_FRAMES_RCV 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5341cc1dd703e82dc7dc3eacb6a295a6bda3aa9f
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207199"
---
# <a name="oid_gen_multicast_frames_rcv"></a>OID \_ 生成 \_ 多播 \_ 帧 \_ RCV


作为查询，OID \_ 代 \_ 多播 \_ 帧 \_ RCV oid 指定接收的没有错误的多播/功能数据包的数量。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
已过时。

<a href="" id="ndis-6-0-and-later-drivers"></a>NDIS 6.0 和更高版本驱动程序  
未请求。 请改用 [OID 生成 \_ \_ 统计信息](oid-gen-statistics.md) 。

<a href="" id="ndis-5-1-drivers"></a>NDIS 5.1 驱动程序  
可选。

<a href="" id="windows-xp"></a>Windows XP  
支持。

<a href="" id="ndis-5-1-drivers"></a>NDIS 5.1 驱动程序  
可选。

<a name="remarks"></a>备注
-------

此 OID 的计数与 [OID_GEN_BROADCAST_FRAMES_RCV](oid-gen-broadcast-frames-rcv.md)中的计数结合，与 RFC 2863 中所述的 *ifInNUcastPkts* 计数器相同。

有关统计信息 Oid 的一般信息，请参阅 [常规统计](./ndis-general-statistics-oids.md)信息。

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


[OID \_ 生成 \_ 统计信息](oid-gen-statistics.md)

 

