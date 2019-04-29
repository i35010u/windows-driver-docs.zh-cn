---
title: OID_GEN_TRANSMIT_QUEUE_LENGTH
description: 为查询，OID_GEN_TRANSMIT_QUEUE_LENGTH OID 指定是否在 NIC 上或驱动程序内部队列中当前排队等待传输的数据包数。
ms.assetid: 042a7df3-a204-45f8-b147-96def7438b4a
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_TRANSMIT_QUEUE_LENGTH 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: dd17076dfd7b0743409e37e6ad6ad2479a30e5cb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387869"
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

有关 Oid 的统计信息的常规信息，请参阅[General Statistics](https://msdn.microsoft.com/library/windows/hardware/ff552485)。

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

 

 




