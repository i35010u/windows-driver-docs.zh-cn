---
title: OID_GEN_XMIT_ERROR
description: 作为查询，OID_GEN_XMIT_ERROR OID 指定了 NIC 无法传输的帧数。
ms.assetid: c4f42271-812b-4da9-8280-79d3bddc5164
ms.date: 11/01/2019
keywords: -从 Windows Vista 开始 OID_GEN_XMIT_ERROR 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2a1a2bcdf2183c422b6d209d0e8966d1d282266d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208647"
---
# <a name="oid_gen_xmit_error"></a>OID \_ 生成 \_ XMIT \_ 错误


作为查询，OID \_ GEN \_ XMIT \_ 错误 OID 指定了 NIC 无法传输的帧数。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
已过时。

<a href="" id="ndis-6-0-and-later-drivers"></a>NDIS 6.0 和更高版本驱动程序  
未请求。 请改用 [OID 生成 \_ \_ 统计信息](oid-gen-statistics.md) 。

<a href="" id="ndis-5-1-drivers"></a>NDIS 5.1 驱动程序  
必需。

<a href="" id="windows-xp"></a>Windows XP  
支持。

<a href="" id="ndis-5-1-drivers"></a>NDIS 5.1 驱动程序  
必需。

<a name="remarks"></a>备注
-------

计数与 RFC 2863 中所述的 *ifOutErrors* 计数器完全相同。

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

 

