---
title: 查询和更改 RSC 状态
description: 本部分介绍如何查询或更改当前接收段合并 (RSC) 的支持 RSC 的微型端口驱动程序的状态。
ms.assetid: 5455FBB2-3603-44EF-B1C6-494D31DD820D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac1d26144e47ab596be373221c93ef3716bfba4c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385431"
---
# <a name="querying-and-changing-rsc-state"></a>查询和更改 RSC 状态


本部分介绍如何查询或更改当前接收段合并 (RSC) 的支持 RSC 的微型端口驱动程序的状态。

## <a name="querying-rsc-state"></a>查询 RSC 状态


可以通过发出查询的当前 RSC 状态[OID\_TCP\_卸载\_当前\_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config) OID 请求。 NDIS 处理此 OID 并不将它传递到微型端口。

## <a name="changing-rsc-state"></a>更改 RSC 状态


可以启用或禁用通过发出 RSC [OID\_TCP\_卸载\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters)OID 请求。 使用此 OID [ **NDIS\_卸载\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload_parameters)结构。 在此结构中， **RscIPv4**并**RscIPv6**成员都可以具有以下值：

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
<td align="left"><p>指定此标志，以禁用 RSC。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>NDIS_OFFLOAD_PARAMETERS_RSC_ENABLED</strong></p></td>
<td align="left"><p>指定此标志可启用 RSC。</p></td>
</tr>
</tbody>
</table>

 

微型端口驱动程序进程后[OID\_TCP\_卸载\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters)OID 请求，它必须为提供[ **NDIS\_状态\_任务\_卸载\_当前\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-task-offload-current-config)使用更新的状态指示卸载状态。

当微型端口驱动程序收到[OID\_TCP\_卸载\_当前\_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config) OID 请求在其中**NDIS\_卸载\_参数\_RSC\_禁用**指定标志，该驱动程序必须指示完成 OID 请求之前存在的任何合并在堆栈中向上的段。

 

 





