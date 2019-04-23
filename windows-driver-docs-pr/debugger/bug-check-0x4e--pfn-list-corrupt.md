---
title: Bug 检查 0x4E PFN_LIST_CORRUPT
description: PFN_LIST_CORRUPT bug 检查具有 0x0000004E 值。 这表示页的帧数 (PFN) 列表已损坏。
ms.assetid: cf78aecb-80d3-4637-a2b5-a2511999c5e3
keywords:
- Bug 检查 0x4E PFN_LIST_CORRUPT
- PFN_LIST_CORRUPT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- PFN_LIST_CORRUPT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 44ebf74d7c9f495ebe035da08e01476c4c833f8e
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903459"
---
# <a name="bug-check-0x4e-pfnlistcorrupt"></a>Bug 检查 0x4E：PFN\_列表\_损坏


PFN\_列表\_损坏错误检查的值为 0x0000004E。 这表示页的帧数 (PFN) 列表已损坏。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="pfnlistcorrupt-parameters"></a>PFN\_列表\_损坏参数


*参数 1*指示冲突类型。 其他参数的含义取决于的值*参数 1*。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 1</th>
<th align="left">参数 2</th>
<th align="left">参数 3</th>
<th align="left">参数 4</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x01</p></td>
<td align="left"><p><strong>ListHead</strong>已损坏的值</p></td>
<td align="left"><p>可用的页面数</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>列表头已损坏。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x02</p></td>
<td align="left"><p>正在删除列表中的条目</p></td>
<td align="left"><p>最大的物理页面数</p></td>
<td align="left"><p>要删除的项的引用计数</p></td>
<td align="left"><p>列表项已损坏。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x07</p></td>
<td align="left"><p>页框架编号</p></td>
<td align="left"><p>当前共享计数</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>驱动程序已在不是它被锁定时解锁某一页更多次。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x8D</p></td>
<td align="left"><p>其状态不一致帧页码</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>页释放列表已损坏。 此错误代码最有可能表明硬件问题。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x8F</p></td>
<td align="left"><p>新页码</p></td>
<td align="left"><p>旧的页码</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>免费或清零页 listhead 已损坏。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x99</p></td>
<td align="left"><p>页框架编号</p></td>
<td align="left"><p>当前页状态</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>页表项 (PTE) 或 PFN 已损坏。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x9A</p></td>
<td align="left"><p>页框架编号</p></td>
<td align="left"><p>当前页状态</p></td>
<td align="left"><p>要移除的项的引用计数</p></td>
<td align="left"><p>驱动程序尝试以释放 IO 的仍为锁定状态的页。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

此错误通常是由传递错误内存描述符列表的驱动程序引起的。 例如，驱动程序可能具有名为**MmUnlockPages**两次用同样的列表。

如果可用的内核调试程序，请检查堆栈跟踪： [ **！ 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)调试扩展显示 bug 检查有关的信息并可有助于确定根本原因，然后输入之一[ **k （显示堆栈回溯）** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-)命令以查看调用堆栈。

 

 




