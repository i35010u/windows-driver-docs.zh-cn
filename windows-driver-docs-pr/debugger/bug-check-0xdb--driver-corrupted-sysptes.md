---
title: Bug 检查 0xDB DRIVER_CORRUPTED_SYSPTES
description: DRIVER_CORRUPTED_SYSPTES bug 检查的值为0x000000DB。 这表明尝试触摸内存时出现无效的 IRQL，原因可能是系统 Pte 损坏。
keywords:
- Bug 检查 0xDB DRIVER_CORRUPTED_SYSPTES
- DRIVER_CORRUPTED_SYSPTES
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_CORRUPTED_SYSPTES
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cc3f9c464fb8080a7c4208087afcda4c2acb5b5a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787845"
---
# <a name="bug-check-0xdb-driver_corrupted_sysptes"></a>Bug 检查0xDB：驱动程序 \_ 损坏 \_ SYSPTES


驱动程序 \_ 损坏的 \_ SYSPTES bug 检查的值为0x000000DB。 这表明尝试触摸内存时出现无效的 IRQL，原因可能是系统 Pte 损坏。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="driver_corrupted_sysptes-parameters"></a>驱动程序 \_ 损坏的 \_ SYSPTES 参数


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
<td align="left"><p>引用的内存</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>IRQL</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p><strong>0：</strong> 读取</p>
<p><strong>1：</strong> 写入</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>引用内存的代码中的地址</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

驱动程序尝试访问分页 (或完全无效的) 内存。 此 bug 检查几乎总是由系统 Pte 损坏的驱动程序引起的。

<a name="resolution"></a>解决方法
----------

如果发生此错误检查，则可以通过编辑注册表来检测问题。 在 **\\ \\ HKEY \_ 本地 \_ 计算机 \\ 系统 \\ CurrentControlSet \\ 控制 \\ 会话管理器 \\ 内存管理** 注册表项中，创建或编辑 **TrackPtes** 值，并将其设置为等于 DWORD 3。 然后重新启动。 系统随后会保存堆栈跟踪，如果驱动程序提交相同的错误，系统将发出 [**bug 检查 0xDA**](bug-check-0xda--system-pte-misuse.md) (系统 \_ PTE \_ 滥用) 。 然后，堆栈跟踪将标识导致错误的驱动程序。

 

 




