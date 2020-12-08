---
title: 新数据类型
description: 新数据类型
keywords:
- 64位 WDK 内核，将驱动程序移植到
- 将驱动程序移植到64位 Windows
- 数据类型 WDK 64 位
- 固定精度整数类型 WDK 64 位
- 指针精度整数类型 WDK 64 位
- 特定精度指针类型 WDK 64 位
- 转换数据类型
- 64位 WDK 内核，数据类型
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56199f85185f8f52f97bdae898be4723118c8712
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814281"
---
# <a name="the-new-data-types"></a>新数据类型





有三类新数据类型：固定精度整数类型、指针精度整数类型和特定精度指针类型。 这些类型已添加到 Windows 环境 (具体说来，到 Basetsd) ，以允许开发人员在引入之前准备好64位 Windows。 这些新类型派生自基本 C 语言整数和长类型，因此它们可在现有代码中使用。 因此，你现在可以在代码中使用这些数据类型，在32位 Windows 上测试你的代码，并使用64位编译器提前查找并修复可移植性问题，以便在64位 Windows 可用于测试时可以准备好驱动程序。

此外，采用这些新数据类型将使代码更可靠。 若要使用这些数据类型，您必须扫描您的代码以获得可能不安全的指针用法、多态性和数据定义。 为安全起见，请使用新类型。 例如，当变量的类型为 **ULONG \_ PTR** 时，很明显，它将用于转换算术运算或多态性的指针。 不能使用本机 Win32 数据类型直接指示这种用法。 可以通过使用派生类型命名或匈牙利表示法来实现此目的，但这两种方法都容易出错。

### <a name="fixed-precision-integer-types"></a>Fixed-Precision 整数类型

固定精度数据类型的长度与32位和64位编程的长度相同。 为帮助您记住这一点，其精度是数据类型名称的一部分。 下面是固定精度的数据类型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>类型</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DWORD32</strong></p></td>
<td><p>32 位无符号整数</p></td>
</tr>
<tr class="even">
<td><p><strong>DWORD64</strong></p></td>
<td><p>64 位无符号整数</p></td>
</tr>
<tr class="odd">
<td><p><strong>INT32</strong></p></td>
<td><p>32 位带符号整数</p></td>
</tr>
<tr class="even">
<td><p><strong>INT64</strong></p></td>
<td><p>64 位带符号整数</p></td>
</tr>
<tr class="odd">
<td><p><strong>LONG32</strong></p></td>
<td><p>32 位带符号整数</p></td>
</tr>
<tr class="even">
<td><p><strong>LONG64</strong></p></td>
<td><p>64 位带符号整数</p></td>
</tr>
<tr class="odd">
<td><p><strong>UINT32</strong></p></td>
<td><p>无符号 <strong>INT32</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>UINT64</strong></p></td>
<td><p>无符号 <strong>INT64</strong></p></td>
</tr>
<tr class="odd">
<td><p><strong>ULONG32</strong></p></td>
<td><p>无符号 <strong>LONG32</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>ULONG64</strong></p></td>
<td><p>无符号 <strong>LONG64</strong></p></td>
</tr>
</tbody>
</table>

 

### <a name="pointer-precision-integer-types"></a>Pointer-Precision 整数类型

当指针精度改变 (也就是说，在为32位平台编译时，32位就变成位，为64位平台编译时64位) ，这些数据类型会相应地反映精度。 因此，在执行指针算法时，可以安全地将指针转换为这些类型之一;如果指针精确度为64位，则类型为64位。 计数类型还反映了指针可引用的最大大小。 下面是指针的精度和计数类型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>类型</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DWORD_PTR</strong></p></td>
<td><p>指针精度的无符号长类型。</p></td>
</tr>
<tr class="even">
<td><p><strong>HALF_PTR</strong></p></td>
<td><p>半指针精度的带符号整型 (16 位在32位系统上，32比64位系统) 。</p></td>
</tr>
<tr class="odd">
<td><p><strong>INT_PTR</strong></p></td>
<td><p>指针精度的带符号整数类型。</p></td>
</tr>
<tr class="even">
<td><p><strong>LONG_PTR</strong></p></td>
<td><p>指针精度的带符号长类型。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SIZE_T</strong></p></td>
<td><p>指针可引用的最大字节数。 此类型用于必须跨越指针的整个范围的计数。</p></td>
</tr>
<tr class="even">
<td><p><strong>SSIZE_T</strong></p></td>
<td><p>签名 <strong>SIZE_T</strong>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>UHALF_PTR</strong></p></td>
<td><p>无符号 <strong>HALF_PTR</strong>。</p></td>
</tr>
<tr class="even">
<td><p><strong>UINT_PTR</strong></p></td>
<td><p>无符号 <strong>INT_PTR</strong>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ULONG_PTR</strong></p></td>
<td><p>无符号 <strong>LONG_PTR</strong>。</p></td>
</tr>
</tbody>
</table>

 

### <a name="fixed-precision-pointer-types"></a>Fixed-Precision 指针类型

还有显式调整指针大小的新指针类型。 在64位代码中使用这些指针类型时要小心：如果使用32位类型声明指针，系统将通过截断64位指针来创建指针。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>类型</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>POINTER_32</strong></p></td>
<td><p>32位指针。 在32位系统上，这是本机指针。 在64位系统上，这是一个被截断的64位指针。</p></td>
</tr>
<tr class="even">
<td><p><strong>POINTER_64</strong></p></td>
<td><p>64位指针。 在64位系统上，这是本机指针。 在32位系统上，这是一个带符号扩展的32位指针。</p>
<p>请注意，假定高指针位的状态是不安全的。</p></td>
</tr>
</tbody>
</table>

 

### <a name="helper-functions"></a>Helper 函数

 (在) Basetsd 中定义的以下内联函数可帮助你安全地将值从一种类型转换为另一种类型：

```cpp
unsigned long HandleToUlong( const void *h )
long HandleToLong( const void *h )
void * LongToHandle( const long h )
unsigned long PtrToUlong( const void *p )
unsigned int PtrToUint( const void *p )
unsigned short PtrToUshort( const void *p )
long PtrToLong( const void *p )
int PtrToInt( const void *p )
short PtrToShort( const void *p )
void * IntToPtr( const int i )
void * UIntToPtr( const unsigned int ui )
void * LongToPtr( const long l )
void * ULongToPtr( const unsigned long ul )
```

**警告**  **IntToPtr** -扩展 **int** 值， **UIntToPtr** 0-扩展无符号 **整数** 值， **LongToPtr** 符号扩展 **长** 值， **ULongToPtr** 零扩展 **无符号长整型** 值。

 

 

 




