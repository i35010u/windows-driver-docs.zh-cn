---
title: OID_GEN_DIRECTED_BYTES_RCV
description: 作为查询，OID_GEN_DIRECTED_BYTES_RCV OID 指定接收的数据包中的字节数，接收时没有错误。
ms.assetid: 435941b5-647f-4c5f-84ef-7b4b832c452e
ms.date: 11/01/2019
keywords: -从 Windows Vista 开始 OID_GEN_DIRECTED_BYTES_RCV 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 75834c9e8bc32f3bbf1714b4a94d66302f5f2b57
ms.sourcegitcommit: b8876f616ac625bb3f38218a32b2dc35ac7b3399
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2019
ms.locfileid: "73443005"
---
# <a name="oid_gen_directed_bytes_rcv"></a>OID\_代\_定向\_字节\_RCV


作为查询，OID\_代\_定向\_字节\_RCV OID 指定接收的定向数据包中的字节数，这些字节是不出错的。

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

计数与 RFC 2863 中所述的*ifInUcastPkts*计数器完全相同。

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

 

 




