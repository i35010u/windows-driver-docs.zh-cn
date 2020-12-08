---
title: Bug 检查 0xC1 SPECIAL_POOL_DETECTED_MEMORY_CORRUPTION
description: SPECIAL_POOL_DETECTED_MEMORY_CORRUPTION bug 检查的值为0x000000C1。 这表明驱动程序已写入特殊池的无效部分。
keywords:
- Bug 检查 0xC1 SPECIAL_POOL_DETECTED_MEMORY_CORRUPTION
- SPECIAL_POOL_DETECTED_MEMORY_CORRUPTION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- SPECIAL_POOL_DETECTED_MEMORY_CORRUPTION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 62b0a3fbf9ae456eff0b9ac4e02c4ec2e867da11
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833703"
---
# <a name="bug-check-0xc1-special_pool_detected_memory_corruption"></a>Bug 检查0xC1：特殊 \_ 池 \_ 检测到 \_ 内存 \_ 损坏


特殊 \_ 池 \_ 检测到 \_ \_ 的内存损坏 bug 检查的值为0x000000C1。 这表明驱动程序已写入特殊池的无效部分。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="special_pool_detected_memory_corruption-parameters"></a>特殊 \_ 池 \_ 检测到的 \_ 内存 \_ 损坏参数


参数4指示冲突类型。

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
<td align="left"><p>驱动程序尝试释放的地址</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0x20</p></td>
<td align="left"><p>驱动程序尝试释放未分配的池。</p></td>
</tr>
<tr class="even">
<td align="left"><p>驱动程序尝试释放的地址</p></td>
<td align="left"><p>请求的字节数</p></td>
<td align="left"><p>计算得出的字节 (实际提供给调用方) </p></td>
<td align="left"><p>0x21,</p>
<p>0x22</p></td>
<td align="left"><p>驱动程序尝试释放错误的地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>驱动程序尝试释放的地址</p></td>
<td align="left"><p>Bits 损坏的地址</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>0x23</p></td>
<td align="left"><p>驱动程序释放了一个地址，但同一页中的邻近字节已损坏。</p></td>
</tr>
<tr class="even">
<td align="left"><p>驱动程序尝试释放的地址</p></td>
<td align="left"><p>Bits 损坏的地址</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>0x24</p></td>
<td align="left"><p>驱动程序释放了一个地址，但在分配结束后出现的字节被覆盖。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>当前 IRQL</p></td>
<td align="left"><p>池类型</p></td>
<td align="left"><p>字节数</p></td>
<td align="left"><p>0x30</p></td>
<td align="left"><p>驱动程序尝试以错误的 IRQL 分配池。</p></td>
</tr>
<tr class="even">
<td align="left"><p>当前 IRQL</p></td>
<td align="left"><p>池类型</p></td>
<td align="left"><p>驱动程序尝试释放的地址</p></td>
<td align="left"><p>0x31</p></td>
<td align="left"><p>驱动程序尝试使用不正确的 IRQL 释放池。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>驱动程序尝试释放的地址</p></td>
<td align="left"><p>一个位已损坏的地址</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>0x32</p></td>
<td align="left"><p>驱动程序释放了一个地址，但同一页中的邻近字节有一个位错误。</p></td>
</tr>
</tbody>
</table>

 

\_池 \_ 类型代码在 ntddk 中进行枚举。 具体而言，0表示非分页池，另一种表示页面缓冲池。

<a name="cause"></a>原因
-----

驱动程序已写入特殊池的无效部分。

<a name="resolution"></a>解决方法
----------

获取当前线程的 backtrace。 此 backtrace 通常会显示错误源。

有关特殊池的信息，请参阅 Windows 驱动程序工具包的驱动程序验证程序部分。

 

 




