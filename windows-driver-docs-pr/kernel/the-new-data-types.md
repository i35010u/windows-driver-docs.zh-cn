---
title: 新数据类型
description: 新数据类型
ms.assetid: 13a0d51e-0a9a-471f-8427-d4a7a7eb6459
keywords:
- 64 位 WDK 内核，移植到驱动程序
- 移植到 64 位 Windows 的驱动程序
- 数据类型 WDK 64 位
- 固定精度的整数类型 WDK 64 位
- 指针精度的整数类型 WDK 64 位
- 特定于精度指针类型 WDK 64 位
- 转换数据类型
- 64 位 WDK 内核，数据类型
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85c1158f8a67c31d017f5aaf15d0db117825f776
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353561"
---
# <a name="the-new-data-types"></a>新数据类型





有三个类的新的数据类型： 固定精度的整数类型、 指针精度的整数类型和特定于精度指针类型。 这些类型已添加到 Windows 环境 （特别是，对 Basetsd.h)，允许开发人员准备好之前引入的 64 位 Windows。 这些新类型被派生自基本的 C 语言整数和长类型，以便在现有代码中起作用。 因此，使用在代码中的类型现在，测试你的代码在 32 位 Windows 上和 64 位编译器用于查找并提前解决可移植性问题，因此您的驱动程序可以是准备就绪后 64 位 Windows 可用于测试这些数据。

此外，采用这些新的数据类型将使代码更可靠。 若要使用这些数据类型，必须扫描代码中可能不安全的指针使用情况、 多态性，以及数据定义。 为了安全起见，使用新的类型。 例如，当变量属于类型时才**ULONG\_PTR**，很明显，它将使用的强制转换指针的算术运算和多态性。 不能直接通过使用本机 Win32 数据类型来指示这类使用情况。 您可以执行此操作通过使用派生的类型命名或匈牙利表示法，但这两种方法容易出错。

### <a name="fixed-precision-integer-types"></a>固定精度的整数类型

固定精度的数据类型都具有相同的长度为 32 位和 64 位编程。 为了帮助您记住这，其精度为数据类型的名称的一部分。 以下是固定精度的数据类型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>在任务栏的搜索框中键入</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DWORD32</strong></p></td>
<td><p>32 位无符号的整数</p></td>
</tr>
<tr class="even">
<td><p><strong>DWORD64</strong></p></td>
<td><p>64 位无符号的整数</p></td>
</tr>
<tr class="odd">
<td><p><strong>INT32</strong></p></td>
<td><p>32 位有符号的整数</p></td>
</tr>
<tr class="even">
<td><p><strong>INT64</strong></p></td>
<td><p>64 位有符号的整数</p></td>
</tr>
<tr class="odd">
<td><p><strong>LONG32</strong></p></td>
<td><p>32 位有符号的整数</p></td>
</tr>
<tr class="even">
<td><p><strong>LONG64</strong></p></td>
<td><p>64 位有符号的整数</p></td>
</tr>
<tr class="odd">
<td><p><strong>UINT32</strong></p></td>
<td><p>无符号<strong>INT32</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>UINT64</strong></p></td>
<td><p>无符号<strong>INT64</strong></p></td>
</tr>
<tr class="odd">
<td><p><strong>ULONG32</strong></p></td>
<td><p>无符号<strong>LONG32</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>ULONG64</strong></p></td>
<td><p>无符号<strong>LONG64</strong></p></td>
</tr>
</tbody>
</table>

 

### <a name="pointer-precision-integer-types"></a>指针精度的整数类型

当指针精确度更改时 （即，因为它将成为 32 位用于 32 位平台，用于 64 位平台编译时的 64 位编译时），这些数据类型将相应地反映的精度。 因此，则可以安全地强制转换到其中一种类型的指针执行指针算术; 时如果指针精确度为 64 位，类型为 64 位。 计数类型还反映一个指针，可以引用的最大大小。 以下是指针精确度和计数类型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>在任务栏的搜索框中键入</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DWORD_PTR</strong></p></td>
<td><p>指针精确度的无符号 long 类型。</p></td>
</tr>
<tr class="even">
<td><p><strong>HALF_PTR</strong></p></td>
<td><p>带符号整型类型的后半部分指针精确度 （在 32 位系统中，在 64 位系统上的 32 位的 16 位）。</p></td>
</tr>
<tr class="odd">
<td><p><strong>INT_PTR</strong></p></td>
<td><p>带符号整型类型的指针精确度。</p></td>
</tr>
<tr class="even">
<td><p><strong>LONG_PTR</strong></p></td>
<td><p>带符号长类型的指针精确度。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SIZE_T</strong></p></td>
<td><p>最大可以引用的指针的字节数。 使用此类型必须跨越多个完整范围的指针的计数。</p></td>
</tr>
<tr class="even">
<td><p><strong>SSIZE_T</strong></p></td>
<td><p>签名<strong>SIZE_T</strong>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>UHALF_PTR</strong></p></td>
<td><p>无符号<strong>HALF_PTR</strong>。</p></td>
</tr>
<tr class="even">
<td><p><strong>UINT_PTR</strong></p></td>
<td><p>无符号<strong>INT_PTR</strong>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ULONG_PTR</strong></p></td>
<td><p>无符号<strong>LONG_PTR</strong>。</p></td>
</tr>
</tbody>
</table>

 

### <a name="fixed-precision-pointer-types"></a>固定精度指针类型

也有新的显式大小指针的指针类型。 在 64 位代码中使用这些指针类型时要小心：如果声明使用 32 位类型的指针，系统将创建通过截断将 64 位指针的指针。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>在任务栏的搜索框中键入</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>POINTER_32</strong></p></td>
<td><p>将 32 位指针。 在 32 位系统上，这是本机指针。 在 64 位系统上，这是被截断的 64 位指针。</p></td>
</tr>
<tr class="even">
<td><p><strong>POINTER_64</strong></p></td>
<td><p>将 64 位指针。 在 64 位系统上，这是本机指针。 在 32 位系统上，这是一个符号扩展的 32 位指针。</p>
<p>请注意，不安全地假定高指针位的状态。</p></td>
</tr>
</tbody>
</table>

 

### <a name="helper-functions"></a>帮助器函数

以下内联函数 （Basetsd.h 中定义） 可帮助你安全地转换值从一种类型到另一个：

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

**警告**  **IntToPtr**登录扩展**int**值**UIntToPtr**补零无符号**int**值、 **LongToPtr**补符号**长**值，并且**ULongToPtr**零扩展**无符号长**值。

 

 

 




