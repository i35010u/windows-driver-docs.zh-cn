---
title: OID_GEN_LINK_SPEED
description: 作为查询，OID_GEN_LINK_SPEED OID 指定 NIC 的最大速度。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_LINK_SPEED 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: aef4927b8e17784fa3fddca2a8672df14175d6da
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827567"
---
# <a name="oid_gen_link_speed"></a>OID \_ GEN \_ LINK \_ 速度


作为查询，OID 生成 \_ \_ 链接 \_ 速度 oid 指定 NIC 的最大速度。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
已过时。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
已过时。  (参见 "备注" 部分) 

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需。

<a href="" id="windows-xp"></a>Windows XP  
支持。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需。

<a name="remarks"></a>备注
-------

[Oid 生成 \_ \_ 链接 \_ 状态](oid-gen-link-state.md)为 NDIS 6.0 和更高版本以及此 oid 的更高版本。 但是，NDIS 6.0 和更高的微型端口驱动程序必须改为使用 [**ndis \_ 状态 \_ 链接 \_ 状态**](./ndis-status-link-state.md) 指示来指示链接速度发生变化。

度量单位为 100 bps，因此值100000表示硬件比特率为 10 Mbps。

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


[**NDIS \_ 状态 \_ 链接 \_ 状态**](./ndis-status-link-state.md)

[OID \_ 生成 \_ 链接 \_ 状态](oid-gen-link-state.md)

 

