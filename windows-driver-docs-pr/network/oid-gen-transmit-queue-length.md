---
title: OID_GEN_TRANSMIT_QUEUE_LENGTH
description: 为查询，OID_GEN_TRANSMIT_QUEUE_LENGTH OID 指定是否在 NIC 上或驱动程序内部队列中当前排队等待传输的数据包数。
ms.assetid: 042a7df3-a204-45f8-b147-96def7438b4a
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_TRANSMIT_QUEUE_LENGTH 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 8624ec39678dde434a1bf1661e137b623f4d8a88
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385737"
---
# <a name="oidgentransmitqueuelength"></a>OID\_GEN\_传输\_队列\_长度


为查询，OID\_GEN\_传输\_队列\_长度 OID 指定是否在 NIC 上或驱动程序内部队列中当前排队等待传输的数据包数。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-drivers"></a>NDIS 6.0 和更高版本的驱动程序  
可选。

<a href="" id="ndis-5-1-drivers"></a>NDIS 5.1 驱动程序  
可选。

<a href="" id="windows-xp"></a>Windows XP  
支持。

<a href="" id="ndis-5-1-drivers"></a>NDIS 5.1 驱动程序  
可选。

<a name="remarks"></a>备注
-------

对于查询，将始终的数据包总数当前正在排队返回的数字。 此数字可以包含未提交的发送请求排队 NDIS 库中。

有关 Oid 的统计信息的常规信息，请参阅[General Statistics](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-general-statistics-oids)。

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


[OID\_GEN\_STATISTICS](oid-gen-statistics.md)

 

 




