---
title: Bug 检查 0xC1 SPECIAL_POOL_DETECTED_MEMORY_CORRUPTION
description: SPECIAL_POOL_DETECTED_MEMORY_CORRUPTION bug 检查具有 0x000000C1 值。 这表示该驱动程序写入的特殊池无效的节。
ms.assetid: 4d5a3d95-de39-4e15-aba8-33257a6f0677
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
ms.openlocfilehash: dc881bf22b2fc0c22b3bc3c1f28ada984acbbfa0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564142"
---
# <a name="bug-check-0xc1-specialpooldetectedmemorycorruption"></a>Bug 检查 0xC1：特殊\_池\_已检测\_内存\_损坏


这两个特殊\_池\_已检测\_内存\_损坏错误检查的值为 0x000000C1。 这表示该驱动程序写入的特殊池无效的节。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="specialpooldetectedmemorycorruption-parameters"></a>特殊\_池\_已检测\_内存\_损坏参数


参数 4 指示冲突的类型。

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
<td align="left"><p>该驱动程序尝试免费的地址</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0x20</p></td>
<td align="left"><p>驱动程序尝试以释放未分配的池。</p></td>
</tr>
<tr class="even">
<td align="left"><p>该驱动程序尝试免费的地址</p></td>
<td align="left"><p>请求的字节数</p></td>
<td align="left"><p>Bytes 计算 （实际提供给调用方）</p></td>
<td align="left"><p>0x21,</p>
<p>0x22</p></td>
<td align="left"><p>驱动程序尝试以释放地址不正确。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>该驱动程序尝试免费的地址</p></td>
<td align="left"><p>Bits 已损坏其中的地址</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>0x23</p></td>
<td align="left"><p>驱动程序释放一个地址，但在同一页面内的邻近字节已损坏。</p></td>
</tr>
<tr class="even">
<td align="left"><p>该驱动程序尝试免费的地址</p></td>
<td align="left"><p>Bits 已损坏其中的地址</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>0x24</p></td>
<td align="left"><p>驱动程序释放一个地址，但已被覆盖字节分配结束后发生。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>当前 IRQL</p></td>
<td align="left"><p>池类型</p></td>
<td align="left"><p>字节数</p></td>
<td align="left"><p>0x30</p></td>
<td align="left"><p>尝试在不正确的 IRQL 池分配一个驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>当前 IRQL</p></td>
<td align="left"><p>池类型</p></td>
<td align="left"><p>该驱动程序尝试免费的地址</p></td>
<td align="left"><p>0x31</p></td>
<td align="left"><p>驱动程序尝试以释放不正确的 IRQL 在池。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>该驱动程序尝试免费的地址</p></td>
<td align="left"><p>其中一位已损坏的地址</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>0x32</p></td>
<td align="left"><p>驱动程序释放一个地址，但在同一页面内的邻近字节具有单一位错误。</p></td>
</tr>
</tbody>
</table>

 

\_池\_ntddk.h 中枚举类型代码。 具体而言，零表示非分页缓冲的池和一个指示页面缓冲的池。

<a name="cause"></a>原因
-----

驱动程序已写入到特殊的池的无效部分。

<a name="resolution"></a>分辨率
----------

获取当前线程的回溯。 此反向跟踪通常会揭示错误的源。

有关特殊的池的信息，请查阅 Windows 驱动程序工具包的驱动程序验证程序部分。

 

 




