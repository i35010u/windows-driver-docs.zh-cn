---
title: 移植问题清单
description: 移植问题清单
ms.assetid: 6ab26321-85b8-4a5b-8ca5-af6cbf56ccd6
keywords:
- 64位 WDK 内核，将驱动程序移植到
- 将驱动程序移植到64位 Windows
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e523c95115c6994216d83bf8d9dbffe89e649487
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827661"
---
# <a name="porting-issues-checklist"></a>移植问题清单





### <a name="general"></a>“常规”

-   使用新的64位安全 Windows 数据类型。

    本文档前面所述的新64位安全数据类型是在 Basetsd 中定义的。 此标头文件包含在 Ntdef 中，该文件包含在 Ntddk、Wdm 和 Ntifs 中。

-   仔细使用平台编译器宏。

    以下假设不再有效：

    ```cpp
    #ifdef _WIN32  // 32-bit Windows code
    ...
    #else          // 16-bit Windows code
    ...
    #endif
    ```

    但是，64位编译器定义 \_WIN32 以便向后兼容。

    此外，以下假设不再有效：

    ```cpp
    #ifdef _WIN16  // 16-bit Windows code
    ...
    #else          // 32-bit Windows code
    ...
    #endif
    ```

    在这种情况下，else 子句可以表示 WIN64 \_WIN32 或 \_。

-   结合使用正确的格式说明符和**printf**和**wsprintf**。

    使用 **% p**来打印十六进制形式的指针。 这是打印指针的最佳选择。

    **请注意**   未来版本的视觉C++对象将支持 **% I**来打印多态数据。 它在64位 windows 中将值视为64位，在32位 Windows 中将其视为32位。 视觉C++对象还支持 **% I64**打印64位的值。

     

<!-- -->

-   了解地址空间。

    不要盲目假设，例如，如果地址是内核地址，则必须设置其高序位。 若要获取最低系统地址，请使用**MM\_最低\_系统\_地址**宏。

### <a name="pointer-arithmetic"></a>指针算法

-   执行未签名和签名的操作时请小心。

    请考虑下列各项：

    ```cpp
    ULONG x;
    LONG y;
    LONG *pVar1;
    LONG *pVar2;
     
    pVar2 = pVar1 + y * (x - 1);
    ```

    出现此问题的原因是*x*是无符号的，这会使整个表达式无符号。 如果*y*为负数，则此操作正常。 在这种情况下， *y*转换为无符号的值，使用32位精度计算表达式，并将其添加到*pVar1*。 在64位 Windows 上，此32位无符号负数将成为较大的64位正数，这会产生错误的结果。 若要解决此问题，请将*x*声明为有符号值，或在表达式中将其显式转换为**LONG** 。

-   使用十六进制常量和无符号值时请小心。

    64位系统上的以下断言不成立：

    ```cpp
    ~((UINT64)(PAGE_SIZE-1)) == (UINT64)~(PAGE_SIZE-1)
    PAGE_SIZE = 0x1000UL  // Unsigned long - 32 bits
    PAGE_SIZE - 1 = 0x00000fff
    ```

    LHS 表达式：

    ```cpp
    // Unsigned expansion(UINT64)(PAGE_SIZE -1 ) = 0x0000000000000fff
    ~((UINT64)(PAGE_SIZE -1 )) = 0xfffffffffffff000
    ```

    RHS 表达式：

    ```cpp
    ~(PAGE_SIZE-1) = 0xfffff000
    (UINT64)(~(PAGE_SIZE - 1)) = 0x00000000fffff000
    ```

    就

    ```cpp
    ~((UINT64)(PAGE_SIZE-1)) != (UINT64)(~(PAGE_SIZE-1))
    ```

-   请注意 NOT 操作。

    请考虑下列各项：

    ```cpp
    UINT_PTR a; ULONG b;
    a = a & ~(b - 1); 
    ```

    问题在于 ~ （b −1）产生 0x0000 0000 *xxxx xxxx* ，而非 0xffff FFFF *xxxx*xxxx。 编译器不会检测到此情况。 若要解决此问题，请按如下所示更改代码：

    ```cpp
    a = a & ~((UINT_PTR)b - 1);
    ```

-   计算缓冲区大小时请小心。

    请考虑下列各项：

    ```cpp
    len = ptr2 - ptr1 
    /* len could be greater than 2**32 */
    ```

    指向指针算法的**PCHAR**的强制转换指针。

    **请注意**   如果*Len*声明为**INT**或**ULONG**，则会生成编译器警告。 即使在正确计算时，缓冲区大小仍可能超出**ULONG**的容量。

     

-   避免使用计算的或硬编码的指针偏移量。

    使用结构时，请尽可能使用[**字段\_OFFSET**](https://docs.microsoft.com/windows/desktop/api/ntdef/nf-ntdef-field_offset)宏来确定结构成员的偏移量。

-   避免使用硬编码指针或句柄值。

    不要将硬编码的指针或句柄（如处理）0xFFFFFFFF 传递到**ZwCreateSection**等例程。 相反，请使用常量（例如，无效\_句柄\_值）来定义每个平台的相应值。

-   请注意，在64位 Windows 中，0xFFFFFFFF 与-1 不相同。

    例如：

    ```cpp
    DWORD index = 0;
    CHAR *p;

    // if (p[index-1] == '0') causes access violation on 64-bit Windows!
    ```

    在32位计算机上：

    ```cpp
    p[index-1] == p[0xffffffff] == p[-1] 
    ```

    在64位计算机上：

    ```cpp
    p[index-1] == p[0x00000000ffffffff] != p[-1]
    ```

    可以通过将*索引*类型从**Dword**更改为**dword\_PTR**来避免此问题。

### <a name="polymorphism"></a>态

- 请注意多态接口。

  不要为多态数据创建接受**DWORD** （或其他固定精度类型）类型参数的函数。 如果数据可以是指针或整数值，则参数类型应为**UINT\_PTR**或**PVOID**，而不是**DWORD**。

  例如，不创建接受类型化为**DWORD**值的异常参数数组的函数。 数组应为**DWORD\_PTR**值的数组。 因此，数组元素可以保存地址或32位整数值。 一般规则是，如果原始类型为**DWORD**并且它需要是指针宽度，请将其转换为**dword\_PTR**值。 这就是本机 Win32 类型有相应的指针精度类型的原因。 如果你的代码使用**DWORD**、 **ULONG**或其他32位类型的多态方式（即，你确实希望参数或结构成员保存地址），请使用**UINT\_PTR**来代替当前类型。

- 调用具有指针 OUT 参数的函数时请小心。

  请勿执行此操作：

  ```cpp
  void GetBufferAddress(OUT PULONG *ptr);
  {
    *ptr=0x1000100010001000;
  }
  void foo()
  {
    ULONG bufAddress;
    //
    // This call causes memory corruption.
    //
    GetBufferAddress((PULONG *)&bufAddress);
  }
  ```

  Typecasting *bufAddress* To （**PULONG** \*）可防止出现编译器错误。 但是， *GetBufferAddress*会将64位值写入 *& bufAddress*的内存位置。 因为*bufAddress*只是一个32位值，所以将覆盖紧随*bufAddress*后面的32位。 这是一个非常微妙、难于发现的 bug。

- 不要将指针转换为**INT**、 **LONG**、 **ULONG**或**DWORD**。

  如果必须强制转换指针来测试某些位、设置或清除位或以其他方式操作其内容，请使用**UINT**\_**ptr**或**INT**\_**ptr**类型。 这些类型是一种整型类型，可缩放为32位和64位 Windows 的指针大小（例如， **ULONG**适用于32位 windows，为64位 windows **\_int64** ）。 例如，假设要移植以下代码：

  ```cpp
  ImageBase = (PVOID)((ULONG)ImageBase | 1);
  ```

  作为移植过程的一部分，你需要更改代码，如下所示：

  ```cpp
  ImageBase = (PVOID)((ULONG_PTR)ImageBase | 1);
  ```

  在适当的位置使用**UINT**\_**ptr**和**INT**\_**ptr** （如果不确定是否需要它们，则在使用时，不会造成任何损害。 不要将指针转换为**ULONG**、 **LONG**、 **INT**、 **UINT**或**DWORD**类型。

  **注意** **句柄**定义为**void \\** ，因此 typecasting，要测试、设置或清除低两位的**ULONG**值<em>的 **HANDLE</em>* 值是编程错误。

     

- 使用**PtrToLong**和**PtrToUlong**截断指针。

  如果必须截断指向32位值的指针，请使用**PtrToLong**或**PtrToUlong**函数（在*Basetsd*中定义）。 此函数在调用期间禁用指针截断警告。

  仔细使用这些功能。 使用这些函数之一截断指针变量后，不要将生成的**LONG**或**ULONG**强制转换回指针。 这些函数截断地址的上限32位，通常需要使用此地址来访问指针最初引用的内存。 在不仔细考虑的情况下使用这些函数将导致代码脆弱。

### <a name="data-structures-and-structure-alignment"></a>数据结构和结构对齐

-   仔细检查数据结构指针的所有使用情况。

    以下是常见的问题：

    -   存储在磁盘上或与32位进程交换的数据结构。
    -   带有指针的显式和隐式联合。
    -   安全描述符。

<!-- -->

-   使用[**字段\_OFFSET**](https://docs.microsoft.com/windows/desktop/api/ntdef/nf-ntdef-field_offset)宏 "。

    例如：

    ```cpp
    struct xx {
       DWORD NumberOfPointers;
       PVOID Pointers[1];
    };
     
    ```

    64位 Windows 中的以下分配是不正确的，因为编译器将使用额外的4个字节填充结构以生成8字节对齐要求：

    ```cpp
    malloc(sizeof(DWORD)+100*sizeof(PVOID)); 
     
    ```

    下面介绍如何正确执行此操作：

    ```cpp
    malloc(FIELD_OFFSET(struct xx, Pointers) +100*sizeof(PVOID));
    ```

-   使用 "**类型\_对齐**宏"。

    **类型\_对齐方式**宏返回当前平台上给定数据类型的对齐要求。 例如：

    ```cpp
    TYPE_ALIGNMENT(KFLOATING_SAVE) == 4 on x86, 8 on Itanium
    TYPE_ALIGNMENT(UCHAR) == 1 everywhere
    ```

    例如，如下所示的代码：

    ```cpp
    ProbeForRead(UserBuffer, UserBufferLength, sizeof(ULONG));
    ```

    更改为时变得更易于移植：

    ```cpp
    ProbeForRead(UserBuffer, UserBufferLength, TYPE_ALIGNMENT(ULONG));
    ```

-   监视公共内核结构中的数据类型更改。

    例如，IO\_状态\_块结构的**信息**字段现在的类型为**ULONG\_PTR**。

-   使用结构打包指令时要格外小心。

    在64位 Windows 上，如果数据结构未对齐，则操作结构的例程（如[**RtlCopyMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlcopymemory)和**memcpy**）将不会出错。 相反，它们将引发异常。 例如：

    ```cpp
    #pragma pack (1)  /* also set by /Zp switch */
    struct Buffer {
        ULONG size;
        void *ptr;
    };

    void SetPointer(void *p) {
        struct Buffer s;
        s.ptr = p;  /* will cause alignment fault */
        ...
    }
    ```

    可以使用未**对齐**的宏来解决此问题：

    ```cpp
    void SetPointer(void *p) {
        struct Buffer s;
        *(UNALIGNED void *)&s.ptr = p;
    }
    ```

    遗憾的是，使用未**对齐**的宏在基于 Itanium 的处理器上非常昂贵。 更好的解决方案是将64位值和指针放在结构的开头。

    **请注意**  如有可能，请避免在同一标头文件中使用不同的包装级别。

     

### <a name="additional-information"></a>其他信息

-   [支持64位驱动程序中的32位 i/o](supporting-32-bit-i-o-in-your-64-bit-driver.md)

-   [准备好64位 Windows](https://docs.microsoft.com/windows/desktop/WinProg64/getting-ready-for-64-bit-windows) （用户模式应用程序移植指南）

 

 




