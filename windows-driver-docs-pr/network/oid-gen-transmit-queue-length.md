---
title: OID_GEN_TRANSMIT_QUEUE_LENGTH
description: 作为查询，OID_GEN_TRANSMIT_QUEUE_LENGTH OID 指定当前排队等待传输的数据包数，无论是在 NIC 上还是在驱动程序内部队列中。
ms.assetid: 042a7df3-a204-45f8-b147-96def7438b4a
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_TRANSMIT_QUEUE_LENGTH 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2a0dd6a03847a7a740f9ae98d4894530412ba5c8
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217989"
---
# <a name="oid_gen_transmit_queue_length"></a>OID \_ 代 \_ 传输 \_ 队列 \_ 长度


作为查询，OID \_ 代 \_ 传输 \_ 队列 \_ 长度 OID 指定当前排队等待传输的数据包数，无论是在 NIC 上还是在驱动程序内部队列中。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-drivers"></a>NDIS 6.0 和更高版本驱动程序  
可选。

<a href="" id="ndis-5-1-drivers"></a>NDIS 5.1 驱动程序  
可选。

<a href="" id="windows-xp"></a>Windows XP  
支持。

<a href="" id="ndis-5-1-drivers"></a>NDIS 5.1 驱动程序  
可选。

<a name="remarks"></a>备注
-------

对于查询，返回的数值总是当前排队的数据包总数。 此数目可以包括在 NDIS 库中排队的未提交的发送请求。

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

 

