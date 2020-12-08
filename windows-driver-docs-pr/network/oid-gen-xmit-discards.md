---
title: OID_GEN_XMIT_DISCARDS
description: 作为查询，NDIS 和过量驱动程序使用 OID_GEN_XMIT_DISCARDS OID 来确定微型端口适配器上丢弃的传输数。
ms.date: 11/01/2019
keywords: -从 Windows Vista 开始 OID_GEN_XMIT_DISCARDS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: fee6ee6fe087a893358e54216e0a172d60210be2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782211"
---
# <a name="oid_gen_xmit_discards"></a>OID \_ 生成 \_ XMIT \_ 放弃


作为查询，NDIS 和过量驱动程序使用 OID \_ GEN \_ XMIT \_ 丢弃 oid 来确定微型端口适配器上丢弃的传输数。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。  (参见 "备注" 部分) 

<a name="remarks"></a>备注
-------

NDIS 处理微型端口驱动程序的此 OID。 有关统计信息的详细信息，请参阅 [OID \_ GEN \_ STATISTICS](oid-gen-statistics.md) OID。

此 OID 返回的计数是接口丢弃的数据包数。 计数与 RFC 2863 中所述的 *ifOutDiscards* 计数器完全相同。

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

 

 




