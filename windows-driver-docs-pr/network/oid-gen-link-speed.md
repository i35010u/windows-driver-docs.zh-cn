---
title: OID_GEN_LINK_SPEED
description: 为查询，OID_GEN_LINK_SPEED OID 指定 NIC 的最大速度
ms.assetid: f8ee887a-969e-4167-9b39-9ee6ef8b1fbc
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_LINK_SPEED 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 097bc08b6a61f54b242d1ab844e23f2b94964a31
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520599"
---
# <a name="oidgenlinkspeed"></a>OID\_GEN\_链接\_速度


为查询，OID\_GEN\_链接\_速度 OID 指定 NIC 的最大速度

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
已过时。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
已过时。 (请参阅备注部分)

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需。

<a href="" id="windows-xp"></a>Windows XP  
支持。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需。

<a name="remarks"></a>备注
-------

[OID\_代\_链接\_状态](oid-gen-link-state.md)是 NDIS 6.0 和更高版本及更高版本的此 OID 的等效项。 但是 NDIS 6.0 和更高版本的微型端口驱动程序必须使用[ **NDIS\_状态\_链接\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567391)状态指示相反来指示链接速度会更改。

度量单位是 100 bps，因此值为 100,000 表示的硬件比特率为 10 Mbps。

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
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_STATUS\_LINK\_STATE**](https://msdn.microsoft.com/library/windows/hardware/ff567391)

[OID\_GEN\_LINK\_STATE](oid-gen-link-state.md)

 

 




