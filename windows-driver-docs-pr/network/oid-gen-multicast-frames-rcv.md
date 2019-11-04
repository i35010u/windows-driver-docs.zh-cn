---
title: OID_GEN_MULTICAST_FRAMES_RCV
description: 作为查询，OID_GEN_MULTICAST_FRAMES_RCV OID 指定接收的没有错误的多播/功能数据包的数量。
ms.assetid: 6001dc07-43ab-420d-b29b-1138485ce218
ms.date: 11/01/2019
keywords: -从 Windows Vista 开始 OID_GEN_MULTICAST_FRAMES_RCV 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5718f41362a33176887c93432183b4d237372c23
ms.sourcegitcommit: b8876f616ac625bb3f38218a32b2dc35ac7b3399
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2019
ms.locfileid: "73443021"
---
# <a name="oid_gen_multicast_frames_rcv"></a>OID\_代\_多播\_帧\_RCV


作为查询，OID\_代\_多播\_帧\_RCV OID 指定接收的无错误多播/功能数据包的数目。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
已过时。

<a href="" id="ndis-6-0-and-later-drivers"></a>NDIS 6.0 和更高版本驱动程序  
未请求。 改用[OID\_代\_统计信息](oid-gen-statistics.md)。

<a href="" id="ndis-5-1-drivers"></a>NDIS 5.1 驱动程序  
可选。

<a href="" id="windows-xp"></a>Windows XP  
支持。

<a href="" id="ndis-5-1-drivers"></a>NDIS 5.1 驱动程序  
可选。

<a name="remarks"></a>备注
-------

此 OID 中与[OID_GEN_BROADCAST_FRAMES_RCV](oid-gen-broadcast-frames-rcv.md)的计数结合的计数与 RFC 2863 中所述的*ifInNUcastPkts*计数器相同。

有关统计信息 Oid 的一般信息，请参阅[常规统计](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-general-statistics-oids)信息。

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


[OID\_代\_统计信息](oid-gen-statistics.md)

 

 




