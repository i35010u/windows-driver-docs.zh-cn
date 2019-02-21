---
title: OID_GEN_ISOLATION_PARAMETERS
description: NDIS 和基础驱动程序发出 OID_GEN_ISOLATION_PARAMETERS 对象标识符 (OID) 的请求，以获取 VM 网络适配器的端口设置的 （隔离） 参数的多租户配置。
ms.assetid: 68E89349-4907-4241-9C50-B13C75273F0D
ms.date: 08/08/2017
keywords: -OID_GEN_ISOLATION_PARAMETERS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6b06fb11539b35acde945f1d25b4646e52deebb6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555376"
---
# <a name="oidgenisolationparameters"></a>OID\_GEN\_隔离\_参数


NDIS 和基础驱动程序发出的 OID 的对象标识符 (OID) 请求\_GEN\_隔离\_参数来获取在 VM 设置的 （隔离） 参数的多租户配置网络适配器的端口。

尽管在端口上单独配置每个路由域，但此 OID 单个查询中返回参数的所有路由域。

基础驱动程序应发出此 OID 中两个步骤：

1.  Io 查询所需的缓冲区大小，发出与 OID 查询**大小**的成员**标头**的成员[ **NDIS\_隔离\_参数**](https://msdn.microsoft.com/library/windows/hardware/dn383679)结构设置为**NDIS\_SIZEOF\_NDIS\_隔离\_参数\_修订\_1**. (请参阅**NDIS\_状态\_无效\_长度**下面。)
2.  发出使用 OID **InformationBuffer**的所需的大小。

如果成功，完成 OID 查询请求**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含指向缓冲区的指针。 此缓冲区包含订单中的以下数据：

1.  [ **NDIS\_隔离\_参数**](https://msdn.microsoft.com/library/windows/hardware/dn383679)结构

2.  一个或多个[ **NDIS\_路由\_域\_条目**](https://msdn.microsoft.com/library/windows/hardware/dn383681)结构，一个用于每个路由域

3.  一个或多个[ **NDIS\_路由\_域\_隔离\_条目**](https://msdn.microsoft.com/library/windows/hardware/dn383684)结构，按路由域分组

在每个[ **NDIS\_路由\_域\_条目**](https://msdn.microsoft.com/library/windows/hardware/dn383681)结构**FirstIsolationInfoEntryOffset**成员包含从 OID 信息缓冲区开头的偏移量 (即，缓冲区开头的**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构指向) 与第一个[ **NDIS\_路由\_域\_隔离\_条目**](https://msdn.microsoft.com/library/windows/hardware/dn383684)为该路由域。 中的偏移量**NextIsolationInfoEntryOffset**列表中的最后一个结构的成员为零。

如果 VM 网络适配器上不设置任何多租户配置参数，则网络适配器的微型端口驱动程序设置**数据。查询\_信息。BytesWritten**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)为零，并返回结构**NDIS\_状态\_成功**。 在此情况下中的数据**数据。查询\_INFORMATION.InformationBuffer**微型端口驱动程序不修改成员。

<a name="remarks"></a>备注
-------

### <a name="return-status-codes"></a>返回状态代码

VM 网络适配器的微型端口驱动程序返回一个此 OID 请求的以下状态代码：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状态代码</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>NDIS_STATUS_SUCCESS</strong></p></td>
<td><p>OID 请求已成功完成。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_INVALID_LENGTH</strong></p></td>
<td><p>信息缓冲区长度太小，无法返回所请求的信息。 VM 网络适配器的微型端口驱动程序设置<strong>数据。METHOD_INFORMATION。BytesNeeded</strong>中的成员<a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>到最小缓冲区大小，以字节为单位，所需的结构。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_FAILURE</strong></p></td>
<td><p>请求由于其他原因而失败。</p></td>
</tr>
</tbody>
</table>

 

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
<td><p>支持 NDIS 6.40 及更高版本。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_隔离\_参数**](https://msdn.microsoft.com/library/windows/hardware/dn383679)

[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_路由\_域\_条目**](https://msdn.microsoft.com/library/windows/hardware/dn383681)

[**NDIS\_路由\_域\_隔离\_条目**](https://msdn.microsoft.com/library/windows/hardware/dn383684)

[**NDIS\_状态\_隔离\_参数\_更改**](ndis-status-isolation-parameters-change.md)

 

 




