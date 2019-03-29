---
title: 微型端口适配器直接 OID 请求
description: 微型端口适配器直接 OID 请求
ms.assetid: 63ced5a3-0c83-4952-aa0e-c3c654b3f241
keywords:
- 直接 OID 请求接口 WDK 网络
- 直接 OID 请求路径 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb6e42d4d5d722722174264794c7303b095a5706
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566921"
---
# <a name="miniport-adapter-direct-oid-requests"></a>微型端口适配器直接 OID 请求





若要支持直接的 OID 请求路径，微型端口驱动程序提供*MiniportXxx*中的函数入口点[ **NDIS\_微型端口\_驱动程序\_特征**](https://msdn.microsoft.com/library/windows/hardware/ff565958)结构和 NDIS 提供**NdisM * Xxx*** 微型端口驱动程序的函数。

*直接 OID 请求接口*类似于标准的 OID 请求接口。 例如， [ **NdisMDirectOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563582)并[ *MiniportDirectOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559371)函数是类似于[**NdisMOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563622)并[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)函数。

**请注意**  NDIS 6.1 支持特定 Oid 与 direct 的 OID 请求接口一起使用。 不支持 NDIS 6.1 和一些 NDIS 6.1 Oid 之前即已存在的 Oid。 若要确定是否可以直接 Oid 界面中使用 OID，请参阅 OID 引用页。 

微型端口驱动程序必须能够处理不会序列化的直接 OID 请求。 与标准的 OID 请求接口，不同 NDIS 不序列化与使用直接的 OID 接口或使用标准的 OID 请求接口发送其他请求直接 OID 请求。 此外，微型端口驱动程序必须能够处理直接 OID 请求在 IRQL &lt;= 调度\_级别。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559371" data-raw-source="[&lt;em&gt;MiniportDirectOidRequest&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559371)"><em>MiniportDirectOidRequest</em></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559416" data-raw-source="[&lt;em&gt;MiniportOidRequest&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559416)"><em>MiniportOidRequest</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559335" data-raw-source="[&lt;em&gt;MiniportCancelDirectOidRequest&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559335)"><em>MiniportCancelDirectOidRequest</em></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559339" data-raw-source="[&lt;em&gt;MiniportCancelOidRequest&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559339)"><em>MiniportCancelOidRequest</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563582" data-raw-source="[&lt;strong&gt;NdisMDirectOidRequestComplete&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563582)"><strong>NdisMDirectOidRequestComplete</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563622" data-raw-source="[&lt;strong&gt;NdisMOidRequestComplete&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563622)"><strong>NdisMOidRequestComplete</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 





