---
title: Bug 检查 0x76 PROCESS_HAS_LOCKED_PAGES
description: PROCESS_HAS_LOCKED_PAGES bug 检查具有 0x00000076 值。 此 bug 检查指示驱动程序无法在 I/O 操作后释放锁定的页。
ms.assetid: 25c63e2e-6d2a-401a-b523-ffa70e9f75df
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
ms.openlocfilehash: 504dc2d81b4247a535c576c08bf7a3590ede1343
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367332"
---
# <a name="bug-check-0x76-processhaslockedpages"></a>Bug 检查 0x76：进程\_HAS\_已锁定\_页


进程\_HAS\_已锁定\_页错误检查的值为 0x00000076。 此 bug 检查指示驱动程序无法在 I/O 操作后释放锁定的页或它试图解锁页已经解锁。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="processhaslockedpages-parameters"></a>进程\_HAS\_已锁定\_页参数


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
<td align="left"><p>0x00</p></td>
<td align="left"><p>进程对象的指针</p></td>
<td align="left"><p>锁定的页的数目</p></td>
<td align="left"><p>指向驱动程序堆栈 （如果启用） 的指针。 否则，此参数为零。</p></td>
<td align="left"><p>正在终止进程已锁定内存页。 该驱动程序必须解锁它可能已锁定过程中，在进程终止之前的任何内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x01</p></td>
<td align="left"><p>MDL 驱动程序指定</p></td>
<td align="left"><p>在该进程中的锁定的内存页的数目</p></td>
<td align="left"><p>一个指向该进程 （如果启用） 的驱动程序堆栈。 否则，此参数为零。</p></td>
<td align="left"><p>该驱动程序尝试解锁未锁定的进程内存页。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

驱动程序或者未能解锁其锁定的页 （参数 1 值为 0x0），或者驱动程序正在尝试解锁的页面尚未锁定或都已解锁 （参数 1 值为 0x1）。

<a name="resolution"></a>分辨率
----------

[ **！ 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)调试扩展显示有关错误检查的信息，有助于在确定根本原因。

**如果参数 1 值为 0x0**

首先，使用[ **！ 搜索**](-search.md)在所有物理内存的当前进程指针上的扩展。 此扩展可能会发现至少一个内存描述符列表 (MDL) 指向当前进程。 接下来，使用 **！ 搜索**上查找以获取指向当前进程的 I/O 请求数据包 (IRP) 每个 MDL。 从此 IRP，可以标识哪些驱动程序正在泄漏页。

否则，可以检测哪些驱动程序引起的错误编辑注册表：

1.  在中 **\\ \\HKEY\_本地\_机\\系统\\CurrentControlSet\\控制\\会话管理器\\内存管理**注册表项，创建或编辑**TrackLockedPages**值，并将其设置为 dword 值 1。

2.  重新启动计算机。

系统则将保存的堆栈跟踪，因此可以轻松地识别出导致问题的驱动程序。 如果驱动程序会再次导致相同的错误[ **bug 检查 0xCB** ](bug-check-0xcb--driver-left-locked-pages-in-process.md) (驱动程序\_左侧\_已锁定\_页\_IN\_进程) 发出并显示在蓝色屏幕上并存储在内存中的位置会导致此错误的驱动程序的名称 (PUNICODE\_字符串) **KiBugCheckDriver**。

**如果参数 1 值为 0x1**

检查驱动程序源代码，进行锁定和解锁内存，并尝试找到内存的第一个操作数不被解除锁定实例锁定。

 

 




