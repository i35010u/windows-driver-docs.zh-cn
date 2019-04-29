---
title: OID_GEN_RECEIVE_HASH
description: 为查询，NDIS 和基础驱动程序使用 OID_GEN_RECEIVE_HASH OID 获取微型端口适配器的当前接收哈希计算设置。
ms.assetid: be120dab-c98d-418f-8777-e2fb37b774a1
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_RECEIVE_HASH 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 9b43c1e6e16220ce2b3fcfd1693ff79e73281188
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391029"
---
# <a name="oidgenreceivehash"></a>OID\_GEN\_RECEIVE\_HASH


为查询，NDIS 和基础驱动程序使用 OID\_GEN\_接收\_哈希 OID，若要获取当前接收哈希计算的微型端口适配器使用的设置。 返回 NDIS [ **NDIS\_接收\_哈希\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567190)结构，其中包含当前接收哈希设置。

作为一组 NDIS 和基础驱动程序使用 OID\_GEN\_接收\_微型端口适配器上配置的接收哈希计算的哈希 OID。 微型端口驱动程序将收到 NDIS\_接收\_哈希\_参数结构。

<a name="remarks"></a>备注
-------

NDIS 微型端口驱动程序，请查询不请求。

对此 OID 集是可选的微型端口驱动程序，包括支持 RSS 的支持。

基础驱动程序可以使用 OID\_GEN\_接收\_要启用和配置上的哈希计算的哈希 OID 收到帧，而不启用 RSS。

**请注意**  协议驱动程序必须禁用接收哈希计算之前它们启用 RSS。 如果启用了 RSS，协议驱动程序禁用 RSS 之前这样，将接收哈希计算。 微型端口驱动程序应失败的集请求**NDIS\_状态\_无效\_OID**或**NDIS\_状态\_不\_支持**若要启用哈希计算，如果收到[OID\_常规\_接收\_规模\_参数](oid-gen-receive-scale-parameters.md)当前已启用。

 

**请注意**  机密密钥追加之后[ **NDIS\_接收\_哈希\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567190)结构成员。

 

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
<td><p>支持 NDIS 6.0 及更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_RECEIVE\_HASH\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff567190)

 

 




