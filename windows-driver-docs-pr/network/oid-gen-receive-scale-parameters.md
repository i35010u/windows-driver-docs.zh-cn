---
title: OID_GEN_RECEIVE_SCALE_PARAMETERS
description: 为查询，NDIS 和基础驱动程序可以使用 OID_GEN_RECEIVE_SCALE_PARAMETERS OID 查询当前接收端缩放 (RSS) 参数的 nic。
ms.assetid: a54190f7-0d2e-4f85-84c2-05fc9ec4994a
ms.date: 08/08/2017
keywords: -OID_GEN_RECEIVE_SCALE_PARAMETERS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ebd164b14c13c5ca30fdec357c1225afcae3d9e7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545658"
---
# <a name="oidgenreceivescaleparameters"></a>OID\_GEN\_RECEIVE\_SCALE\_PARAMETERS


为查询，NDIS 和基础驱动程序可以使用 OID\_GEN\_接收\_规模\_参数 OID 来查询当前接收端缩放 (RSS) 参数的 nic。 返回 NDIS [ **NDIS\_接收\_规模\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567228)结构，它定义当前的 RSS 参数。

作为一组 NDIS 和基础驱动程序使用 OID\_GEN\_接收\_规模\_参数 OID，若要设置的 nic。 当前的 RSS 参数 微型端口驱动程序将收到 NDIS\_接收\_规模\_定义 RSS 参数的参数结构。

> [!NOTE]
> 在 RSSv2，此 OID 是仅用于查询给定缩放实体的当前 RSS 参数。 有关支持 RSSv2 的微型端口驱动程序，请参阅[OID_GEN_RECEIVE_SCALE_PARAMETERS_V2](oid-gen-receive-scale-parameters-v2.md)设置 RSS 间接表以外的参数。

<a name="remarks"></a>备注
-------

NDIS 微型端口驱动程序，请查询未请求和集是用于支持 RSS 的驱动程序。 NDIS 处理查询的微型端口驱动程序。

TCP/IP 驱动程序配置 IPv4 和 IPv6 使用单个 OID 设置请求的 OID\_GEN\_接收\_规模\_参数。 也就是说，当堆栈应为 IPv4 和 IPv6 启用 RSS，它会设置这两个中的相应标志**HashInformation**的成员[ **NDIS\_接收\_规模\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567228)结构并将其发送一个 OID 请求。 此外，IPv4 和 IPv6 使用相同的机密密钥，密钥将始终为 40 个字节，即使仅 IPv4 环境中启用。

基础的微型端口适配器必须使用最新的 OID\_GEN\_接收\_规模\_参数 OID 设置已收到。 例如，如果微型端口获取 OID\_GEN\_接收\_规模\_参数 OID 与 IPv4 哈希类型缺少，它必须禁用 IPv4 RSS，如果之前已启用。

**请注意**  过量的驱动程序可以使用[OID\_常规\_接收\_哈希](oid-gen-receive-hash.md)OID 来启用和配置上的哈希计算接收帧，而不启用 RSS。

 

**请注意**  驱动程序必须禁用的协议接收哈希计算 ([OID\_常规\_接收\_哈希](oid-gen-receive-hash.md)) 它们启用 RSS 之前。 如果启用了 RSS，协议驱动程序禁用 RSS 之前这样，将接收哈希计算。 微型端口驱动程序应失败的集请求**NDIS\_状态\_无效\_OID**或**NDIS\_状态\_不\_支持**若要启用 RSS，如果 OID\_代\_接收\_哈希当前已启用。

 

**请注意**  间接表和密钥后将追加[ **NDIS\_接收\_规模\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567228)结构成员。 有关间接寻址表和机密密钥的详细信息，请参阅**NDIS\_接收\_规模\_参数**。

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>支持 NDIS 6.0 及更高版本。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_RECEIVE\_SCALE\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff567228)

[OID\_GEN\_RECEIVE\_HASH](oid-gen-receive-hash.md)

 

 




