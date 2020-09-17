---
title: 移植问题清单
description: 移植问题清单
ms.assetid: 6ab26321-85b8-4a5b-8ca5-af6cbf56ccd6
keywords:
- 64位 WDK 内核，将驱动程序移植到
- 将驱动程序移植到64位 Windows
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9458ac090f332b95686218a73ecfbb1f881fc878
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715534"
---
# <a name="porting-issues-checklist"></a>移植问题清单





### <a name="general"></a>常规

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

    但是，64位编译器定义了 \_ WIN32 以便向后兼容。

    此外，以下假设不再有效：

    ```cpp
    #ifdef _WIN16  // 16-bit Windows code
    ...
    #else          // 32-bit Windows code
    ...
    #endif
    ```

    在这种情况下，else 子句可以表示 \_ WIN32 或 \_ WIN64。

-   结合使用正确的格式说明符和 **printf** 和 **wsprintf**。

    使用 **% p** 来打印十六进制形式的指针。 这是打印指针的最佳选择。

    **注意**   Visual C++ 的未来版本将支持 **% I**来打印多态数据。 它在64位 windows 中将值视为64位，在32位 Windows 中将其视为32位。 Visual C++ 还将支持 **% I64** 打印64位的值。

     

<!-- -->

-   了解地址空间。

    不要盲目假设，例如，如果地址是内核地址，则必须设置其高序位。 若要获取最低系统地址，请使用 **MM \_ \_ system \_ address** 宏。

### <a name="pointer-arithmetic"></a>指针算术

-   执行未签名和签名的操作时请小心。

    考虑以下情况：

    ```cpp
    ULONG x;
    LONG y;
    LONG *pVar1;
    LONG *pVar2;
     
    pVar2 = pVar1 + y * (x - 1);
    ```

    出现此问题的原因是 *x* 是无符号的，这会使整个表达式无符号。 如果 *y* 为负数，则此操作正常。 在这种情况下， *y* 转换为无符号的值，使用32位精度计算表达式，并将其添加到 *pVar1*。 在64位 Windows 上，此32位无符号负数将成为较大的64位正数，这会产生错误的结果。 若要解决此问题，请将 *x* 声明为有符号值，或在表达式中将其显式转换为 **LONG** 。

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

    考虑以下情况：

    ```cpp
    UINT_PTR a; ULONG b;
    a = a & ~(b - 1); 
    ```

    问题在于 ~ (b − 1) 生成 0x0000 0000 *xxxx xxxx* ，而非 0xffff FFFF *xxxx*xxxx。 编译器不会检测到此情况。 若要解决此问题，请按如下所示更改代码：

    ```cpp
    a = a & ~((UINT_PTR)b - 1);
    ```

-   计算缓冲区大小时请小心。

    考虑以下情况：

    ```cpp
    len = ptr2 - ptr1 
    /* len could be greater than 2**32 */
    ```

    指向指针算法的 **PCHAR** 的强制转换指针。

    **注意**   如果*len*声明为**INT**或**ULONG**，则会生成编译器警告。 即使在正确计算时，缓冲区大小仍可能超出 **ULONG**的容量。

     

-   避免使用计算的或硬编码的指针偏移量。

    使用结构时，尽可能使用 [**字段 \_ 偏移**](/windows/win32/api/ntdef/nf-ntdef-field_offset) 宏来确定结构成员的偏移量。

-   避免使用硬编码指针或句柄值。

    不要将硬编码的指针或句柄（如 (句柄) 0xFFFFFFFF）传递到 **ZwCreateSection**（如）。 相反，请使用 \_ \_ 可以定义为每个平台的适当值的常量（例如无效的句柄值）。

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

    可以通过将 *索引* 类型从 **Dword** 更改为 **dword \_ PTR**来避免此问题。

### <a name="polymorphism"></a>多形性

- 请注意多态接口。

  不要为多态数据创建接受 **DWORD** (或其他固定精度类型的参数的函数) 。 如果数据可以是指针或整数值，则参数类型应为 **UINT \_ PTR** 或 **PVOID**，而不是 **DWORD**。

  例如，不创建接受类型化为 **DWORD** 值的异常参数数组的函数。 数组应为 **DWORD \_ PTR** 值的数组。 因此，数组元素可以保存地址或32位整数值。 一般规则是，如果原始类型为 **DWORD** 并且它需要是指针宽度，请将其转换为 **dword \_ PTR** 值。 这就是本机 Win32 类型有相应的指针精度类型的原因。 如果你的代码使用 **DWORD**、 **ULONG**或其他32位类型的多态方式 (也就是说，你确实希望参数或结构成员保存地址) ，请使用 **UINT \_ PTR** 来代替当前类型。

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

  Typecasting *bufAddress* To (**PULONG** \*) 防止出现编译器错误。 但是， *GetBufferAddress* 会将64位值写入 *&bufAddress*的内存位置。 因为 *bufAddress* 只是一个32位值，所以将覆盖紧随 *bufAddress* 后面的32位。 这是一个非常微妙、难于发现的 bug。

- 不要将指针转换为 **INT**、 **LONG**、 **ULONG**或 **DWORD**。

  如果必须强制转换指针来测试某些位、设置或清除位或以其他方式操作其内容，请使用**UINT** \_ **ptr**类型或**INT** \_ **ptr**类型。 这些类型是一种整型类型，可缩放为32位和64位 Windows (的指针大小，例如， **ULONG**用于32位 windows，以及用于64位 windows) 的** \_ int64** 。 例如，假设要移植以下代码：

  ```cpp
  ImageBase = (PVOID)((ULONG)ImageBase | 1);
  ```

  作为移植过程的一部分，你需要更改代码，如下所示：

  ```cpp
  ImageBase = (PVOID)((ULONG_PTR)ImageBase | 1);
  ```

  在适当的 (中使用**UINT** \_ **ptr**和**INT** \_ **ptr** ，如果不确定是否需要它们，则在) 时不会有任何损害。 不要将指针转换为 **ULONG**、 **LONG**、 **INT**、 **UINT**或 **DWORD**类型。

  **注意****句柄**定义为**void \\ ** <em>，因此 typecasting，*将</em>* 值设置为**ULONG**值以测试、设置或清除低两位是编程错误。  

     

- 使用 **PtrToLong** 和 **PtrToUlong** 截断指针。

  如果必须截断指向32位值的指针，请使用*Basetsd*) 中定义的**PtrToLong**或**PtrToUlong**函数 (。 此函数在调用期间禁用指针截断警告。

  仔细使用这些功能。 使用这些函数之一截断指针变量后，不要将生成的 **LONG** 或 **ULONG** 强制转换回指针。 这些函数截断地址的上限32位，通常需要使用此地址来访问指针最初引用的内存。 在不仔细考虑的情况下使用这些函数将导致代码脆弱。

### <a name="data-structures-and-structure-alignment"></a>数据结构和结构对齐

-   仔细检查数据结构指针的所有使用情况。

    以下是常见的问题：

    -   存储在磁盘上或与32位进程交换的数据结构。
    -   带有指针的显式和隐式联合。
    -   安全描述符。

<!-- -->

-   使用 [**字段 \_ 偏移**](/windows/win32/api/ntdef/nf-ntdef-field_offset) 宏。

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

-   使用 " **类型 \_ 对齐** " 宏。

    **类型 \_ 对齐**宏返回当前平台上给定数据类型的对齐要求。 例如：

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

    例如，IO 状态**Information**块结构中的信息 \_ 字段 \_ 现在为**ULONG \_ PTR**类型。

-   使用结构打包指令时要格外小心。

    在64位 Windows 上，如果数据结构未对齐，则操作结构的例程（如 [**RtlCopyMemory**](/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlcopymemory) 和 **memcpy**）将不会出错。 相反，它们将引发异常。 例如：

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

    可以使用未 **对齐** 的宏来解决此问题：

    ```cpp
    void SetPointer(void *p) {
        struct Buffer s;
        *(UNALIGNED void *)&s.ptr = p;
    }
    ```

    遗憾的是，使用未 **对齐** 的宏在基于 Itanium 的处理器上非常昂贵。 更好的解决方案是将64位值和指针放在结构的开头。

    **注意**   如果可能，请避免在同一标头文件中使用不同的包装级别。

     

### <a name="additional-information"></a>其他信息

-   [在 64 位驱动程序中支持 32 位 I/O](supporting-32-bit-i-o-in-your-64-bit-driver.md)

-   [准备好64位 Windows](/windows/desktop/WinProg64/getting-ready-for-64-bit-windows) (用户模式应用程序迁移指南) 

 

