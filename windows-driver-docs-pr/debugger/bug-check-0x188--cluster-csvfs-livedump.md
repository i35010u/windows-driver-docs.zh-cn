---
title: Bug 检查 0x188 CLUSTER_CSVFS_LIVEDUMP
description: CLUSTER_CSVFS_LIVEDUMP bug 检查的值为0x00000188。 这表明 CSVFS 启动了此 livedump 来帮助调试不一致的状态。
keywords:
- Bug 检查 0x188 CLUSTER_CSVFS_LIVEDUMP
- CLUSTER_CSVFS_LIVEDUMP
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CLUSTER_CSVFS_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 124b159e8fe5da016c072dca8b742db9794f2ca9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840465"
---
# <a name="bug-check-0x188-cluster_csvfs_livedump"></a>Bug 检查0x188：群集 \_ CSVFS \_ LIVEDUMP


群集 \_ CSVFS \_ LIVEDUMP bug 检查的值为0x00000188。 这表明 CSVFS 启动了此 livedump 来帮助调试不一致的状态。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="cluster_csvfs_livedump-parameters"></a>群集 \_ CSVFS \_ LIVEDUMP 参数


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
0x1：对 oplock 降级到无的缓存清除操作失败
<p>2-CSVFS！ _SCB</p>
0x2：对不是的 oplock 升级的缓存清除操作失败
<p>2-CSVFS！ _SCB</p>
0x3：在设置清除失败模式时清除缓存
<p>2-CSVFS！ _SCB</p>
0x4： oplock 降级到无失败的缓存刷新
<p>2-CSVFS！ _SCB</p></td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">请参阅参数1</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">预留</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">预留</td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

第一个参数包含以下原因： CSVFS 检测到当前状态可能导致数据损坏或其他种类的不一致时，它将生成具有此状态代码的实时转储。 Parameter1 具有指向为其创建此实时转储的方案的代码。 应在原因代码的上下文中解释其他参数。

 

 




