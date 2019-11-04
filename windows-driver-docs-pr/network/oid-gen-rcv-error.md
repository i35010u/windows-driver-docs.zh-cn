---
title: OID_GEN_RCV_ERROR
description: 作为查询，OID_GEN_RCV_ERROR OID 指定 NIC 接收的帧数量，但不会因错误而指示协议。
ms.assetid: 0481f225-869f-4313-9bc5-7af1de0b7d2d
ms.date: 11/01/2019
keywords: -从 Windows Vista 开始 OID_GEN_RCV_ERROR 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 784834bbdf94baa97e5a895c7086d76f2d8bcc4a
ms.sourcegitcommit: b8876f616ac625bb3f38218a32b2dc35ac7b3399
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2019
ms.locfileid: "73443015"
---
# <a name="oid_gen_rcv_error"></a>OID\_GEN\_RCV\_错误


作为查询，OID\_GEN\_RCV\_错误 OID 指定 NIC 接收的帧数量，但不会因错误而指示协议。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
已过时。

<a href="" id="ndis-6-0-and-later-drivers"></a>NDIS 6.0 和更高版本驱动程序  
未请求。 改用[OID\_代\_统计信息](oid-gen-statistics.md)。

<a href="" id="ndis-5-1-drivers"></a>NDIS 5.1 驱动程序  
必需.

<a href="" id="windows-xp"></a>Windows XP  
支持。

<a href="" id="ndis-5-1-drivers"></a>NDIS 5.1 驱动程序  
必需.

<a name="remarks"></a>备注
-------

计数与 RFC 2863 中所述的*ifInErrors*计数器完全相同。

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

 

 




