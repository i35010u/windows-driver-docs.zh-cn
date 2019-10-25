---
title: 查询和更改 RSC 状态
description: 本部分介绍如何查询或更改支持 RSC 的微型端口驱动程序的当前接收段合并（RSC）状态。
ms.assetid: 5455FBB2-3603-44EF-B1C6-494D31DD820D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b35a3494657abfd6a58b492872902539a17f993
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844887"
---
# <a name="querying-and-changing-rsc-state"></a>查询和更改 RSC 状态


本部分介绍如何查询或更改支持 RSC 的微型端口驱动程序的当前接收段合并（RSC）状态。

## <a name="querying-rsc-state"></a>正在查询 RSC 状态


可以通过发出[OID\_TCP\_卸载\_当前\_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config) OID 请求来查询当前 RSC 状态。 NDIS 处理此 OID，但不将其向下传递到小型端口。

## <a name="changing-rsc-state"></a>更改 RSC 状态


可以通过[\_TCP\_卸载\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters)OID 请求，来启用或禁用 RSC。 此 OID 使用[**NDIS\_卸载\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)结构。 在此结构中， **RscIPv4**和**RscIPv6**成员可以具有以下值：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">术语</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong></p></td>
<td align="left"><p>RSC 状态保持不变。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>NDIS_OFFLOAD_PARAMETERS_RSC_DISABLED</strong></p></td>
<td align="left"><p>指定此标志可禁用 RSC。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>NDIS_OFFLOAD_PARAMETERS_RSC_ENABLED</strong></p></td>
<td align="left"><p>指定此标志可启用 RSC。</p></td>
</tr>
</tbody>
</table>

 

在微型端口驱动程序处理[oid 后\_TCP\_卸载\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters)OID 请求，它必须为[**NDIS\_状态\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-task-offload-current-config)\_\_更新的卸载状态。

当微型端口驱动程序接收[OID 时\_TCP\_卸载\_当前\_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config) OID 请求，在该请求中， **NDIS\_卸载\_** 在，驱动程序必须在完成 OID 请求之前，指示堆栈上的任何现有接合段。

 

 





