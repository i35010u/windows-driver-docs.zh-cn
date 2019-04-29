---
title: 协议驱动程序直接 OID 请求
description: 协议驱动程序直接 OID 请求
ms.assetid: 387d27de-3214-4f93-8f45-9a2f28e5036f
keywords:
- 直接 OID 请求接口 WDK 网络
- 直接 OID 请求路径 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1faea9159af9c0ec03a8efe654eebd29f2a7b65f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373868"
---
# <a name="protocol-driver-direct-oid-requests"></a>协议驱动程序直接 OID 请求





若要支持直接的 OID 请求路径，协议驱动程序提供*ProtocolXxx*中的函数入口点[ **NDIS\_协议\_驱动程序\_特征**](https://msdn.microsoft.com/library/windows/hardware/ff566825)结构和 NDIS 提供**Ndis * Xxx*** 协议驱动程序的函数。

*直接 OID 请求接口*类似于标准的 OID 请求接口。 例如， [ **NdisDirectOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561746)并[ **ProtocolDirectOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff570259)函数是类似于[ **NdisOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff563710)并[ **ProtocolOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff570264)函数。

**请注意**  NDIS 6.1 和更高版本支持特定 Oid 用于直接 OID 请求接口。 不支持 NDIS 6.1 和一些 NDIS 6.1 Oid 之前即已存在的 Oid。 若要确定是否可以直接 Oid 界面中使用 OID，请参阅 OID 引用页。 有关示例，请参阅中的说明[OID\_TCP\_任务\_IPSEC\_卸载\_V2\_添加\_SA](https://msdn.microsoft.com/library/windows/hardware/ff569812) OID。

 

若要支持直接的 Oid 请求接口，使用标准的 OID 请求接口的文档。 下表显示了直接的 OID 请求接口中的函数和标准的 OID 请求接口之间的关系。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">直接 OID 函数</th>
<th align="left">标准 OID 函数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570259" data-raw-source="[&lt;strong&gt;ProtocolDirectOidRequestComplete&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570259)"><strong>ProtocolDirectOidRequestComplete</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570264" data-raw-source="[&lt;strong&gt;ProtocolOidRequestComplete&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570264)"><strong>ProtocolOidRequestComplete</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561746" data-raw-source="[&lt;strong&gt;NdisDirectOidRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561746)"><strong>NdisDirectOidRequest</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563710" data-raw-source="[&lt;strong&gt;NdisOidRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563710)"><strong>NdisOidRequest</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561621" data-raw-source="[&lt;strong&gt;NdisCancelDirectOidRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561621)"><strong>NdisCancelDirectOidRequest</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561622" data-raw-source="[&lt;strong&gt;NdisCancelOidRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561622)"><strong>NdisCancelOidRequest</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 





