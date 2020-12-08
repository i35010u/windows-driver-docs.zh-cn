---
title: Bug 检查 0x19D CLUSTER_SVHDX_LIVEDUMP
description: CLUSTER_SVHDX_LIVEDUMP bug 检查的值为0x0000019D。 这表示 SVHDX 启动了此 livedump 以帮助调试不一致的状态。
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
ms.openlocfilehash: 4c024e818b34aff6a02f9d1f888f295710c62fc7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819279"
---
# <a name="bug-check-0x19d-cluster_svhdx_livedump"></a>Bug 检查0x19D： CLUSTER \_ SVHDX \_ LIVEDUMP


CLUSTER \_ SVHDX \_ LIVEDUMP bug 检查的值为0x0000019D。 这表示 SVHDX 启动了此 livedump 以帮助调试不一致的状态。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="cluster_svhdx_livedump-parameters"></a>CLUSTER \_ SVHDX \_ LIVEDUMP 参数


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
<p>0x1：装载共享虚拟磁盘失败</p>
2-Svhdxflt！ _SVHDX_VIRTUALDISK_CONTEXT 3-nt 的地址！ _FILE_OBJECT 4-NTSTATUS</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">请参阅参数1</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">请参阅参数1</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">请参阅参数1</td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

当 SVHDX 检测到当前状态可能会导致某种类型的不一致时，它将生成具有此状态代码的实时转储。 Parameter1 具有指向为其创建此实时转储的方案的代码。 应在原因代码的上下文中解释其他参数。

 

 




