---
title: Bug 检查 0x10E VIDEO_MEMORY_MANAGEMENT_INTERNAL
description: VIDEO_MEMORY_MANAGEMENT_INTERNAL bug 检查具有 0x0000010E 值。 这指示视频内存管理器遇到它不能从恢复的条件。
ms.assetid: 2fb29098-084c-462a-bb06-789e73924d16
keywords:
- Bug 检查 0x10E VIDEO_MEMORY_MANAGEMENT_INTERNAL
- VIDEO_MEMORY_MANAGEMENT_INTERNAL
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- VIDEO_MEMORY_MANAGEMENT_INTERNAL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 97a048d99b5a4a6ceb5d33184773f6b432237865
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239824"
---
# <a name="bug-check-0x10e-videomemorymanagementinternal"></a>Bug 检查 0x10E：视频\_内存\_管理\_内部


视频\_内存\_管理\_内部 bug 检查的值为 0x0000010E。 这指示视频内存管理器遇到它不能从恢复的条件。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="videomemorymanagementinternal-parameters"></a>视频\_内存\_管理\_内部参数


参数 1 是感兴趣; 的唯一参数此列标识了确切的冲突。 必须逐个检查不会显示此表中的参数 1 的值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 1</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>尝试旋转非轮换的范围。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>尝试销毁非空进程堆。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3</p></td>
<td align="left"><p>尝试从 aperture 段取消映射失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x4</p></td>
<td align="left"><p>在旋转必须成功路径失败。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x5</p></td>
<td align="left"><p>延迟的命令失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x6</p></td>
<td align="left"><p>尝试重新分配就必须取消其逐出的分配的资源。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x7</p></td>
<td align="left"><p>无效尝试延迟免费使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x8</p></td>
<td align="left"><p>拆分直接内存访问 (DMA) 缓冲区包含无效的引用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x9</p></td>
<td align="left"><p>尝试逐出分配失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xA</p></td>
<td align="left"><p>无效地尝试使用已固定的分配时进行。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xB</p></td>
<td align="left"><p>驱动程序返回从无效的错误代码<em>BuildPagingBuffer</em>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xC</p></td>
<td align="left"><p>段中检测到资源泄漏。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xD</p></td>
<td align="left"><p>正在未正确使用一个段。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xE</p></td>
<td align="left"><p>尝试将映射到 aperture 段分配失败。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xF</p></td>
<td align="left"><p>驱动程序返回从无效的错误代码<em>AcquireSwizzlingRange</em>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10</p></td>
<td align="left"><p>驱动程序返回从无效的错误代码<em>ReleaseSwizzlingRange</em>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x11</p></td>
<td align="left"><p>已尝试使用 aperture 段无效。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x12</p></td>
<td align="left"><p>驱动程序时提供的 DMA 缓冲区溢出。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x13</p></td>
<td align="left"><p>驱动程序时提供的专用数据缓冲区溢出。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x14</p></td>
<td align="left"><p>尝试清除所有段失败。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x15</p></td>
<td align="left"><p>尝试释放仍处于旋转状态的虚拟地址说明符 (VAD)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x16</p></td>
<td align="left"><p>驱动程序中断的有保证的 DMA 缓冲区模型约定。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x17</p></td>
<td align="left"><p>发生了意外的系统命令故障。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x18</p></td>
<td align="left"><p>尝试发布已固定的分配的资源失败。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x19</p></td>
<td align="left"><p>驱动程序修补 DMA 缓冲区失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1A</p></td>
<td align="left"><p>已释放共享分配的所有者。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1B</p></td>
<td align="left"><p>尝试释放仍在使用 aperture 范围。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x25</p></td>
<td align="left"><p>GPU 试图在未定义的 aperture 区域上重写。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

检查此错误通常是由视频驱动程序行为不正确引起的。

<a name="resolution"></a>分辨率
----------

如果问题仍然存在，请检查 Windows 更新以获取更新的视频驱动程序。

 

 




