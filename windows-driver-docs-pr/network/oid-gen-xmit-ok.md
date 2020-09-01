---
title: OID_GEN_XMIT_OK
description: 作为查询，OID_GEN_XMIT_OK OID 指定了在不出错的情况下传输的帧数。
ms.assetid: ac7120a3-58bb-4047-b4b7-ad9fbaf14e4f
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_XMIT_OK 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 42088b6f86516939082d51be73e3fb93a56b9966
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209685"
---
# <a name="oid_gen_xmit_ok"></a>OID \_ 生成 \_ XMIT \_ 正常


作为查询，OID \_ GEN \_ XMIT \_ OK OID 指定了在没有错误的情况下传输的帧数。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-drivers"></a>NDIS 6.0 和更高版本驱动程序  
必需。

<a href="" id="ndis-5-1-drivers"></a>NDIS 5.1 驱动程序  
必需。

<a href="" id="windows-xp"></a>Windows XP  
支持。

<a href="" id="ndis-5-1-drivers"></a>NDIS 5.1 驱动程序  
必需。

<a name="remarks"></a>备注
-------

OID \_ GEN \_ XMIT \_ OK 指定传输的不含错误的帧数。 但是， [OID 生成 \_ \_ 统计](oid-gen-statistics.md) 信息不包括此信息。

注意：统计信息 Oid 对于 NDIS 6.0 和更高的微型端口驱动程序是必需的，除非 NDIS 处理它们。 有关统计信息 Oid 的一般信息，请参阅 [常规统计](./ndis-general-statistics-oids.md)信息。

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

 

