---
title: OID_TCP_TASK_IPSEC_OFFLOAD_V2_UPDATE_SA
description: 作为一组 TCP/IP 传输使用 OID_TCP_TASK_IPSEC_OFFLOAD_V2_UPDATE_SA OID 请求微型端口驱动程序更新指定的安全关联 (Sa) 上的 nic。
ms.assetid: 22849103-9148-4621-b78f-b9f34f2c7ac1
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_TCP_TASK_IPSEC_OFFLOAD_V2_UPDATE_SA 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e841825a7b13c740cbf979088ee2ba9e06d4d0bf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523029"
---
# <a name="oidtcptaskipsecoffloadv2updatesa"></a>OID\_TCP\_TASK\_IPSEC\_OFFLOAD\_V2\_UPDATE\_SA


\[IPsec 任务卸载功能已弃用，不应使用。\]

作为一组 TCP/IP 传输使用 OID\_TCP\_任务\_IPSEC\_卸载\_V2\_更新\_SA OID 以请求微型端口驱动程序更新指定的安全性NIC 上的关联 (Sa)

**请注意**  NDIS 支持此 OID 与 direct 的 OID 请求接口。 有关直接 OID 请求接口的详细信息，请参阅[NDIS 6.1 直接 OID 请求接口](https://msdn.microsoft.com/library/windows/hardware/ff564736)。

 

<a name="remarks"></a>备注
-------

所有 NDIS 6.1 微型端口驱动程序支持 IPsec 都卸载版本 2 (IPsecOV2) 必须支持此 OID。

该驱动程序微型端口驱动程序接收此请求时，应更新 NIC 上指定的 SAs 微型端口驱动程序可能会失败此请求，如果找不到 SA 或 ESN 不受支持。 在这种情况下，返回的状态应为 NDIS\_状态\_无效\_参数。

微型端口驱动程序收到[ **IPSEC\_卸载\_V2\_更新\_SA** ](https://msdn.microsoft.com/library/windows/hardware/ff556990)结构，其中包含有关更新的信息和指向下一步 IPSEC\_卸载\_V2\_更新\_SA 结构链接列表中的。

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
<td><p>支持 NDIS 6.1 及更高版本。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**IPSEC\_OFFLOAD\_V2\_UPDATE\_SA**](https://msdn.microsoft.com/library/windows/hardware/ff556990)

 

 




