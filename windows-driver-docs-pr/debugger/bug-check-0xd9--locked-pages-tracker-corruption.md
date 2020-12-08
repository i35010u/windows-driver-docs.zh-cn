---
title: Bug 检查 0xD9 LOCKED_PAGES_TRACKER_CORRUPTION
description: LOCKED_PAGES_TRACKER_CORRUPTION bug 检查的值为0x000000D9。 这表示内部锁定页面跟踪结构已损坏。
keywords:
- Bug 检查 0xD9 LOCKED_PAGES_TRACKER_CORRUPTION
- LOCKED_PAGES_TRACKER_CORRUPTION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- LOCKED_PAGES_TRACKER_CORRUPTION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 36bd21a3fbb6a39ae1804c950eda955e87a30667
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787853"
---
# <a name="bug-check-0xd9-locked_pages_tracker_corruption"></a>Bug 检查0xD9：锁定 \_ 页面 \_ 跟踪器 \_ 损坏


锁定 \_ 页面 \_ 跟踪器 \_ 损坏 bug 检查的值为0x000000D9。 这表示内部锁定页面跟踪结构已损坏。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="locked_pages_tracker_corruption-parameters"></a>锁定 \_ 页面 \_ 跟踪器 \_ 损坏参数


参数1指示违规类型。 其他参数的意义取决于参数1的值。

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
<th align="left">参数2</th>
<th align="left">参数3</th>
<th align="left">参数4</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x01</p></td>
<td align="left"><p>内部锁跟踪结构的地址</p></td>
<td align="left"><p>内存描述符列表的地址</p></td>
<td align="left"><p>为当前进程锁定的页数</p></td>
<td align="left"><p>MDL 正在同一进程列表中插入两次。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x02</p></td>
<td align="left"><p>内部锁跟踪结构的地址</p></td>
<td align="left"><p>内存描述符列表的地址</p></td>
<td align="left"><p>为当前进程锁定的页数</p></td>
<td align="left"><p>在系统范围列表上，MDL 插入了两次。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x03</p></td>
<td align="left"><p>找到的第一个内部跟踪结构的地址</p></td>
<td align="left"><p>内部锁跟踪结构的地址</p></td>
<td align="left"><p>内存描述符列表的地址</p></td>
<td align="left"><p>释放 MDL 后，在进程列表中找到了两次。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x04</p></td>
<td align="left"><p>内部锁跟踪结构的地址</p></td>
<td align="left"><p>内存描述符列表的地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>删除 MDL 后，在该系统范围列表中找到该 MDL。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

错误由参数1的值指示。

 

 




