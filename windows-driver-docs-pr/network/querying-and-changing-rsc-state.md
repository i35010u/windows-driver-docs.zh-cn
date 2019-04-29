---
title: 查询和更改 RSC 状态
description: 本部分介绍如何查询或更改当前接收段合并 (RSC) 的支持 RSC 的微型端口驱动程序的状态。
ms.assetid: 5455FBB2-3603-44EF-B1C6-494D31DD820D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e2757cf1740bcd118e679d4fffa04394930f319
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360961"
---
# <a name="querying-and-changing-rsc-state"></a>查询和更改 RSC 状态


本部分介绍如何查询或更改当前接收段合并 (RSC) 的支持 RSC 的微型端口驱动程序的状态。

## <a name="querying-rsc-state"></a>查询 RSC 状态


可以通过发出查询的当前 RSC 状态[OID\_TCP\_卸载\_当前\_CONFIG](https://msdn.microsoft.com/library/windows/hardware/ff569805) OID 请求。 NDIS 处理此 OID 并不将它传递到微型端口。

## <a name="changing-rsc-state"></a>更改 RSC 状态


可以启用或禁用通过发出 RSC [OID\_TCP\_卸载\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569807)OID 请求。 使用此 OID [ **NDIS\_卸载\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff566706)结构。 在此结构中， **RscIPv4**并**RscIPv6**成员都可以具有以下值：

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

 

微型端口驱动程序进程后[OID\_TCP\_卸载\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569807)OID 请求，它必须为提供[ **NDIS\_状态\_任务\_卸载\_当前\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff567424)使用更新的状态指示卸载状态。

当微型端口驱动程序收到[OID\_TCP\_卸载\_当前\_CONFIG](https://msdn.microsoft.com/library/windows/hardware/ff569805) OID 请求在其中**NDIS\_卸载\_参数\_RSC\_禁用**指定标志，该驱动程序必须指示完成 OID 请求之前存在的任何合并在堆栈中向上的段。

 

 





