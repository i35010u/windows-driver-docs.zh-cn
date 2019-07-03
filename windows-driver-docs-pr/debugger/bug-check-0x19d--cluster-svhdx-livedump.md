---
title: Bug 检查 0x19D CLUSTER_SVHDX_LIVEDUMP
description: CLUSTER_SVHDX_LIVEDUMP bug 检查具有 0x0000019D 值。 这指示 SVHDX 启动此 livedump 来帮助调试不一致的状态。
ms.assetid: E261617D-E84A-4644-8854-53A189395637
keywords:
- Bug 检查 0x19D CLUSTER_SVHDX_LIVEDUMP
- CLUSTER_SVHDX_LIVEDUMP
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CLUSTER_SVHDX_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8a50dfb7ca3451e934edad2290127d382a637e1f
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519781"
---
# <a name="bug-check-0x19d-clustersvhdxlivedump"></a>Bug 检查 0x19D：CLUSTER\_SVHDX\_LIVEDUMP


群集\_SVHDX\_LIVEDUMP bug 检查的值为 0x0000019D。 这指示 SVHDX 启动此 livedump 来帮助调试不一致的状态。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。


## <a name="clustersvhdxlivedump-parameters"></a>群集\_SVHDX\_LIVEDUMP 参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">1</td>
<td align="left"><p>原因代码</p>
<p>0x1:装载的共享虚拟磁盘发生故障</p>
2-地址 Svhdxflt ！ _SVHDX_VIRTUALDISK_CONTEXT 3-nt 地址 ！ _FILE_OBJECT 4-NTSTATUS</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">请参阅参数 1</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">请参阅参数 1</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">请参阅参数 1</td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

当 SVHDX 检测到当前状态可能会导致某种形式的不一致时它将生成具有此状态代码的实时转储。 Parameter1 具有代码指向此实时转储哪些方案创建的。 其他参数应解释的原因代码的上下文中。

 

 




