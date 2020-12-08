---
title: Bug 检查 0x39 SYSTEM_EXIT_OWNED_MUTEX
description: SYSTEM_EXIT_OWNED_MUTEX bug 检查的值为0x00000039。 这表明，辅助角色例程在不释放其拥有的 mutex 对象的情况下返回。
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
ms.openlocfilehash: 84961bcfddf4bdc41e4d175e2f46d528c21d8100
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822609"
---
# <a name="bug-check-0x39-system_exit_owned_mutex"></a>Bug 检查0x39：系统 \_ 退出 \_ 拥有的 \_ MUTEX


系统 \_ 出口 \_ 拥有 \_ 的互斥体 bug 检查的值为0x00000039。 这表明，辅助角色例程在不释放其拥有的 mutex 对象的情况下返回。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="system_exit_owned_mutex-parameters"></a>系统 \_ 出口 \_ 拥有的 \_ MUTEX 参数


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
<td align="left"><p>导致错误的辅助进程例程的地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>传递给辅助进程例程的参数。</p></td>
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

辅助例程在仍拥有 mutex 对象时返回。 当前工作线程将继续运行其他不相关的工作项，并且永远不会释放 mutex。

<a name="resolution"></a>解决方法
----------

需要调试器才能分析此问题。 若要查找导致错误的驱动程序，请使用 **ln** (列出最接近) 调试器命令的符号：

kd &gt; ln 地址

其中 address 是在参数1中给定的辅助角色。

 

 




