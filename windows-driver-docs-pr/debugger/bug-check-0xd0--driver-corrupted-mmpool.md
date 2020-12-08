---
title: Bug 检查 0xD0 DRIVER_CORRUPTED_MMPOOL
description: DRIVER_CORRUPTED_MMPOOL bug 检查的值为0x000000D0。 这表示系统尝试在进程 IRQL 上访问无效内存，但该进程的 IRQL 太高。
keywords:
- Bug 检查 0xD0 DRIVER_CORRUPTED_MMPOOL
- DRIVER_CORRUPTED_MMPOOL
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_CORRUPTED_MMPOOL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9d1cbd56f12d49bb3cb9db136aa4eff44a01a5e8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825193"
---
# <a name="bug-check-0xd0-driver_corrupted_mmpool"></a>Bug 检查0xD0：驱动程序 \_ 损坏 \_ MMPOOL


驱动程序 \_ 损坏的 \_ MMPOOL bug 检查的值为0x000000D0。 这表示系统尝试在进程 IRQL 上访问无效内存，但该进程的 IRQL 太高。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="driver_corrupted_mmpool-parameters"></a>驱动程序 \_ 损坏的 \_ MMPOOL 参数


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
<td align="left"><p>引用时为 IRQL</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p><strong>0：</strong> 读取</p>
<p><strong>1：</strong> 写入</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>对引用的内存进行寻址</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

当 IRQL 太大时，内核试图访问可分页内存 (或可能是完全无效的内存) 。 此问题的最终原因几乎肯定是损坏了系统池的驱动程序。

在大多数情况下，如果驱动程序损坏大的分配 (页面 \_ 大小或更大) ，则会产生此 bug 检查结果。 较小的分配导致 [**bug 检查 0xC5**](bug-check-0xc5--driver-corrupted-expool.md) (驱动程序 \_ 损坏 \_ EXPOOL) 。

<a name="resolution"></a>解决方法
----------

如果最近安装了任何新软件，请检查是否已正确安装。 查看制造商网站上的已更新驱动程序。

若要调试此错误，请使用驱动程序验证程序的特殊池选项。 如果这无法显示导致错误的驱动程序，请使用全局标志实用工具启用 "按池的特殊池" 标记。

有关特殊池的信息，请参阅 Windows 驱动程序工具包的驱动程序验证程序部分。

另一种方法是打开 **\\ \\ HKEY \_ 本地 \_ 计算机 \\ 系统 \\ CurrentControlSet \\ 控制 \\ 会话管理器 \\ 内存管理** 注册表项。 在此注册表项中，创建或编辑 **ProtectNonPagedPool** 值，并将其设置为等于 DWORD 1。 然后重新启动。 然后，系统将取消所有已释放的非分页池的映射。 这会阻止驱动程序损坏池。 不过 (这不会保护来自 DMA 硬件的池。 ) 

 

 




