---
title: Windows 内核运行时库的已过时例程
description: Windows 内核运行时库的已过时例程
ms.assetid: cd9aa441-a7f2-42b1-8319-611bf53c995d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 288b4145db7542de3dec4a22e0e33e4eeedb1837
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373397"
---
# <a name="windows-kernel-run-time-library-obsolete-routines"></a>Windows 内核运行时库的已过时例程


导出以下运行时库已过时例程以支持现有的驱动程序二进制文件：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>已过时的例程</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>RtlEnlargedIntegerMultiply</strong></td>
<td><p>为了提高性能，使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntintsafe/nf-ntintsafe-rtlulongmult" data-raw-source="[&lt;strong&gt;RtlLongMult&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntintsafe/nf-ntintsafe-rtlulongmult)"> <strong>RtlLongMult</strong> </a>例程，如果结果可放入一个 32 位有符号整数。 否则，使用编译器支持对 64 位整数运算。</p></td>
</tr>
<tr class="even">
<td><strong>RtlEnlargedUnsignedDivide</strong></td>
<td><p>为了提高性能，对 64 位整数运算中使用的编译器支持。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlEnlargedUnsignedMultiply</strong></td>
<td><p>为了提高性能，使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntintsafe/nf-ntintsafe-rtlulongmult" data-raw-source="[&lt;strong&gt;RtlULongMult&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntintsafe/nf-ntintsafe-rtlulongmult)"> <strong>RtlULongMult</strong> </a>例程，如果结果可放入一个 32 位无符号整数。 否则，使用编译器支持对 64 位整数运算。</p></td>
</tr>
<tr class="even">
<td><strong>RtlExtendedIntegerMultiply</strong></td>
<td><p>为了提高性能，对 64 位整数运算中使用的编译器支持。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlExtendedLargeIntegerDivide</strong></td>
<td><p>为了提高性能，对 64 位整数运算中使用的编译器支持。</p></td>
</tr>
<tr class="even">
<td><strong>RtlExtendedMagicDivide</strong></td>
<td><p>为了提高性能，对 64 位整数运算中使用的编译器支持。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlFillBytes</strong></td>
<td><p>用给定的无符号字符填充的调用方提供的缓冲区。 使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlfillmemory" data-raw-source="[&lt;strong&gt;RtlFillMemory&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlfillmemory)"> <strong>RtlFillMemory</strong> </a>相反。</p></td>
</tr>
<tr class="even">
<td><strong>RtlLargeIntegerAdd</strong></td>
<td><p>为了提高性能，对 64 位整数运算中使用的编译器支持。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlLargeIntegerAnd</strong></td>
<td><p>为了提高性能，对 64 位整数运算中使用的编译器支持。</p></td>
</tr>
<tr class="even">
<td><strong>RtlLargeIntegerArithmeticShift</strong></td>
<td><p>为了提高性能，对 64 位整数运算中使用的编译器支持。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlLargeIntegerDivide</strong></td>
<td><p>为了提高性能，对 64 位整数运算中使用的编译器支持。</p></td>
</tr>
<tr class="even">
<td><strong>RtlLargeIntegerEqualTo</strong></td>
<td><p>为了提高性能，对 64 位整数运算中使用的编译器支持。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlLargeIntegerEqualToZero</strong></td>
<td><p>为了提高性能，对 64 位整数运算中使用的编译器支持。</p></td>
</tr>
<tr class="even">
<td><strong>RtlLargeIntegerGreaterOrEqualToZero</strong></td>
<td><p>为了提高性能，对 64 位整数运算中使用的编译器支持。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlLargeIntegerGreaterThan</strong></td>
<td><p>为了提高性能，对 64 位整数运算中使用的编译器支持。</p></td>
</tr>
<tr class="even">
<td><strong>RtlLargeIntegerGreaterThanOrEqualTo</strong></td>
<td><p>为了提高性能，对 64 位整数运算中使用的编译器支持。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlLargeIntegerGreaterThanZero</strong></td>
<td><p>为了提高性能，对 64 位整数运算中使用的编译器支持。</p></td>
</tr>
<tr class="even">
<td><strong>RtlLargeIntegerLessOrEqualToZero</strong></td>
<td><p>为了提高性能，对 64 位整数运算中使用的编译器支持。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlLargeIntegerLessThan</strong></td>
<td><p>为了提高性能，对 64 位整数运算中使用的编译器支持。</p></td>
</tr>
<tr class="even">
<td><strong>RtlLargeIntegerLessThanOrEqualTo</strong></td>
<td><p>为了提高性能，对 64 位整数运算中使用的编译器支持。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlLargeIntegerLessThanZero</strong></td>
<td><p>为了提高性能，对 64 位整数运算中使用的编译器支持。</p></td>
</tr>
<tr class="even">
<td><strong>RtlLargeIntegerNegate</strong></td>
<td><p>为了提高性能，对 64 位整数运算中使用的编译器支持。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlLargeIntegerNotEqualTo</strong></td>
<td><p>为了提高性能，对 64 位整数运算中使用的编译器支持。</p></td>
</tr>
<tr class="even">
<td><strong>RtlLargeIntegerNotEqualToZero</strong></td>
<td><p>为了提高性能，对 64 位整数运算中使用的编译器支持。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlLargeIntegerShiftLeft</strong></td>
<td><p>为了提高性能，对 64 位整数运算中使用的编译器支持。</p></td>
</tr>
<tr class="even">
<td><strong>RtlLargeIntegerShiftRight</strong></td>
<td><p>为了提高性能，对 64 位整数运算中使用的编译器支持。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlLargeIntegerSubtract</strong></td>
<td><p>为了提高性能，对 64 位整数运算中使用的编译器支持。</p></td>
</tr>
<tr class="even">
<td><strong>RtlZeroBytes</strong></td>
<td><p>提供一个指向块和长度，以字节为单位，要填充的零，填充内存的块。 为了提高性能，使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlzeromemory" data-raw-source="[&lt;strong&gt;RtlZeroMemory&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlzeromemory)"> <strong>RtlZeroMemory</strong></a>。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[**RtlFillMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlfillmemory)  
[**RtlLongMult**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntintsafe/nf-ntintsafe-rtlulongmult)  
[**RtlZeroMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlzeromemory)  



