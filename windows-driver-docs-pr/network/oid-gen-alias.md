---
title: OID_GEN_ALIAS
description: 为查询，使用 OID_GEN_ALIAS OID 获取的接口 (RFC 2863 从 ifAlias) 的别名字符串。 版本信息 Windows Vista 和 laterSupported。 NDIS 6.0 和更高版本的微型端口 driversNot 请求。 NDIS 接口提供程序仅。
ms.assetid: ff5e6494-aa4e-4a0a-b773-64b612236c8c
ms.date: 08/08/2017
keywords: -OID_GEN_ALIAS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 361c0dfc20777c407824a41c82b062a0f1ea718c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385502"
---
# <a name="oidgenalias"></a>OID\_常规\_别名


为查询，使用 OID\_GEN\_别名 OID 获取接口的别名字符串 (*ifAlias*从[RFC 2863](https://go.microsoft.com/fwlink/p/?linkid=84054))。

**版本信息**

<a href="" id="windows-vista-and-later"></a>Windows Vista 及更高版本  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 NDIS 接口提供程序仅。

<a name="remarks"></a>备注
-------

[NDIS 网络接口](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interfaces2)提供程序可以将分配为它的接口的唯一别名字符串。 如果名称应保持相同的接口与相关联，该提供程序可以使计算机重新启动后持久的字符串和需重新初始化。

仅 NDIS 网络接口提供程序，并因此不微型端口驱动程序或筛选器驱动程序必须支持此 OID 作为 OID 的请求。

如果接口提供程序返回 NDIS\_状态\_成功后，查询的结果是在 NDIS 中返回的别名字符串\_IF\_盘点\_字符串结构。

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


[NDIS 网络接口 Oid](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interface-oids)

 

 




