---
title: Windows 内核全局变量
description: 内核全局变量。
ms.assetid: 1ea5c4e3-ed70-449c-a49e-b1e3c892e981
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ecaf5b20ac14617420e08e38dad895a204a1bfc5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565545"
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
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Mm64BitPhysicalAddress</strong></td>
<td><code>PBOOLEAN Mm64BitPhysicalAddress</code>
<p>中 wdm.h 中声明</p></td>
<td><p>指定的硬件和操作系统是否支持 64 位物理地址。 指向一个值，则该值<strong>，则返回 TRUE</strong>如果硬件和操作系统支持 64 位物理地址，并且是<strong>FALSE</strong>否则为。</p>
<p>有关如何在您的驱动程序中使用此变量的详细信息，请参阅<a href="performing-dma-in-64-bit-windows.md" data-raw-source="[Performing DMA in 64-Bit Windows](performing-dma-in-64-bit-windows.md)">64 位 Windows 中执行 DMA</a>。</p></td>
</tr>
<tr class="even">
<td><strong>MmBadPointer</strong></td>
<td><code>PVOID MmBadPointer;</code>
<p>中 wdm.h 中声明</p></td>
<td><p>指向保证是无效的内存位置的指针。</p>
<div class="alert">
<strong>请注意</strong>从 Windows 8.1 <strong>MmBadPointer</strong>已弃用。 驱动程序应使用<a href="mm-bad-pointer.md#mm_bad_pointer" data-raw-source="[&lt;strong&gt;MM_BAD_POINTER&lt;/strong&gt;](mm-bad-pointer.md#mm_bad_pointer)"> <strong>MM_BAD_POINTER</strong> </a>宏相反。
</div>
<div>
 
</div>
<p>操作系统生成 bug 检查内存地址指定的<strong>MmBadPointer</strong>访问变量。</p>
<p>可以使用<strong>MmBadPointer</strong>调试驱动程序代码。 将任何未初始化的指针变量设置为<strong>MmBadPointer</strong>若要查找你的代码尝试取消引用了无效的指针的第一个时间。</p>
<p>所有地址中的 PAGE_SIZE <strong>MmBadPointer</strong>保证无效。 例如，如果<em>地址</em>是指针; 如果<strong>MmBadPointer</strong> &lt; = <em>地址</em> &lt; <strong>MmBadPointer</strong> + PAGE_SIZE，尝试访问 *<em>地址</em>会导致操作系统生成的 bug 检查。 <strong>MmBadPointer</strong> + PAGE_SIZE 不保证无效。</p></td>
</tr>
<tr class="odd">
<td><strong>PsInitialSystemProcess</strong></td>
<td><code>PEPROCESS PsInitialSystemProcess;</code>
<p>Ntddk.h 中声明</p></td>
<td><p>指向<a href="eprocess.md" data-raw-source="[&lt;strong&gt;EPROCESS&lt;/strong&gt;](eprocess.md)"> <strong>EPROCESS</strong> </a>系统进程的结构。</p></td>
</tr>
<tr class="even">
<td><strong>NLS_MB_CODE_PAGE_TAG</strong></td>
<td><code>extern BOOLEAN  NLS_MB_CODE_PAGE_TAG;</code></td>
<td><p>指定代码页是单字节或多字节代码页。</p>
<p><strong>NLS_MB_CODE_PAGE_TAG</strong>是<strong>TRUE</strong>的多字节代码页和<strong>FALSE</strong>的单字节代码页。</p>
<p>NLS_MB_CODE_PAGE_TAG 保留供系统使用。 从用户模式下，调用<a href="https://go.microsoft.com/fwlink/p/?linkid=121902" data-raw-source="[GetCPInfoEx](https://go.microsoft.com/fwlink/p/?linkid=121902)">GetCPInfoEx</a>相反。</p>
<p>如果可能，你的应用程序应使用 Unicode，而不是代码页。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[**EPROCESS**](eprocess.md)  
[GetCPInfoEx](https://go.microsoft.com/fwlink/p/?linkid=121902)  
[**MM\_错误\_指针**](mm-bad-pointer.md#mm_bad_pointer)  
[在 64 位 Windows 中执行 DMA](performing-dma-in-64-bit-windows.md)  



