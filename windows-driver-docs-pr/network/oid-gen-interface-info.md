---
title: OID_GEN_INTERFACE_INFO
description: 为查询，使用 OID_GEN_INTERFACE_INFO OID 来获取网络接口的当前状态和统计信息。
ms.assetid: fa1dd52f-7cf6-4e95-af15-02ae65fcb872
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_INTERFACE_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 3a094db6a5c26df79dac06e9fcf879ec2d9a33da
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575316"
---
# <a name="oidgeninterfaceinfo"></a>OID\_GEN\_接口\_信息


为查询，使用 OID\_GEN\_接口\_信息 OID，若要获取网络接口的当前状态和统计信息。

**版本信息**

<a href="" id="windows-vista-and-later"></a>Windows Vista 及更高版本  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 NDIS 接口提供程序仅。

<a name="remarks"></a>备注
-------

仅[NDIS 网络接口](https://msdn.microsoft.com/library/windows/hardware/ff566527)提供程序，因此不微型端口驱动程序或筛选器驱动程序必须支持此 OID 作为 OID 的请求。

如果查询成功，接口提供程序返回 NDIS\_状态\_成功和查询的结果是[ **NDIS\_接口\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff565736)结构。 此结构包含接口的生存期内更改的信息。

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


[**NDIS\_接口\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff565736)

[NDIS 网络接口 Oid](https://msdn.microsoft.com/library/windows/hardware/ff566545)

 

 




