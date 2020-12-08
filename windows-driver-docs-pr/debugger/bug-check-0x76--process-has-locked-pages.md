---
title: Bug 检查 0x76 PROCESS_HAS_LOCKED_PAGES
description: PROCESS_HAS_LOCKED_PAGES bug 检查的值为0x00000076。 此 bug 检查表明驱动程序无法在 i/o 操作后释放锁定页。
keywords:
- Bug 检查 0x76 PROCESS_HAS_LOCKED_PAGES
- PROCESS_HAS_LOCKED_PAGES
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- PROCESS_HAS_LOCKED_PAGES
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7d7a0b402c14f6b71367284f0c2eb6e6a5de3330
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787015"
---
# <a name="bug-check-0x76-process_has_locked_pages"></a>Bug 检查0x76：进程 \_ 已 \_ 锁定 \_ 页面


该进程 \_ 已 \_ 锁定 \_ 页面 bug 检查的值为0x00000076。 此 bug 检查表明驱动程序在执行 i/o 操作后未能释放锁定的页，或者它尝试解除锁定已解锁的页。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="process_has_locked_pages-parameters"></a>进程 \_ 已 \_ 锁定 \_ PAGES 参数


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
<td align="left"><p>0x00</p></td>
<td align="left"><p>指向进程对象的指针</p></td>
<td align="left"><p>锁定页面的数目</p></td>
<td align="left"><p>如果启用) ，则指向驱动程序堆栈 (的指针。 否则，此参数为零。</p></td>
<td align="left"><p>终止的进程具有锁定的内存页。 在进程终止之前，驱动程序必须解除它可能已在进程中锁定的任何内存的锁定。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x01</p></td>
<td align="left"><p>驱动程序指定的 MDL</p></td>
<td align="left"><p>该进程中当前锁定的内存页数</p></td>
<td align="left"><p>指向该进程的驱动程序堆栈的指针 (如果启用) ，则为。 否则，此参数为零。</p></td>
<td align="left"><p>驱动程序正在尝试解锁未锁定的进程内存页。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

驱动程序无法解除锁定锁定的页面 (参数1值为 0x0) ，或驱动程序正在尝试解锁尚未锁定的页面或已解锁的页面 (参数1值为 0x1) 。

<a name="resolution"></a>解决方法
----------

[**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。

**如果参数1的值为0x0**

首先在所有物理内存中的当前进程指针上使用 [**！搜索**](-search.md) 扩展。 此扩展可能会找到指向当前进程 (MDL) 的至少一个内存描述符列表。 接下来，使用 **！搜索** 你发现的每个 MDL，以获取指向当前进程 (IRP) 的 i/o 请求包。 您可以通过此 IRP 识别哪个驱动程序正在泄漏页面。

否则，可以通过编辑注册表来检测导致错误的驱动程序：

1.  在 **\\ \\ HKEY \_ 本地 \_ 计算机 \\ 系统 \\ CurrentControlSet \\ 控制 \\ 会话管理器 \\ 内存管理** 注册表项中，创建或编辑 **TrackLockedPages** 值，然后将其设置为等于 DWORD 1。

2.  重新启动计算机。

系统随后会保存堆栈跟踪，因此你可以轻松地识别导致问题的驱动程序。 如果驱动程序再次导致相同的错误，则会发出 [**bug 检查 0xCB**](bug-check-0xcb--driver-left-locked-pages-in-process.md) (驱动程序 \_ \_ \_ \_ \_ 已发出) 的进程中的已锁定页面，并且导致此错误的驱动程序的名称将显示在蓝色屏幕上，并存储在内存中的 PUNICODE \_) **KiBugCheckDriver** 位置 (位置。

**如果参数1的值为0x1**

检查用于锁定和解锁内存的驱动程序源代码，并尝试查找内存未锁定的实例，而无需先进行锁定。

 

 




