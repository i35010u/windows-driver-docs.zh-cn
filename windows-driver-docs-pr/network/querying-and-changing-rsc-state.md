---
title: 查询和更改 RSC 状态
description: 本部分介绍如何查询或更改当前接收段合并， (RSC 功能的微型端口驱动程序的 RSC) 状态。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c43fe3c4d8da6094ff42e1f22d38ed68fc234b21
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820043"
---
# <a name="querying-and-changing-rsc-state"></a>查询和更改 RSC 状态


本部分介绍如何查询或更改当前接收段合并， (RSC 功能的微型端口驱动程序的 RSC) 状态。

## <a name="querying-rsc-state"></a>正在查询 RSC 状态


可以通过发出 [OID \_ TCP \_ 卸载 \_ 当前 \_ 配置](./oid-tcp-offload-current-config.md) OID 请求来查询当前 RSC 状态。 NDIS 处理此 OID，但不将其向下传递到小型端口。

## <a name="changing-rsc-state"></a>更改 RSC 状态


可以通过颁发 [oid \_ TCP \_ 卸载 \_ 参数](./oid-tcp-offload-parameters.md) OID 请求，启用或禁用 RSC。 此 OID 使用 [**NDIS \_ 卸载 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters) 结构。 在此结构中， **RscIPv4** 和 **RscIPv6** 成员可以具有以下值：

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

 

当微型端口驱动程序处理 [oid \_ TCP \_ 卸载 \_ 参数](./oid-tcp-offload-parameters.md) OID 请求后，它必须为 [**NDIS \_ 状态 \_ 任务 " \_ 卸载 \_ 当前 \_ 配置**](./ndis-status-task-offload-current-config.md) 状态指示" 提供更新的卸载状态。

当微型端口驱动程序收到 [oid \_ TCP \_ 卸载 \_ 当前的 \_ 配置](./oid-tcp-offload-current-config.md) OID 请求，其中指定了 **NDIS \_ 卸载 \_ 参数 \_ RSC \_ DISABLED** 标志时，驱动程序必须在完成 OID 请求之前，指出堆栈上的任何现有合并段。

 

