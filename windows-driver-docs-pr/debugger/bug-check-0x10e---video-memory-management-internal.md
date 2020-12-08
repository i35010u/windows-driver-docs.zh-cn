---
title: Bug 检查 0x10E VIDEO_MEMORY_MANAGEMENT_INTERNAL
description: VIDEO_MEMORY_MANAGEMENT_INTERNAL bug 检查的值为0x0000010E。 这表明视频内存管理器遇到了无法恢复的情况。
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
ms.openlocfilehash: 238a0df92603339b5236ea5e6e7d8cd0c4922292
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790065"
---
# <a name="bug-check-0x10e-video_memory_management_internal"></a>Bug 检查0x10E： \_ 内部视频内存 \_ 管理 \_


视频 \_ 内存 \_ 管理 \_ 内部错误检查的值为0x0000010E。 这表明视频内存管理器遇到了无法恢复的情况。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="video_memory_management_internal-parameters"></a>视频 \_ 内存 \_ 管理 \_ 内部参数


参数1是感兴趣的唯一参数;这会确定具体的冲突。 必须单独检查此表中未出现的参数1的值。

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
<td align="left"><p>尝试旋转非旋转范围。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>尝试销毁非空进程堆。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3</p></td>
<td align="left"><p>尝试从光圈段取消映射失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x4</p></td>
<td align="left"><p>必须成功的路径中的轮换失败。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x5</p></td>
<td align="left"><p>延迟的命令失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x6</p></td>
<td align="left"><p>尝试为已取消逐出的分配重新分配资源。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x7</p></td>
<td align="left"><p>尝试使用无效的来延迟可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x8</p></td>
<td align="left"><p> (DMA) 缓冲区的拆分直接内存访问包含无效的引用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x9</p></td>
<td align="left"><p>尝试逐出分配失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xA</p></td>
<td align="left"><p>使用固定分配的尝试无效。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xB</p></td>
<td align="left"><p>驱动程序从 <em>BuildPagingBuffer</em>返回了无效的错误代码。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xC</p></td>
<td align="left"><p>在段中检测到资源泄漏。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xD</p></td>
<td align="left"><p>段的使用不正确。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xE</p></td>
<td align="left"><p>尝试将分配映射到孔径段失败。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xF</p></td>
<td align="left"><p>驱动程序从 <em>AcquireSwizzlingRange</em>返回了无效的错误代码。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10</p></td>
<td align="left"><p>驱动程序从 <em>ReleaseSwizzlingRange</em>返回了无效的错误代码。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x11</p></td>
<td align="left"><p>对使用口径段的尝试无效。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x12</p></td>
<td align="left"><p>驱动程序溢出了提供的 DMA 缓冲区。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x13</p></td>
<td align="left"><p>驱动程序溢出了提供的专用数据缓冲区。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x14</p></td>
<td align="left"><p>尝试清除所有段失败。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x15</p></td>
<td align="left"><p>尝试释放仍处于旋转状态的虚拟地址描述符 (VAD) </p></td>
</tr>
<tr class="even">
<td align="left"><p>0x16</p></td>
<td align="left"><p>驱动程序中断了保证的 DMA 缓冲区模型约定。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x17</p></td>
<td align="left"><p>出现意外的系统命令失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x18</p></td>
<td align="left"><p>尝试释放固定的分配的资源失败。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x19</p></td>
<td align="left"><p>驱动程序无法修补 DMA 缓冲区。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1A</p></td>
<td align="left"><p>共享分配的所有者已释放。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1B</p></td>
<td align="left"><p>尝试释放仍在使用中的口径范围。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x25</p></td>
<td align="left"><p>GPU 试图写入口径的未定义区域。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

此 bug 检查通常是由于视频驱动程序的行为不正确引起的。

<a name="resolution"></a>解决方法
----------

如果问题仍然存在，请查看更新的视频驱动程序 Windows 更新。

 

 




