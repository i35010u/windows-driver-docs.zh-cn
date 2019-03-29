---
title: Bug 检查 0x39 SYSTEM_EXIT_OWNED_MUTEX
description: SYSTEM_EXIT_OWNED_MUTEX bug 检查具有 0x00000039 值。 这指示辅助例程返回而不释放它拥有的互斥体对象。
ms.assetid: 79257486-f65e-4d02-acf0-b7f0607a21cc
keywords:
- Bug 检查 0x39 SYSTEM_EXIT_OWNED_MUTEX
- SYSTEM_EXIT_OWNED_MUTEX
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- SYSTEM_EXIT_OWNED_MUTEX
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4890cfe1cf28c4ba9700ed0fe8e15706af6198a2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577179"
---
# <a name="bug-check-0x39-systemexitownedmutex"></a>Bug 检查 0x39：系统\_退出\_拥有的\_互斥体


系统\_退出\_拥有的\_互斥体 bug 检查的值为 0x00000039。 这指示辅助例程返回而不释放它拥有的互斥体对象。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="systemexitownedmutex-parameters"></a>系统\_退出\_拥有的\_互斥体参数


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
<td align="left"><p>1</p></td>
<td align="left"><p>导致错误的辅助角色例程的地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>传递给辅助角色例程的参数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>工作项的地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>保留。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

辅助角色例程返回时它仍拥有的 mutex 对象。 当前的工作线程将继续运行其他不相关的工作项，并将永远不会释放互斥体。

<a name="resolution"></a>分辨率
----------

调试器需要分析此问题。 若要查找驱动程序导致了错误，请使用**ln** （列表最接近符号） 调试器命令：

kd&gt; ln 地址

其中，地址是在参数 1 中给定的辅助角色例程。

 

 




