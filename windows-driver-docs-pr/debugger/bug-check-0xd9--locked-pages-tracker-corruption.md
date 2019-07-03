---
title: Bug 检查 0xD9 LOCKED_PAGES_TRACKER_CORRUPTION
description: LOCKED_PAGES_TRACKER_CORRUPTION bug 检查具有 0x000000D9 值。 这表示已损坏的内部锁定页跟踪结构。
ms.assetid: 81011ce6-159c-448f-9f68-7b1eb949ff68
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
ms.openlocfilehash: dc24da4c44399f1e548c6ee2412ed0344b3954d3
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67518850"
---
# <a name="bug-check-0xd9-lockedpagestrackercorruption"></a>Bug 检查 0xD9：锁定\_PAGES\_跟踪器\_损坏


LOCKED\_PAGES\_跟踪器\_损坏错误检查的值为 0x000000D9。 这表示已损坏的内部锁定页跟踪结构。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。


## <a name="lockedpagestrackercorruption-parameters"></a>锁定\_PAGES\_跟踪器\_损坏参数


参数 1 指示冲突的类型。 其他参数的含义取决于参数 1 的值。

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
<td align="left"><p>跟踪结构内部锁的地址</p></td>
<td align="left"><p>内存描述符列表的地址</p></td>
<td align="left"><p>为当前进程锁定了页面数</p></td>
<td align="left"><p>两次上相同的进程列表插入了 MDL。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x02</p></td>
<td align="left"><p>跟踪结构内部锁的地址</p></td>
<td align="left"><p>内存描述符列表的地址</p></td>
<td align="left"><p>为当前进程锁定了页面数</p></td>
<td align="left"><p>在整个系统列表中两次插入 MDL。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x03</p></td>
<td align="left"><p>找到的第一个内部跟踪结构的地址</p></td>
<td align="left"><p>跟踪结构内部锁的地址</p></td>
<td align="left"><p>内存描述符列表的地址</p></td>
<td align="left"><p>正在释放时，MDL 找进程列表中两次。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x04</p></td>
<td align="left"><p>跟踪结构内部锁的地址</p></td>
<td align="left"><p>内存描述符列表的地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>MDL 上未找到系统范围列表中可用后已将其删除。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

参数 1 的值指示错误。

 

 




