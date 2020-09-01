---
title: Windows 内核运行时库的已过时例程
description: Windows 内核运行时库的已过时例程
ms.assetid: cd9aa441-a7f2-42b1-8319-611bf53c995d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 91e4fce8b3ef55b09b2a52a130c3541ed9ba7857
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185609"
---
# <a name="windows-kernel-run-time-library-obsolete-routines"></a>Windows 内核运行时库的已过时例程


为了支持现有的驱动程序二进制文件，将导出以下运行时库过时例程：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>过时例程</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>RtlEnlargedIntegerMultiply</strong></td>
<td><p>若要获得更好的性能，请使用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongmult" data-raw-source="[&lt;strong&gt;RtlLongMult&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongmult)"><strong>RtlLongMult</strong></a> 例程（如果结果适用于32位有符号整数）。 否则，请使用适用于64位整数操作的编译器支持。</p></td>
</tr>
<tr class="even">
<td><strong>RtlEnlargedUnsignedDivide</strong></td>
<td><p>为了获得更好的性能，请使用适用于64位整数操作的编译器支持。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlEnlargedUnsignedMultiply</strong></td>
<td><p>若要获得更好的性能，请在结果适用于32位无符号整数的情况下使用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongmult" data-raw-source="[&lt;strong&gt;RtlULongMult&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongmult)"><strong>RtlULongMult</strong></a> 例程。 否则，请使用适用于64位整数操作的编译器支持。</p></td>
</tr>
<tr class="even">
<td><strong>RtlExtendedIntegerMultiply</strong></td>
<td><p>为了获得更好的性能，请使用适用于64位整数操作的编译器支持。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlExtendedLargeIntegerDivide</strong></td>
<td><p>为了获得更好的性能，请使用适用于64位整数操作的编译器支持。</p></td>
</tr>
<tr class="even">
<td><strong>RtlExtendedMagicDivide</strong></td>
<td><p>为了获得更好的性能，请使用适用于64位整数操作的编译器支持。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlFillBytes</strong></td>
<td><p>使用给定的无符号字符填充调用方提供的缓冲区。 改用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlfillmemory" data-raw-source="[&lt;strong&gt;RtlFillMemory&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlfillmemory)"><strong>RtlFillMemory</strong></a> 。</p></td>
</tr>
<tr class="even">
<td><strong>RtlLargeIntegerAdd</strong></td>
<td><p>为了获得更好的性能，请使用适用于64位整数操作的编译器支持。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlLargeIntegerAnd</strong></td>
<td><p>为了获得更好的性能，请使用适用于64位整数操作的编译器支持。</p></td>
</tr>
<tr class="even">
<td><strong>RtlLargeIntegerArithmeticShift</strong></td>
<td><p>为了获得更好的性能，请使用适用于64位整数操作的编译器支持。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlLargeIntegerDivide</strong></td>
<td><p>为了获得更好的性能，请使用适用于64位整数操作的编译器支持。</p></td>
</tr>
<tr class="even">
<td><strong>RtlLargeIntegerEqualTo</strong></td>
<td><p>为了获得更好的性能，请使用适用于64位整数操作的编译器支持。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlLargeIntegerEqualToZero</strong></td>
<td><p>为了获得更好的性能，请使用适用于64位整数操作的编译器支持。</p></td>
</tr>
<tr class="even">
<td><strong>RtlLargeIntegerGreaterOrEqualToZero</strong></td>
<td><p>为了获得更好的性能，请使用适用于64位整数操作的编译器支持。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlLargeIntegerGreaterThan</strong></td>
<td><p>为了获得更好的性能，请使用适用于64位整数操作的编译器支持。</p></td>
</tr>
<tr class="even">
<td><strong>RtlLargeIntegerGreaterThanOrEqualTo</strong></td>
<td><p>为了获得更好的性能，请使用适用于64位整数操作的编译器支持。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlLargeIntegerGreaterThanZero</strong></td>
<td><p>为了获得更好的性能，请使用适用于64位整数操作的编译器支持。</p></td>
</tr>
<tr class="even">
<td><strong>RtlLargeIntegerLessOrEqualToZero</strong></td>
<td><p>为了获得更好的性能，请使用适用于64位整数操作的编译器支持。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlLargeIntegerLessThan</strong></td>
<td><p>为了获得更好的性能，请使用适用于64位整数操作的编译器支持。</p></td>
</tr>
<tr class="even">
<td><strong>RtlLargeIntegerLessThanOrEqualTo</strong></td>
<td><p>为了获得更好的性能，请使用适用于64位整数操作的编译器支持。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlLargeIntegerLessThanZero</strong></td>
<td><p>为了获得更好的性能，请使用适用于64位整数操作的编译器支持。</p></td>
</tr>
<tr class="even">
<td><strong>RtlLargeIntegerNegate</strong></td>
<td><p>为了获得更好的性能，请使用适用于64位整数操作的编译器支持。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlLargeIntegerNotEqualTo</strong></td>
<td><p>为了获得更好的性能，请使用适用于64位整数操作的编译器支持。</p></td>
</tr>
<tr class="even">
<td><strong>RtlLargeIntegerNotEqualToZero</strong></td>
<td><p>为了获得更好的性能，请使用适用于64位整数操作的编译器支持。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlLargeIntegerShiftLeft</strong></td>
<td><p>为了获得更好的性能，请使用适用于64位整数操作的编译器支持。</p></td>
</tr>
<tr class="even">
<td><strong>RtlLargeIntegerShiftRight</strong></td>
<td><p>为了获得更好的性能，请使用适用于64位整数操作的编译器支持。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlLargeIntegerSubtract</strong></td>
<td><p>为了获得更好的性能，请使用适用于64位整数操作的编译器支持。</p></td>
</tr>
<tr class="even">
<td><strong>RtlZeroBytes</strong></td>
<td><p>在给定指向块的指针和要填充的长度（以字节为单位）的情况下，使用零填充内存块。 为了获得更好的性能，请使用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlzeromemory" data-raw-source="[&lt;strong&gt;RtlZeroMemory&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlzeromemory)"><strong>RtlZeroMemory</strong></a>。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[**RtlFillMemory**](/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlfillmemory)  
[**RtlLongMult**](/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongmult)  
[**RtlZeroMemory**](/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlzeromemory)