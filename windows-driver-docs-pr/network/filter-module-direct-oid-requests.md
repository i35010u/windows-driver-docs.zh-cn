---
title: 筛选器模块直接 OID 请求
description: 筛选器模块直接 OID 请求
ms.assetid: 0ab7079b-6578-4932-a276-40a961b55efe
keywords:
- 直接 OID 请求接口 WDK 网络
- 直接 OID 请求路径 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 049fc5adfe6b237310ebdcdc4262c8708bcdc0ec
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350011"
---
# <a name="filter-module-direct-oid-requests"></a>筛选器模块直接 OID 请求





若要支持直接的 OID 请求路径，筛选器驱动程序提供*FilterXxx*中的函数入口点[ **NDIS\_筛选器\_驱动程序\_特征** ](https://msdn.microsoft.com/library/windows/hardware/ff565515)结构和 NDIS 提供**NdisF * Xxx*** 的筛选器驱动程序函数。

*直接 OID 请求接口*类似于标准的 OID 请求接口。 例如， [ **NdisFDirectOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561809)并[ *FilterDirectOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff549931)函数是类似于[**NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)并[ *FilterOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff549954)函数。

**请注意**  NDIS 6.1 和更高版本支持特定 Oid 用于直接 OID 请求接口。 不支持 NDIS 6.1 和一些 NDIS 6.1 Oid 之前即已存在的 Oid。 若要确定是否可以直接 Oid 界面中使用 OID，请参阅 OID 引用页。 有关示例，请参阅中的说明[OID\_TCP\_任务\_IPSEC\_卸载\_V2\_添加\_SA](https://msdn.microsoft.com/library/windows/hardware/ff569812) OID。

 

筛选器驱动程序必须能够处理不会序列化的直接 OID 请求。 与标准的 OID 请求接口，不同 NDIS 不序列化与使用直接的 OID 接口或使用标准的 OID 请求接口发送其他请求直接 OID 请求。 此外，筛选器驱动程序必须能够处理直接 OID 请求在 IRQL &lt;= 调度\_级别。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549931" data-raw-source="[&lt;em&gt;FilterDirectOidRequest&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549931)"><em>FilterDirectOidRequest</em></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549954" data-raw-source="[&lt;em&gt;FilterOidRequest&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549954)"><em>FilterOidRequest</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549908" data-raw-source="[&lt;em&gt;FilterCancelDirectOidRequest&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549908)"><em>FilterCancelDirectOidRequest</em></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549911" data-raw-source="[&lt;em&gt;FilterCancelOidRequest&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549911)"><em>FilterCancelOidRequest</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549933" data-raw-source="[&lt;em&gt;FilterDirectOidRequestComplete&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549933)"><em>FilterDirectOidRequestComplete</em></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549956" data-raw-source="[&lt;em&gt;FilterOidRequestComplete&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549956)"><em>FilterOidRequestComplete</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561809" data-raw-source="[&lt;strong&gt;NdisFDirectOidRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561809)"><strong>NdisFDirectOidRequest</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561830" data-raw-source="[&lt;strong&gt;NdisFOidRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561830)"><strong>NdisFOidRequest</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561815" data-raw-source="[&lt;strong&gt;NdisFDirectOidRequestComplete&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561815)"><strong>NdisFDirectOidRequestComplete</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561815" data-raw-source="[&lt;strong&gt;NdisFDirectOidRequestComplete&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561815)"><strong>NdisFDirectOidRequestComplete</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561788" data-raw-source="[&lt;strong&gt;NdisFCancelDirectOidRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561788)"><strong>NdisFCancelDirectOidRequest</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561792" data-raw-source="[&lt;strong&gt;NdisFCancelOidRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561792)"><strong>NdisFCancelOidRequest</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 





