---
title: Windows 内核全局变量
description: 内核全局变量。
ms.assetid: 1ea5c4e3-ed70-449c-a49e-b1e3c892e981
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2fdcb277255b0798b21e9cfa9dd3a763f7bcb582
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733489"
---
# <a name="windows-kernel-global-variables"></a>Windows 内核全局变量


内核全局变量。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>变量</th>
<th>声明</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Mm64BitPhysicalAddress</strong></td>
<td><code>PBOOLEAN Mm64BitPhysicalAddress</code>
<p>在 Wdm 中声明</p></td>
<td><p>指定硬件和操作系统是否支持64位物理地址。 指向一个值。如果硬件和操作系统支持64位物理地址，则该值为 <strong>TRUE</strong> ; 否则为 <strong>FALSE</strong> 。</p>
<p>有关如何在您的驱动程序中使用此变量的详细信息，请参阅 <a href="performing-dma-in-64-bit-windows.md" data-raw-source="[Performing DMA in 64-Bit Windows](performing-dma-in-64-bit-windows.md)">在64位 Windows 中执行 DMA</a>。</p></td>
</tr>
<tr class="even">
<td><strong>MmBadPointer</strong></td>
<td><code>PVOID MmBadPointer;</code>
<p>在 Wdm 中声明</p></td>
<td><p>指向可保证无效的内存位置的指针。</p>
<div class="alert">
<strong>注意</strong>  从 Windows 8.1 开始， <strong>MmBadPointer</strong> 已弃用。 驱动程序应改为使用 <a href="mm-bad-pointer.md#mm_bad_pointer" data-raw-source="[&lt;strong&gt;MM_BAD_POINTER&lt;/strong&gt;](mm-bad-pointer.md#mm_bad_pointer)"><strong>MM_BAD_POINTER</strong></a> 宏。
</div>
<div>
 
</div>
<p>如果访问由 <strong>MmBadPointer</strong> 变量指定的内存地址，操作系统会生成 bug 检查。</p>
<p>可以使用 <strong>MmBadPointer</strong> 来调试驱动程序代码。 将任何未初始化的指针变量设置为 <strong>MmBadPointer</strong> ，以便在第一次代码尝试取消引用无效的指针时查找。</p>
<p>保证 <strong>MmBadPointer</strong> PAGE_SIZE 中的所有地址都是无效的。 例如，如果<em>address</em>是一个指针，并且如果<strong>MmBadPointer</strong> &lt; =  <em>address</em> &lt; <strong>MmBadPointer</strong> + PAGE_SIZE，则尝试访问 *<em>地址</em>会导致操作系统生成 bug 检查。 <strong>MmBadPointer</strong> + 不保证 PAGE_SIZE 无效。</p></td>
</tr>
<tr class="odd">
<td><strong>PsInitialSystemProcess</strong></td>
<td><code>PEPROCESS PsInitialSystemProcess;</code>
<p>在 Ntddk 中声明</p></td>
<td><p>指向系统进程的 <a href="eprocess.md" data-raw-source="[&lt;strong&gt;EPROCESS&lt;/strong&gt;](eprocess.md)"><strong>EPROCESS</strong></a> 结构。</p></td>
</tr>
<tr class="even">
<td><strong>NLS_MB_CODE_PAGE_TAG</strong></td>
<td><code>extern BOOLEAN  NLS_MB_CODE_PAGE_TAG;</code></td>
<td><p>指定代码页是单字节代码页还是多字节代码页。</p>
<p>对于多字节代码页<strong>NLS_MB_CODE_PAGE_TAG</strong>为<strong>TRUE</strong> ，对于单字节代码页，则为<strong>FALSE</strong> 。</p>
<p>NLS_MB_CODE_PAGE_TAG 保留供系统使用。 在用户模式下，请改为调用 <a href="/previous-versions//ms776330(v=vs.85)" data-raw-source="[GetCPInfoEx](/previous-versions//ms776330(v=vs.85))">GetCPInfoEx</a> 。</p>
<p>如果可能，应用程序应使用 Unicode，而不是代码页。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[**EPROCESS**](eprocess.md)  
[GetCPInfoEx](/previous-versions//ms776330(v=vs.85))  
[**MM \_ 错误 \_ 指针**](mm-bad-pointer.md#mm_bad_pointer)  
[在 64 位 Windows 中执行 DMA](performing-dma-in-64-bit-windows.md)