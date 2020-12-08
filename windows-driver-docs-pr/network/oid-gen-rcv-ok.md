---
title: OID_GEN_RCV_OK
description: 作为查询，OID_GEN_RCV_OK OID 指定 NIC 接收的不出错的帧数，并指示绑定的协议。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_RCV_OK 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 3a7a932015260bf800b83cd0ef4ceace18801e38
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818849"
---
# <a name="oid_gen_rcv_ok"></a>OID \_ 生成 \_ RCV \_ 正常


作为查询，OID \_ GEN \_ RCV \_ OK OID 指定 NIC 接收的不出错的帧数，并指示绑定的协议。

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

OID \_ GEN \_ RCV \_ OK 指定接收的没有错误的帧数。 但是， [OID 生成 \_ \_ 统计](oid-gen-statistics.md) 信息不包括此信息。

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

## <a name="see-also"></a>请参阅


[OID \_ 生成 \_ 统计信息](oid-gen-statistics.md)

 

