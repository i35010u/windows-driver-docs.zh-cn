---
title: 移植问题清单
description: 移植问题清单
ms.assetid: 6ab26321-85b8-4a5b-8ca5-af6cbf56ccd6
keywords:
- 64 位 WDK 内核，移植到驱动程序
- 移植到 64 位 Windows 的驱动程序
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab2d63a59ae3a3fdfe5f81e3dc3d73a87b6a36d5
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349794"
---
# <a name="porting-issues-checklist"></a>移植问题清单





### <a name="general"></a>常规

-   使用新的 64 位安全 Windows 数据类型。

    Basetsd.h 中定义新的 64 位安全数据类型，本文档前面所述。 此标头文件包括在 Ntdef.h，包含在 Ntddk.h、 wdm.h 中和 Ntifs.h。

-   谨慎使用平台编译器宏。

    以下假设不再有效：

    ```cpp
    #ifdef _WIN32  // 32-bit Windows code
    ...
    #else          // 16-bit Windows code
    ...
    #endif
    ```

    但是，64 位编译器定义\_WIN32 向后兼容性。

    此外，以下假设不再有效：

    ```cpp
    #ifdef _WIN16  // 16-bit Windows code
    ...
    #else          // 32-bit Windows code
    ...
    #endif
    ```

    在这种情况下，可以表示 else 子句\_WIN32 或\_WIN64。

-   使用具有正确的格式说明符**printf**并**wsprintf**。

    使用 **%p**打印十六进制中的指针。 这是打印指针的最佳选择。

    **请注意**   Visual c + + 的未来版本将支持 **%I**打印多态数据。 它会将值视为在 64 位 Windows 和 32 位 Windows 中的 32 位的 64 位。 也支持 visual c + + **%i64**打印都是 64 位的值。

     

<!-- -->

-   知道您的地址空间。

    不要盲目地假定，例如，如果地址是内核地址，必须设置其高顺序位。 若要获取的最小的系统地址，请使用**MM\_最低\_系统\_地址**宏。

### <a name="pointer-arithmetic"></a>指针算术

-   执行未签名和签名操作时要小心。

    请考虑下列各项：

    ```cpp
    ULONG x;
    LONG y;
    LONG *pVar1;
    LONG *pVar2;
     
    pVar2 = pVar1 + y * (x - 1);
    ```

    因为将会出现问题*x*是未签名，因此未签名的整个表达式。 此工作正常，除非*y*为负。 在这种情况下， *y*转换为无符号值，计算该表达式，使用 32 位精度，比例进行调整，并添加到*pVar1*。 在 64 位 Windows 上此 32 位无符号的负数将成为大型 64 位正数，这将使错误结果。 若要解决此问题，请声明*x*为有符号值或显式类型转换到**长**在表达式中。

-   使用十六进制常量和无符号的值时要小心。

    以下断言不在 64 位系统上，则返回 true:

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

    因此：

    ```cpp
    ~((UINT64)(PAGE_SIZE-1)) != (UINT64)(~(PAGE_SIZE-1))
    ```

-   谨慎而不是操作数。

    请考虑下列各项：

    ```cpp
    UINT_PTR a; ULONG b;
    a = a & ~(b - 1); 
    ```

    问题在于该 ~(b−1) 生成 0x0000 0000 *xxxx xxxx*和不 0xFFFF FFFF *xxxx xxxx*。 编译器将不会检测此。 若要解决此问题，请按如下所示更改代码：

    ```cpp
    a = a & ~((UINT_PTR)b - 1);
    ```

-   计算缓冲区大小时要小心。

    请考虑下列各项：

    ```cpp
    len = ptr2 - ptr1 
    /* len could be greater than 2**32 */
    ```

    强制转换为指针**PCHAR**指针算法。

    **请注意**  如果*len*声明**INT**或者**ULONG**，这将生成编译器警告。 缓冲区大小，即使计算正确，可能会仍然超过容量**ULONG**。

     

-   避免使用计算出的或硬编码的指针的偏移量。

    使用结构，使用[**字段\_偏移量**](https://msdn.microsoft.com/library/windows/hardware/ff545727)宏只要有可能确定结构成员的偏移量。

-   避免使用硬编码的指针或句柄值。

    不要传递硬编码的指针或句柄 （手柄） 0xFFFFFFFF 如到例程如**ZwCreateSection**。 请改用常量，如无效\_处理\_值，该值可以定义为具有适当的值为每个平台。

-   请注意，在 64 位 Windows 中 0xFFFFFFFF 不相同，则为-1。

    例如：

    ```cpp
    DWORD index = 0;
    CHAR *p;

    // if (p[index-1] == '0') causes access violation on 64-bit Windows!
    ```

    在 32 位计算机：

    ```cpp
    p[index-1] == p[0xffffffff] == p[-1] 
    ```

    在 64 位计算机：

    ```cpp
    p[index-1] == p[0x00000000ffffffff] != p[-1]
    ```

    为避免此问题，只需更改的类型*索引*从**DWORD**到**DWORD\_PTR**。

### <a name="polymorphism"></a>多态性

- 要注意多态的接口。

  不创建接受的类型参数的函数**DWORD** （或其他固定精度类型） 的多态数据。 如果数据可以是指针或整数值，参数类型应为**UINT\_PTR**或**PVOID**，而非**DWORD**。

  例如，不创建接受的类型的异常参数数组的函数**DWORD**值。 数组应为一个数组**DWORD\_PTR**值。 因此，数组元素可以包含地址或 32 位整数值。 一般规则是，如果原始类型是**DWORD** ，它需指针宽度，将其转换为**DWORD\_PTR**值。 这是原因都有相应的本机 Win32 类型的指针精度类型。 如果使用的代码**DWORD**， **ULONG**，或其他 32 位类型中的多态方式 （即，真正想要保存一个地址的参数或结构的成员），使用**UINT\_PTR**来替代当前的类型。

- 调用具有输出参数的指针的函数时要小心。

  不这样做：

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

  类型上强制转换*bufAddress*到 (**PULONG** \*) 可防止发生编译器错误。 但是， *GetBufferAddress*将一个 64 位值写入内存位置 *& bufAddress*。 因为*bufAddress*是仅为 32 位值，紧跟 32 位*bufAddress*将被覆盖。 这是一个非常细微，硬查找 bug。

- 不强制转换为指针**INT**，**长**， **ULONG**，或者**DWORD**。

  如果必须转换为一个指针来测试某些内部测试版，设置或清除位为单位或否则为操作其内容，使用**UINT**\_**PTR**或**INT** \_**PTR**类型。 这些类型是为 32 位和 64 位 Windows 扩展到指针的大小的整型类型 (例如， **ULONG**的 32 位 Windows 和 **\_int64**的 64 位 Windows)。 例如，假设要移植的以下代码：

  ```cpp
  ImageBase = (PVOID)((ULONG)ImageBase | 1);
  ```

  移植过程的一部分，则会更改代码，如下所示：

  ```cpp
  ImageBase = (PVOID)((ULONG_PTR)ImageBase | 1);
  ```

  使用**UINT**\_**PTR**并**INT**\_**PTR**在适当的位置 （并且您不确定它们是否必需的没有任何危害只是在用例中使用它们）。 不强制转换的类型指针**ULONG**，**长**， **INT**， **UINT**，或**DWORD**。

  **请注意****处理**定义为**void \\** <em>因此类型上强制转换、 **处理</em>* 值**ULONG**值以测试、 设置或清除低两位是编程错误。  

     

- 使用**PtrToLong**并**PtrToUlong**要截断的指针。

  如果必须截断为 32 位值的指针，使用**PtrToLong**或**PtrToUlong**函数 (在中定义*Basetsd.h*)。 此函数禁用调用的持续时间的指针截断警告。

  谨慎使用这些函数。 截断指针变量时使用这些函数之一后，永远不会转换得到**长**或**ULONG**回指针。 这些函数将截断高 32 位的一个地址，这通常需要访问最初引用的指针的内存。 使用这些功能而无需仔细考虑将导致代码不太可靠。

### <a name="data-structures-and-structure-alignment"></a>数据结构和结构对齐方式

-   请仔细检查所有使用的数据结构的指针。

    以下是常见的问题区域：

    -   存储在磁盘上或 32 位进程与交换的数据结构。
    -   显式和隐式具有指针的联合。
    -   安全描述符。

<!-- -->

-   使用[**字段\_偏移量**](https://msdn.microsoft.com/library/windows/hardware/ff545727)宏。

    例如：

    ```cpp
    struct xx {
       DWORD NumberOfPointers;
       PVOID Pointers[1];
    };
     
    ```

    以下分配是在 64 位 Windows 中不正确，因为编译器将填充与附加的 4 个字节进行的 8 字节对齐要求的结构：

    ```cpp
    malloc(sizeof(DWORD)+100*sizeof(PVOID)); 
     
    ```

    下面介绍了如何正确执行：

    ```cpp
    malloc(FIELD_OFFSET(struct xx, Pointers) +100*sizeof(PVOID));
    ```

-   使用**类型\_对齐**宏。

    **类型\_对齐**宏将返回在当前平台上给定的数据类型的对齐需求。 例如：

    ```cpp
    TYPE_ALIGNMENT(KFLOATING_SAVE) == 4 on x86, 8 on Itanium
    TYPE_ALIGNMENT(UCHAR) == 1 everywhere
    ```

    例如，代码如下：

    ```cpp
    ProbeForRead(UserBuffer, UserBufferLength, sizeof(ULONG));
    ```

    变得更易于移植到更改时：

    ```cpp
    ProbeForRead(UserBuffer, UserBufferLength, TYPE_ALIGNMENT(ULONG));
    ```

-   监视公共内核结构中的数据类型更改。

    例如，**信息**字段中 IO\_状态\_块结构现在是类型的**ULONG\_PTR**。

-   使用结构封装指令时务必小心。

    在 64 位 Windows 上的数据结构未对齐，如果例程操纵结构，如[ **RtlCopyMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff561808)并**memcpy**，不会发生错误。 相反，它们将引发异常。 例如：

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

    可以使用**未对齐**宏以解决此问题：

    ```cpp
    void SetPointer(void *p) {
        struct Buffer s;
        *(UNALIGNED void *)&s.ptr = p;
    }
    ```

    遗憾的，使用**未对齐**宏是非常昂贵的基于 Itanium 处理器上。 更好的解决方案是将 64 位值和指针放在该结构的开头。

    **请注意**  如果可能，避免在同一个标头文件中使用不同的封装级别。

     

### <a name="additional-information"></a>其他信息

-   [在 64 位驱动程序支持 32 位 I/O](supporting-32-bit-i-o-in-your-64-bit-driver.md)

-   [获取已准备的 64 位 Windows](https://msdn.microsoft.com/library/windows/desktop/aa384198) （移植指南的用户模式应用程序）

 

 




