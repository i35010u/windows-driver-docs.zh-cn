---
title: OID_WWAN_CREATE_MAC
description: OID_WWAN_CREATE_MAC 请求微型端口驱动程序，以创建新的 NDIS 端口。
ms.assetid: 4EF98858-86CD-409B-BE41-E57B24158609
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_CREATE_MAC 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 0d1a9d416aa8890ca81aa0dd9ae54d3183bd5aad
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386725"
---
# <a name="oidwwancreatemac"></a>OID\_WWAN\_CREATE\_MAC


OID\_WWAN\_创建\_MAC 请求微型端口驱动程序，以创建新的 NDIS 端口。 将此新的 NDIS 端口上发送的其他 PDP 上下文的上下文激活请求。

微型端口驱动程序必须处理集请求，一开始以异步方式返回 NDIS\_状态\_指示\_原始请求和更高版本完成与请求的必需[ **NDIS\_WWAN\_MAC\_信息**](https://msdn.microsoft.com/library/windows/hardware/dn449747)结构，指示 NDIS 端口号和 MAC 地址与端口相关联。

不支持查询请求。

<a name="remarks"></a>备注
-------

微型端口驱动程序必须处理请求以创建 （激活） 新的 NDIS 端口以异步方式以防止死锁。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>在 Windows 8.1 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_WWAN\_MAC\_INFO**](https://msdn.microsoft.com/library/windows/hardware/dn449747)

[OID\_WWAN\_DELETE\_MAC](oid-wwan-delete-mac.md)

 

 




